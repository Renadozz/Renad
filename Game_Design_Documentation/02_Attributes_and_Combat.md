# Attributes, Combat, Formulas, and Progression

## Linked documents

[Status effects and consumables](03_Status_Effects_and_Consumables.md) · [Player skills](04_Player_and_Skills.md) · [Equipment](05_Equipment_and_Drop_Pools.md) · [Economy](07_Economy_Market_and_Alchemy.md) · [Enemy codex](12_Enemy_Codex.md) · [Enemy AI](13_Enemy_AI_Patterns.md) · [Boss patterns](14_Boss_Patterns.md)

## Canonical data ownership

All combatants use the shared attributes below. Values marked **Player-only** or **Enemy-only** are stored only for that entity type. Encounter-template properties are deliberately not enemy attributes; they belong to [Encounter spawns](11_Encounter_Spawns.md).

|Attribute / state|Player|Enemy|Meaning and storage rule|
|---|:---:|:---:|---|
|Level|Yes|Yes|Integer level used for progression, encounter balance, and content gates.|
|Max Health; Current Health|Yes|Yes|Combatants are defeated at `Current Health <= 0`. Current Health is clamped between 0 and Max Health.|
|Max Mana; Current Mana|Yes|No|Only the Player pays Mana for Skills. Enemies use cooldown-driven AI and never have or spend Mana.|
|Physical Attack|Yes|Yes|Base for Physical damage.|
|Magic Power|Yes|Yes|Base for Magic damage and Magic-based DoTs.|
|Defense|Yes|Yes|Mitigates Physical damage.|
|Magical Defense|Yes|Yes|Mitigates Magic damage.|
|Speed|Yes|Yes|Determines action-gauge gain and time until the next action. Minimum effective value is 1.|
|Accuracy|Yes|Yes|Used only for Physical hit checks.|
|Evasion|Yes|Yes|Reduces incoming Physical hit chance.|
|Critical Chance; Critical Damage|Yes|Yes|Used only after a Physical hit. Default Critical Damage is 150%.|
|Global Status Resistance; specific Status Resistance|Yes|Yes|Subtracts from a status's base chance. Specific resistance is optional per Status.|
|Fire; Water; Earth; Air; Darkness; Holy Resistance|Yes|Yes|Reduces or increases Damage of the matching element. Neutral Damage has no elemental resistance step.|
|Physical Penetration; Magic Penetration|Yes|Yes|Reduces target Defense or Magical Defense before mitigation. Usually granted by Equipment, Skills, or boss mechanics.|
|Element Damage Bonus|Yes|Yes|Outgoing multiplier for a named element.|
|Damage Reduction|Yes|Yes|Final incoming-Damage reduction after mitigation, Resistance, and Critical. Capped at 75%.|
|Healing Received; Barrier Strength; Lifesteal|Yes|Yes|Derived modifiers used by relevant skills/effects. Enemies use them only when their AI or boss pattern grants them.|
|Action Gauge; cooldown map; active-effect map|Yes|Yes|Runtime combat state. The action gauge is from 0 to under 100 immediately after an action.|
|Equipment; Accessory Slot; Backpack; Gold; Skill Points; Experience|Yes|No|Player progression and inventory state. The Player has exactly one Accessory Slot.|
|AI Pattern ID; Rank; Element Types; Combat Role; Loot Profile ID|No|Yes|Enemy definition data. AI Pattern IDs resolve to [Enemy AI patterns](13_Enemy_AI_Patterns.md); Loot Profile data resolves to [Enemy Codex](12_Enemy_Codex.md).|
|Quest/contract drop flags; spawn flags|No|Yes|Runtime eligibility flags: active quest, incomplete objective, unique/boss state, and scripted-spawn conditions.|
|Encounter Template ID; template weight; respawn rule; area scaling|No|No|Stored on the encounter template, never on an individual enemy.|

## Player baseline growth

The game has no fixed class. Build identity comes from Equipment, Skills, passive selection, one Accessory, Grade Effects, and Grade Passives. The following formulas establish level-only base stats before Equipment and temporary effects.

```text
Max Health(L)       = 260 + 37 × (L - 1)
Max Mana(L)         = 60 + 7 × (L - 1)
Physical Attack(L)  = 25 + 4 × (L - 1)
Magic Power(L)      = 25 + 4 × (L - 1)
Defense(L)          = 14 + Floor(1.4 × (L - 1))
Magical Defense(L)  = 14 + Floor(1.4 × (L - 1))
Speed(L)            = 10 + Floor((L - 1) / 15)
Accuracy(L)         = 75 + Floor((L - 1) / 5)
Evasion(L)          = 5% + Floor((L - 1) / 10)
Critical Chance(L)  = 5% + Floor((L - 1) / 10)
```

|Level|Max HP|Max MP|PAtk / MPow|Def / MDef|Speed|Accuracy|Evasion / Crit|
|---:|---:|---:|---:|---:|---:|---:|---:|
|1|260|60|25|14|10|75|5%|
|25|1,148|228|121|47|11|79|7%|
|50|2,073|403|221|82|13|84|9%|
|75|2,998|578|321|117|14|89|12%|
|100|3,923|753|421|152|16|94|14%|

## Current-stat calculation and modifier stacking

```text
Total Relative Modifier = Sum(all valid relative modifiers for that stat)
Current Flat Stat = Max(0, Floor(Base Flat Stat × (1 + Total Relative Modifier)))

Current Percentage-Point Stat = Base Points
  + Equipment Points + Passive Points + Buff Points + Debuff Points

Effective Speed = Max(1, Floor(Base Speed × (1 + Total Speed Modifier)))
```

|Stat|Stack form|Cap / floor|
|---|---|---|
|Physical Attack; Magic Power; Defense; Magical Defense; Speed|Relative modifiers add before multiplying the base value.|Relative total: -75% to +100%; Speed minimum 1.|
|Accuracy|Percentage points.|No direct cap; final Physical hit chance is capped.|
|Evasion|Percentage points.|85% cap.|
|Critical Chance|Percentage points.|75% cap.|
|Global Status Resistance|Percentage points.|-50% to 80%.|
|Specific Status Resistance|Percentage points.|-50% to 100%.|
|Elemental Resistance|Percentage points.|-75% to 75%.|
|Damage Reduction|Percentage points.|0% to 75%.|

**Example — current Physical Attack:** Base PAtk 200, Equipment +30%, `Berserk` +15%, `Weakness` -20%. Total modifier = `0.30 + 0.15 - 0.20 = 0.25`; Current PAtk = `Floor(200 × 1.25) = 250`.

## Action gauge, action lifecycle, and durations

Every combatant begins combat with `Action Gauge = 0`. The combat engine advances time to the next actor instead of resolving in fixed round order.

```text
Time Until Action = (100 - Current Action Gauge) / Effective Speed

1. Calculate Time Until Action for every living combatant.
2. Advance time by the smallest positive result.
3. Add Effective Speed × advanced time to every living combatant's gauge.
4. If tied, Player acts before Enemy; among Enemies use encounter-slot order.
5. The selected actor resolves one complete action.
6. Subtract 100 from that actor's gauge; retain any excess gauge.
7. Autosave only after the whole lifecycle is complete.
```

**Gauge example:** Player Speed 20, Goblin Speed 12, Mage Speed 10; all gauges start at 0.

|Event|Advanced time|Player gauge|Goblin gauge|Mage gauge|Result|
|---|---:|---:|---:|---:|---|
|Start|0.000|0|0|0|No actor is ready.|
|Player becomes ready|5.000|100|60|50|Player acts; after action Player gauge becomes 0.|
|Goblin becomes ready|3.333|66.67|100|83.33|Goblin acts; after action Goblin gauge becomes 0.|
|Mage becomes ready|1.667|100|20|100|Player/Mage tie; Player acts first by tie rule.|

### Canonical action lifecycle

```text
Start of actor's own action
  → reduce that actor's cooldowns by 1, minimum 0
  → check action-denial control (Stun, Sleep, Freeze)
  → if denied: consume the action; do not pay Mana; do not choose a Skill
  → otherwise select one valid Skill, Basic Attack, or Item action
  → validate equipment, target, Mana, cooldown, and duplicate-effect rule
  → pay Mana when applicable
  → resolve hit/critical or automatic Magic hit
  → resolve Damage, statuses, weapon traits, Grade Effects, and reactions
  → resolve end-of-action DoT, regeneration, and duration countdown
  → subtract 100 Gauge; checkpoint autosave
```

Effects always count down at the end of the **affected unit's own completed action**. Effects applied in that same action do not immediately lose one duration. A denied action still counts as a completed action for duration countdowns.

## Physical hit, critical, and Physical damage

```text
Raw Hit Chance = Attacker Accuracy - Target Evasion
Final Hit Chance = Clamp(Raw Hit Chance, 10%, 95%)
Physical Hit = Random(0,1) < Final Hit Chance

Final Critical Chance = Clamp(Attacker Critical Chance, 0%, 75%)
Critical = Physical Hit AND Random(0,1) < Final Critical Chance
Critical Multiplier = Attacker Critical Damage; default 1.50

Combined Physical Penetration =
  1 - ((1 - Equipment Physical Penetration) × (1 - Skill Defense Ignore))
Effective Defense = Max(0, Target Current Defense × (1 - Combined Physical Penetration))
Physical Mitigation = 100 / (100 + Effective Defense)
Raw Physical Damage = Attacker Current Physical Attack × Skill Coefficient
Damage Before Element = Raw Physical Damage × Physical Mitigation
```

**Physical example:** Attacker has 200 PAtk, uses `P130`, has 25% Equipment Penetration, and the Skill ignores 20% Defense. Target has 150 Defense, 10% Fire Resistance, and the hit is a Fire Physical critical.

```text
Combined Penetration = 1 - ((1 - 0.25) × (1 - 0.20)) = 0.40
Effective Defense = 150 × (1 - 0.40) = 90
Mitigation = 100 / (100 + 90) = 0.526315...
Raw Damage = 200 × 1.30 = 260
Before Element = 260 × 0.526315... = 136.84
After 10% Fire Resistance = 136.84 × 0.90 = 123.16
After 150% Critical = 123.16 × 1.50 = 184.74
Final Damage before Barrier = Floor(184.74) = 184
```

## Magic damage, elements, final modifiers, and Barrier

Magic always hits and cannot critically hit unless an explicit future Skill says otherwise.

```text
Combined Magic Penetration =
  1 - ((1 - Equipment Magic Penetration) × (1 - Skill Magical Defense Ignore))
Effective Magical Defense = Max(0, Target Current Magical Defense × (1 - Combined Magic Penetration))
Magic Mitigation = 100 / (100 + Effective Magical Defense)
Raw Magic Damage = Attacker Current Magic Power × Skill Coefficient
Damage Before Element = Raw Magic Damage × Magic Mitigation

Total Element Resistance = Clamp(
  Base + Equipment + Passive + Buff + Debuff + Ward,
  -75%, 75%
)
Element Multiplier = 1 - Total Element Resistance
Outgoing Element Multiplier = 1 + Attacker Element Damage Bonus

Damage Before Critical = Damage Before Element
  × Element Multiplier × Outgoing Element Multiplier × Skill Conditional Multiplier
Damage After Critical = Damage Before Critical × (Critical ? Critical Multiplier : 1)
Damage After Reduction = Damage After Critical × (1 - Target Damage Reduction)
Final Damage = Max(1, Floor(Damage After Reduction))

Barrier Absorbed = Min(Current Barrier, Final Damage)
Health Damage = Final Damage - Barrier Absorbed
New Barrier = Current Barrier - Barrier Absorbed
```

**Magic example:** 260 Magic Power uses `M120 Water` against 180 Magical Defense, 30% Water Resistance, 10% outgoing Water Damage, and 15% Damage Reduction.

```text
Raw Magic = 260 × 1.20 = 312
Magic Mitigation = 100 / (100 + 180) = 0.357142...
Before Element = 312 × 0.357142... = 111.43
Element and outgoing = 111.43 × (1 - 0.30) × 1.10 = 85.80
After Damage Reduction = 85.80 × (1 - 0.15) = 72.93
Final Damage = Floor(72.93) = 72
```

Neutral Damage skips Element Resistance and Element Damage Bonus. Negative Resistance increases Damage: `-25%` Resistance produces multiplier `1 - (-0.25) = 1.25`.

## Statuses, DoTs, healing, Lifesteal, and Barrier creation

```text
Total Status Resistance = Clamp(Global Status Resistance + Specific Status Resistance, -50%, 100%)
Final Status Chance = Clamp(Base Status Chance - Total Status Resistance, 0%, 100%)
Status applies when Random(0,1) < Final Status Chance

DoT Damage = Max(1, Floor(Stored Source Power × DoT Coefficient × relevant mitigation))
Healing = Floor(Base Healing × (1 + Healing Received Modifier))
Lifesteal Healing = Floor(Health Damage Dealt × Lifesteal Percentage × (1 + Healing Received Modifier))
Created Barrier = Floor(Base Barrier × (1 + Barrier Strength Modifier))
```

A status is skipped if the target already has the same status with at least one own action remaining. Boss immunities are checked before chance resolution. `Health Damage Dealt` is post-Barrier damage; Barrier-only damage never produces Lifesteal.

|DoT|Snapshot|Coefficient|Trigger|Special rule|
|---|---|---:|---|---|
|Burn|Source Magic Power|0.45|End of target action|Fire Magic mitigation; cannot Crit.|
|Poison|Source Magic Power|0.35|End of target action|Neutral Physical mitigation; ignores 50% Defense; cannot Crit.|
|Bleeding|Source Physical Attack|0.45|After target uses a Physical Skill or takes a Physical critical hit|Neutral Physical mitigation; cannot Crit.|
|Curse|Source Magic Power|0.40|End of target action|Darkness Magic mitigation; cannot Crit.|

**Status example:** A `65%` Rooted effect targets a unit with 15% Global Status Resistance and 10% Rooted Resistance. Total resistance is 25%; final chance is `Clamp(65 - 25, 0, 100) = 40%`.

**Barrier and Lifesteal example:** A 200-Damage hit strikes a 70-Barrier target. Barrier absorbs 70; Health Damage is 130. At 10% Lifesteal and 20% Healing Received, healing is `Floor(130 × 0.10 × 1.20) = 15`.

## Equipment value, upgrades, grades, and item sale price

```text
Blacksmith Multiplier = 1 + (Upgrade Level × 0.10)
Blacksmith Flat Value = Floor(Original +0 Flat Value × Blacksmith Multiplier)
Blacksmith Percentage Value = RoundToOneDecimal(Original +0 Percentage × Blacksmith Multiplier)

Grade Flat Value = Blacksmith Flat Value + Floor(Blacksmith Flat Value × Grade Bonus)
Grade Percentage Value = RoundToOneDecimal(Blacksmith Percentage × (1 + Grade Bonus))

Sale Value = Floor(Original +0 Base Value × 0.25)
```

Grade bonuses are Common 0%, Uncommon 10%, Rare 20%, Epic 30%, Legendary 40%, Mythic 50%. Trait values, Grade Effect rolls, and Grade Passive rolls never scale. Upgrade and Grade improvements never increase sell value, preventing profit through upgrading then resale.

**Upgrade example:** A +0 Sword with 100 PAtk at `+3` has `Floor(100 × 1.30) = 130` PAtk before Grade. If it is Epic: `130 + Floor(130 × 0.30) = 169` PAtk. Its 1,000 Gold base sale value remains `Floor(1,000 × .25) = 250` Gold.

## Experience curve and reward resolution

`XP to next level` is the XP needed to advance from the listed level. The curve deliberately starts approachable and rises sharply after Level 40. Total XP from Level 1 to Level 100 is **1,820,650**.

|Current Level|XP to Next Level|Cumulative XP to Next Level|
|---:|---:|---:|
|1|220|220|
|2|310|530|
|3|400|930|
|4|490|1,420|
|5|580|2,000|
|6|670|2,670|
|7|760|3,430|
|8|850|4,280|
|9|940|5,220|
|10|1,030|6,250|
|11|1,200|7,450|
|12|1,380|8,830|
|13|1,560|10,390|
|14|1,740|12,130|
|15|1,920|14,050|
|16|2,100|16,150|
|17|2,280|18,430|
|18|2,460|20,890|
|19|2,640|23,530|
|20|2,820|26,350|
|21|3,000|29,350|
|22|3,300|32,650|
|23|3,600|36,250|
|24|3,900|40,150|
|25|4,200|44,350|
|26|4,500|48,850|
|27|4,800|53,650|
|28|5,100|58,750|
|29|5,400|64,150|
|30|5,700|69,850|
|31|6,000|75,850|
|32|6,300|82,150|
|33|6,600|88,750|
|34|6,900|95,650|
|35|7,200|102,850|
|36|7,500|110,350|
|37|7,800|118,150|
|38|8,100|126,250|
|39|8,400|134,650|
|40|8,700|143,350|
|41|9,500|152,850|
|42|10,000|162,850|
|43|10,500|173,350|
|44|11,000|184,350|
|45|11,500|195,850|
|46|12,000|207,850|
|47|12,500|220,350|
|48|13,000|233,350|
|49|13,500|246,850|
|50|14,000|260,850|
|51|14,500|275,350|
|52|15,000|290,350|
|53|15,500|305,850|
|54|16,000|321,850|
|55|16,500|338,350|
|56|17,000|355,350|
|57|17,500|372,850|
|58|18,000|390,850|
|59|18,500|409,350|
|60|19,000|428,350|
|61|20,500|448,850|
|62|21,250|470,100|
|63|22,000|492,100|
|64|22,750|514,850|
|65|23,500|538,350|
|66|24,250|562,600|
|67|25,000|587,600|
|68|25,750|613,350|
|69|26,500|639,850|
|70|27,250|667,100|
|71|28,000|695,100|
|72|28,750|723,850|
|73|29,500|753,350|
|74|30,250|783,600|
|75|31,000|814,600|
|76|31,750|846,350|
|77|32,500|878,850|
|78|33,250|912,100|
|79|34,000|946,100|
|80|34,750|980,850|
|81|37,000|1,017,850|
|82|37,800|1,055,650|
|83|38,600|1,094,250|
|84|39,400|1,133,650|
|85|40,200|1,173,850|
|86|41,000|1,214,850|
|87|41,800|1,256,650|
|88|42,600|1,299,250|
|89|43,400|1,342,650|
|90|44,200|1,386,850|
|91|45,000|1,431,850|
|92|45,800|1,477,650|
|93|46,600|1,524,250|
|94|47,400|1,571,650|
|95|48,200|1,619,850|
|96|49,000|1,668,850|
|97|49,800|1,718,650|
|98|50,600|1,769,250|
|99|51,400|1,820,650|

### XP formula by band

```text
L 1–10:  XP(L→L+1) = 220 + 90 × (L - 1)
L 11–20: XP(L→L+1) = 1,200 + 180 × (L - 11)
L 21–40: XP(L→L+1) = 3,000 + 300 × (L - 21)
L 41–60: XP(L→L+1) = 9,500 + 500 × (L - 41)
L 61–80: XP(L→L+1) = 20,500 + 750 × (L - 61)
L 81–99: XP(L→L+1) = 37,000 + 800 × (L - 81)
```

```text
Enemy XP = fixed Enemy Codex XP × (1 + Experience Gain modifier)
Enemy Gold = Floor(fixed Enemy Codex Gold × (1 + Gold Find modifier))
Quest XP = Floor(listed base Quest XP × World-Tier XP coefficient)

Loot order:
XP/Gold → guaranteed materials → supplemental crafting rolls → Equipment roll → conditional Quest/Proof drop
```

The Tier coefficient and campaign pace check are in [Town, quests, and contracts](09_Town_Quests_and_Contracts.md#quest-xp-scaling-and-campaign-pace-validation). Experience Gain affects enemy rewards only unless a Quest explicitly says otherwise.

## Difficulty checkpoints

|Encounter|Target player level|Expected state|Intent|
|---|---:|---|---|
|Tier 1 normal group|1–12|Starter equipment; Tier I Skills|Three to six player actions per normal enemy; learn Gauge, statuses, and basic Item use.|
|Tier 3 Elite / Unique|28–40|Rare or upgraded Uncommon; one defensive Skill|Requires target priority and counter-potion preparation.|
|Regional boss|63–75|Rare/Epic build; cleansing medicine; Tier V choices|Cannot be solved by raw damage alone.|
|Dragon elite|88–95|Epic/early Legendary; specific elemental preparation|Punishes a single-stat build.|
|Ancient Dragon|94–98|Late Epic/Legendary; Tier VI skills; crafted endgame supply|Endurance and phase-management benchmark.|
|Dragon King|95–100|Focused Legendary/Mythic or upgraded Epic build; defense plus recovery option|Expected 35–55 Player actions and multi-phase response.|

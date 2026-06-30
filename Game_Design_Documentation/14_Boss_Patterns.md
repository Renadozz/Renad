# Area-Final Boss Patterns

## Linked documents

[Enemy Codex](12_Enemy_Codex.md) · [Enemy AI](13_Enemy_AI_Patterns.md) · [Town and Contracts](09_Town_Quests_and_Contracts.md) · [Status effects](03_Status_Effects_and_Consumables.md)

## Boss encounter rules

|Rule|Implementation|
|---|---|
|Finality|Each regional boss is only accessible for its Story quest and, after that, its matching Boss Challenge Contract.|
|Summons|Only a boss pattern that explicitly lists `Summon Minion` may summon; at most two summon actions and never above three living enemies.|
|Phase transition|A phase becomes active when the boss's current HP percentage is within its range. `Phase Rage` only occurs once.|
|Status safety|Boss AI follows normal duplicate-status rules, cooldowns, and target validity.|
|Reward safety|Sigils never repeat. Boss Challenge Proofs only drop while that exact Challenge Contract is active.|
|Final boss|Dragon King has no repeatable contract, no summons, and no ordinary drops.|

## Boss-only skill definitions

|Skill|Boss|Effect|Cooldown|
|---|---|---|---|
|Totem Command|Goblin King|Summon one Goblin Scout first, then Goblin Dagger, only if fewer than 3 living enemies; max 2 uses.|5|
|Royal Tremor|Goblin King|M125 Earth; 50% Slow for 2 own actions.|4|
|Runic Reversal|Ruin Guardian|Gain Barrier 18% Max HP; then remove one negative status from self.|4|
|Guardian Verdict|Ruin Guardian|M130 Holy/Earth; 50% Magic Vulnerability for 2 own actions.|4|
|Glacier Shell|Frost Titan|Gain Barrier 20% Max HP and +15% Water Resistance for 2 own actions.|4|
|Magma Burst|Inferno Lord|M130 Fire/Earth; 60% Scorched for 2 own actions.|4|
|Veil of Dread|Shadow Lord|Gain Evasion Up +25% and Magic Ward +25% for 2 own actions.|4|
|Oath Barrier|Oracle|Gain Barrier 18% Max HP and Cleanse one negative status.|4|
|Cleansing Dawn|Oracle|Restore 15% Max HP and remove one negative status.|4|
|Draconic Cataclysm|Dragon King|M165 Fire/Air/Darkness; resolve Burn, Winded, and Curse separately using 55% base chance each.|5|

<a id="goblin-king"></a>
## Goblin King

**Area:** King's Clearing  
**Quest state:** S-T6-01 / R-EKC-B01  
**Pattern type:** Area-final boss

|Phase|Priority sequence|Purpose|
|---|---|---|
|Opening (100–71%)|Rally Command → All Friendlies if adds exist; otherwise Totem Command if fewer than 3 living; then Armor Break Strike.|Establishes a physical-pressure group.|
|Ritual pressure (70–36%)|Royal Tremor if no Slow; Totem Command if a summon slot is available; Heavy Attack fallback.|Earth control plus add management.|
|Crown rage (≤35%)|Phase Rage once if no Berserk; Stun Slam if no Stun; Heavy Attack.|More damage and speed without infinite summon loops.|

**Hard rules:** Can summon at most two times. Story Sigil only during S-T6-01; Challenge Proof only during R-EKC-B01.

<a id="ruin-guardian"></a>
## Ruin Guardian

**Area:** Ruin Guardian Chamber  
**Quest state:** S-T6-02 / R-ARGC-B01  
**Pattern type:** Area-final boss

|Phase|Priority sequence|Purpose|
|---|---|---|
|Opening (100–71%)|Runic Reversal → Barrier; Guardian Verdict if player has no Magic Vulnerability; Stun Slam.|Barrier-driven construct opener.|
|Oath trial (70–36%)|Earthquake if no Slow; Judgment Beam if no Magic Vulnerability; Fortify.|Alternates physical and magical defense pressure.|
|Broken oath (≤35%)|Phase Rage once; Guardian Verdict; Heavy Attack.|Forces a high-pressure finish.|

**Hard rules:** Never summons. Air Sigil only during S-T6-02; Challenge Proof only during R-ARGC-B01.

<a id="frost-titan"></a>
## Frost Titan

**Area:** Summit Shrine  
**Quest state:** S-T6-03 / R-WSS-B01  
**Pattern type:** Area-final boss

|Phase|Priority sequence|Purpose|
|---|---|---|
|Opening (100–71%)|Glacier Shell; Chilling Mist if no Wet; Avalanche if no Freeze or Slow.|Sets Wet before control.|
|Whiteout (70–36%)|Avalanche; Heavy Attack; Glacier Shell when Barrier expires.|Maintains Freeze/Slow pressure.|
|Shatterpeak (≤35%)|Phase Rage once; Avalanche; Stun Slam.|Fastest action-gauge phase.|

**Hard rules:** Never summons. Water Sigil only during S-T6-03; Titan Glacier Heart only during R-WSS-B01.

<a id="inferno-lord"></a>
## Inferno Lord

**Area:** Inferno Core  
**Quest state:** S-T6-04 / R-FIC-B01  
**Pattern type:** Area-final boss

|Phase|Priority sequence|Purpose|
|---|---|---|
|Opening (100–71%)|Magma Burst if no Scorched; Summon Minion if fewer than 3 living; Infernal Nova if no Burn.|Creates Fire setup and controlled add pressure.|
|Core overload (70–36%)|Infernal Nova; Flame Wave; Summon Minion if an add slot remains.|Burn pressure across repeated actions.|
|Unbound inferno (≤35%)|Phase Rage once; Combustion-style Heavy Fire strike against Burned/Scorched Player; Infernal Nova fallback.|Rewards the boss for its setup state.|

**Hard rules:** Summons at most two times: Flame Elemental first, Ember Hound second. Fire Sigil only during S-T6-04; Inferno Ember only during R-FIC-B01.

<a id="shadow-lord"></a>
## Shadow Lord

**Area:** Dread Throne  
**Quest state:** S-T6-05 / R-DDT-B01  
**Pattern type:** Area-final boss

|Phase|Priority sequence|Purpose|
|---|---|---|
|Opening (100–71%)|Veil of Dread; Voidstorm if no Shadow Mark; Summon Minion if fewer than 3 living.|Starts with defense and Darkness setup.|
|Court of shadows (70–36%)|Life Drain if HP ≤ 55%; Fear Howl if no Fear; Soul Rend against Magic-Focused Player.|Sustain and anti-caster pressure.|
|Dread eclipse (≤35%)|Phase Rage once; Voidstorm; Summon Minion if allowed.|High-speed final Darkness phase.|

**Hard rules:** Summons at most two times: Shade first, Dread Knight second. Darkness Sigil only during S-T6-05; Dread Veil Fragment only during R-DDT-B01.

<a id="oracle"></a>
## Oracle

**Area:** Oracle Chamber  
**Quest state:** S-T6-06 / R-HOC-B01  
**Pattern type:** Area-final boss

|Phase|Priority sequence|Purpose|
|---|---|---|
|Opening (100–71%)|Oath Barrier; Solar Verdict if no Holy Mark; Judgment Beam if no Magic Vulnerability.|Holy setup and protection.|
|Trial of mercy (70–36%)|Cleansing Dawn if HP ≤ 55%; Heal if HP ≤ 40%; Solar Verdict.|Self-sustain guarded by cooldowns.|
|Final judgment (≤35%)|Phase Rage once; Solar Verdict; Judgment Beam; Holy Bolt fallback.|No summon; direct final verdict pressure.|

**Hard rules:** Never summons. Holy Sigil only during S-T6-06; Oracle’s Trial Seal only during R-HOC-B01.

<a id="ancient-dragon"></a>
## Ancient Dragon

**Area:** Ancient Nest  
**Quest state:** S-DRAGON-04 / R-DRAN-B01  
**Pattern type:** Area-final boss

|Phase|Priority sequence|Purpose|
|---|---|---|
|Opening (100–71%)|Scale Harden; Dragonfire Breath if no Burn; Storm Wing if no Winded.|Multi-element setup with defense.|
|Ancient memory (70–36%)|Eclipse if no Curse; Summon Minion if fewer than 3 living; Dragonfire Breath.|Adds battlefield pressure but respects 3-unit limit.|
|Elder rage (≤35%)|Phase Rage once; Storm Wing; Eclipse; Dragonfire Breath.|Boss Magic deals +10% damage.|

**Hard rules:** Summons at most two times: Dragon Whelp first, Dragon Servant second. It is repeatable after S-DRAGON-04; Story Memory Scale and Challenge Memory Scale have separate conditions.

<a id="dragon-king"></a>
## Dragon King

**Area:** Dragon King's Lair  
**Quest state:** S-DRAGON-05  
**Pattern type:** Area-final boss

|Phase|Priority sequence|Purpose|
|---|---|---|
|Dominion seal (100–76%)|Scale Harden; Dragonfire Breath if no Burn; Storm Wing if no Winded; Eclipse if no Curse.|Starts the three-element setup.|
|Sovereign assault (75–41%)|Armor Break Strike if no Armor Break; Draconic Cataclysm; Dragonfire Breath/Storm Wing/Eclipse according to missing statuses.|Combines physical break with three-element Magic pressure.|
|Last seal (≤40%)|Phase Rage once; Draconic Cataclysm; Armor Break Strike; repeat missing-status priority.|All Boss Magic has +25% damage and +10% status chance.|

**Hard rules:** Always alone. Never summons. Cannot be repeated. Enemy reward is 0 XP/0 Gold/none; only `Dragon King’s Seal` drops, while S-DRAGON-05 completion awards 6,500 quest XP.


## Boss-pattern coverage

|Area|Area-final boss|Pattern status|
|---|---|---|
|King's Clearing|Goblin King|Defined|
|Ruin Guardian Chamber|Ruin Guardian|Defined|
|Summit Shrine|Frost Titan|Defined|
|Inferno Core|Inferno Lord|Defined|
|Dread Throne|Shadow Lord|Defined|
|Oracle Chamber|Oracle|Defined|
|Ancient Nest|Ancient Dragon|Defined|
|Dragon King's Lair|Dragon King|Defined|

The regional boss names, story IDs, conditional proofs, and base rewards are cross-validated in [12_Enemy_Codex.md](12_Enemy_Codex.md).

## Final-boss stat target override

The Dragon King is **Level 100** and uses the Codex profile `HP 21,500 / P 1,080 / M 1,015 / D 620 / MD 620`. This deliberately exceeds the Ancient Dragon’s offensive pressure while retaining a longer HP pool and the three-element phase sequence. The target Player band remains Level 95–99; Level 90 is the minimum preparation recommendation, not the balance target.


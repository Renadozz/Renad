# Blacksmith, Enchanter, and Weapon Traits

## Linked documents

[Equipment](05_Equipment_and_Drop_Pools.md) · [Item prices](06_Item_Price_Catalog.md) · [Enemy material sources](12_Enemy_Codex.md) · [Player passives](04_Player_and_Skills.md)

## Blacksmith

|Upgrade|Success|Materials|Gold|
|---|---:|---|---:|
|+0 → +1|90%|3× Iron Scrap|50|
|+1 → +2|80%|2× Iron Scrap; 2× Iron Ore|150|
|+2 → +3|65%|3× Crystal Shard; 1× Magic Crystal|350|
|+3 → +4|45%|2× Obsidian Fragment; 1× Molten Core|700|
|+4 → +5|25%|1× Ancient Dragon Scale; 1× Ancient Dragon Fang; 1× Obsidian Core|1,500|

```text
Multiplier = 1 + (Upgrade Level × 0.10)
Flat original +0 value = Floor(+0 value × Multiplier)
Percentage original +0 value = RoundToOneDecimal(+0 value × Multiplier)
```

All calculations use the original +0 item values, never the prior upgrade result.

## Enchanter grades

|Upgrade|Success|Materials|Gold|Weapon trait result|
|---|---:|---|---:|---|
|Common → Uncommon|80%|2× Enchantment Dust|100|None|
|Uncommon → Rare|60%|2× Enchantment Fragment|300|None|
|Rare → Epic|40%|2× Enchantment Crystal|700|One compatible Epic trait|
|Epic → Legendary|20%|2× Dragon Rune; 1× Ancient Dragon Scale|1,500|Keep Epic; add one compatible Legendary trait|
|Legendary → Mythic|8%|3× Dragon Rune; 1× Mythic Ember; 1× Ancient Dragon Fang|3,000|Keep prior traits; add one compatible Mythic trait|

|Grade|Original item-value bonus|
|---|---:|
|Common|0%|
|Uncommon|10%|
|Rare|20%|
|Epic|30%|
|Legendary|40%|
|Mythic|50%|

Trait values never receive Blacksmith or Grade scaling.

## Eligibility and failure

|Rule|Canonical behavior|
|---|---|
|Eligible gear|Weapons, Shields, Armor, and Helmets when their item data permits. Accessories are never eligible.|
|Trait eligibility|Sword, Great Sword, Axe, Hammer, Staff, Bow, Dagger, and Shield only.|
|Failure|Consumes stated materials and Gold; never breaks or downgrades the item.|
|Quest safety|Quest Items, Sigils, and Dragon King's Seal cannot be upgraded, salvaged, enchanted, or disenchanted.|
|Drop cap|Legendary and Mythic do not drop and are not sold.|
|Trait persistence|Traits and their values are stored permanently until the Player uses the paid Trait Reroll service. Reroll count is stored on the individual item and never resets for that item.|
|No duplicate family|A weapon cannot receive two traits of the same family.|

## Materials

|System|Basic source path|
|---|---|
|Blacksmith|Tiered enemy material drops, contracts, bosses, salvage.|
|Enchanter|Disenchanting, unique contracts, boss challenges, Dragon content.|
|Exact source and quantities|[12_Enemy_Codex.md](12_Enemy_Codex.md)|
|All trait compatibility and pools|[Source_Blacksmith_Enchanter_Trait_System.md](Source_Blacksmith_Enchanter_Trait_System.md)|

## Salvage and disenchant

The source document's grade-based salvage and disenchant tables remain canonical. For any equipment item the Player must choose one destructive path:

```text
Sell → Gold
or Blacksmith Salvage → smithing material
or Enchanter Disenchant → enchanting material
```

The generated equipment base values and sale values are in [05_Equipment_and_Drop_Pools.md](05_Equipment_and_Drop_Pools.md) and [06_Item_Price_Catalog.md](06_Item_Price_Catalog.md).

## Grade Effects, Grade Passives, and Accessory override

- At Epic, Weapons/Shields gain one compatible random Epic Trait; Armor and Helmets gain one compatible random Epic Grade Effect.
- At Legendary, they keep prior effects, gain one Legendary Grade Effect, and gain one compatible permanent Grade Passive.
- At Mythic, they keep prior effects, gain one Mythic Grade Effect, and gain one additional compatible permanent Grade Passive.
- A Mythic two-hand Weapon gains **two** Mythic Grade Effects and **two** Mythic Grade Passives at Mythic.
- There is one Accessory slot. Accessories are never Blacksmith-upgraded, Enchanter-graded, salvaged, or disenchanted.

Full compatibility pools and totals are in [Equipment](05_Equipment_and_Drop_Pools.md).

## Direct Epic generation rule

Any **Weapon or Shield** generated at **Epic** Grade from an Elite, Unique, Regional Boss, Quest reward, or Market stock immediately rolls exactly one random compatible **Epic Trait**. Any **Armor or Helmet** generated at Epic Grade immediately rolls exactly one compatible **Epic Armor Grade Effect**. This makes direct Epic drops comply with the same first-roll rule as a successful `Rare → Epic` Enchanter upgrade. A directly generated Epic Item has no Grade Passive until the later Legendary upgrade succeeds.



## Detailed upgrade and grade workflow

### Blacksmith attempt

```text
1. Select an eligible Weapon, Shield, Armor, or Helmet at +0 to +4.
2. Show current original +0 values, projected next-level values, success chance, Gold, and materials.
3. Verify Backpack / Material inventory and Gold.
4. Consume the listed Gold and materials.
5. Roll success chance once.
6. On success: increase Upgrade Level by 1 and recalculate all original numeric values from +0.
7. On failure: retain item, Grade, Traits, Effects, Passives, and current Upgrade Level.
```

### Enchanter attempt

```text
1. Select an eligible Common through Legendary item; Accessories are invalid.
2. Show next Grade, material list, chance, effect/passive outcome, and trait compatibility preview.
3. Consume listed Gold and materials.
4. Roll success chance once.
5. On success: increase Grade; recalculate original numeric Item values from Grade Bonus.
6. If the new Grade is Epic: roll a random compatible Epic Weapon/Shield Trait or Armor Effect.
7. If Legendary/Mythic: retain previous rolls and add the next compatible Effect/Trait and Grade Passive(s).
8. On failure: no downgrade, no destruction, and no Trait loss.
```

### Material source map

|Material|Primary use|Farm / service source|
|---|---|---|
|Iron Scrap; Iron Ore; Crystal Shard; Magic Crystal|Early to mid Blacksmith levels|Direct Monster drops; Common/Uncommon/Rare salvage. See [craft-input sources](03_Status_Effects_and_Consumables.md#craft-input-source-matrix).|
|Obsidian Fragment; Molten Core; Obsidian Core|Late Blacksmith levels|Fire and Dragon enemies; Epic salvage; high-tier Contracts.|
|Ancient Dragon Scale; Ancient Dragon Fang|+4 → +5; late Enchanter requirements|Ancient Dragon and Dragon endgame content.|
|Enchantment Dust; Fragment; Crystal|Common→Epic grade path; rerolls|Disenchanting and Unique / Contract rewards.|
|Dragon Rune; Mythic Ember|Legendary/Mythic grades and rerolls|Dragon content; Ancient Dragon rewards.|

<a id="trait-and-grade-passive-rerolls"></a>
## Trait and Grade Passive rerolls

The Enchanter offers two high-cost services. Both reroll counters are stored per **individual Equipment Item** and never reset from unequipping, upgrading, grading, selling-related previews, or restocking. A newly generated Item begins with `TraitRerollCount = 0` and `PassiveRerollCount = 0`.

|Service|Eligible item|What changes|What remains|
|---|---|---|---|
|Trait Reroll|Epic, Legendary, or Mythic Weapon/Shield; Epic+ Armor uses Effect Reroll|Rerolls all Grade Traits/Grade Effects of the item at their current Grades. New rolls obey type, element, combat style, and no-duplicate-family rules.|Item type, base stats, upgrade level, Grade, built-in effect, and Grade Passives.|
|Grade Passive Reroll|Legendary or Mythic Weapon/Shield/Armor|Rerolls all Grade Passives on that item; a Mythic two-hand Weapon rerolls all three of its Passives.|Item type, base stats, upgrade level, Grade, built-in effect, and Grade Traits/Effects.|

```text
Trait Reroll Gold(n) = RoundUpTo50(7,500 × 1.60^n)
Trait Reroll Enchantment Crystals(n) = 2 + n
Trait Reroll Dragon Runes(n) = 0 when n = 0; otherwise 1 + Floor((n - 1) / 2)
Trait Reroll Mythic Ember = 1 only for a Mythic item

Passive Reroll Gold(n) = RoundUpTo50(10,000 × 1.70^n)
Passive Reroll Enchantment Crystals(n) = 3 + n
Passive Reroll Dragon Runes(n) = 1 + Floor(n / 2)
Passive Reroll Ancient Dragon Fang = 1 for Mythic items; 0 for Legendary items
```

`n` is the completed reroll count before the new attempt. Increase the matching counter by 1 immediately when the reroll begins; a reroll has no failure chance because the rising cost is the risk.

|Attempt number|Trait Reroll Gold|Passive Reroll Gold|Meaning|
|---:|---:|---:|---|
|1 (`n=0`)|7,500|10,000|First reroll on this item.|
|2 (`n=1`)|12,000|17,000|Already substantially more expensive.|
|3 (`n=2`)|19,200|28,900|Endgame sink.|
|4 (`n=3`)|30,750|49,150|Deliberately expensive; no reset on this item.|

A reroll does not allow duplicate Trait families, invalid elements, or invalid Weapon/Armor compatibility. The Item's sell value remains based on its original +0 Base Value, so rerolling cannot create a Gold loop.

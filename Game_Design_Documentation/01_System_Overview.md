# System Overview and Canonical Rules

## Linked documents

[Documentation index](00_README.md) · [Player and Skills](04_Player_and_Skills.md) · [Equipment](05_Equipment_and_Drop_Pools.md) · [Town and Quests](09_Town_Quests_and_Contracts.md) · [Enemy Codex](12_Enemy_Codex.md) · [Consistency Audit](16_Consistency_Audit.md)

## Game loop

```text
Town
  → select story quest or one repeatable contract
  → travel through City Gate to an unlocked area
  → resolve fixed encounter templates and combat
  → collect Gold, materials, equipment, and conditional Quest Items
  → return to Town
  → rest, sell/craft, upgrade, enchant, equip, and advance quests
```

## Permanent system boundaries

|System|Canonical rule|Source detail|
|---|---|---|
|Progression|World Tiers interleave Earth → Air → Water → Fire → Darkness → Holy; Dragon content is last.|[09_Town_Quests_and_Contracts.md](09_Town_Quests_and_Contracts.md)|
|Combat|One Player against a maximum of three living enemies; summons count toward that limit.|[02_Attributes_and_Combat.md](02_Attributes_and_Combat.md)|
|Active skills|All learned, currently valid active skills are usable; there are no active-skill slots.|[04_Player_and_Skills.md](04_Player_and_Skills.md)|
|Passives|Three Player passive slots plus 2 Grade Passives normally, or 3 with the Mythic two-hand Weapon exception.|[04_Player_and_Skills.md](04_Player_and_Skills.md)|
|Equipment grades|Drops and rewards may be Common through Epic; Legendary and Mythic are Enchanter-only.|[08_Blacksmith_and_Enchanter.md](08_Blacksmith_and_Enchanter.md)|
|Blacksmith|Every item tracks `+0` through `+5`; all scaling is from the original `+0` values.|[08_Blacksmith_and_Enchanter.md](08_Blacksmith_and_Enchanter.md)|
|Quest Items|Only exist while their exact quest/contract objective needs them. They use 0 backpack slots.|[09_Town_Quests_and_Contracts.md](09_Town_Quests_and_Contracts.md)|
|Autosave|Save only after permanent changes or fully completed action lifecycles.|[09_Town_Quests_and_Contracts.md](09_Town_Quests_and_Contracts.md)|
|Final boss|Dragon King is a one-time solo boss that drops only `Dragon King's Seal`; quest completion grants the story reward separately.|[14_Boss_Patterns.md](14_Boss_Patterns.md)|

## Canonical data ownership

|Data domain|Single owner|Referenced by|
|---|---|---|
|Core attributes, mitigation, action timing|[02_Attributes_and_Combat.md](02_Attributes_and_Combat.md)|Player, Skills, Enemies, Forms|
|Status definitions and removal effects|[03_Status_Effects_and_Consumables.md](03_Status_Effects_and_Consumables.md)|Skills, AI, Potions, Traits|
|Skill definitions and equipment requirements|[04_Player_and_Skills.md](04_Player_and_Skills.md)|Player UI, Enemy balance, Forms|
|Item definitions, stat blocks, item pools|[05_Equipment_and_Drop_Pools.md](05_Equipment_and_Drop_Pools.md)|Enemies, Market, Blacksmith, Enchanter|
|Prices and sellability|[06_Item_Price_Catalog.md](06_Item_Price_Catalog.md)|Market, loot UI, Forms|
|Recipes and material sources|[07_Economy_Market_and_Alchemy.md](07_Economy_Market_and_Alchemy.md)|Market, loot, Alchemist|
|Upgrade / grade rules and trait rolls|[08_Blacksmith_and_Enchanter.md](08_Blacksmith_and_Enchanter.md)|Equipment, Enemy drops|
|Quest and contract state|[09_Town_Quests_and_Contracts.md](09_Town_Quests_and_Contracts.md)|Loot resolver, map gates|
|Map areas and area unlocks|[10_Map_Regions_and_Progression.md](10_Map_Regions_and_Progression.md)|City Gate, encounters|
|Enemy spawn composition|[11_Encounter_Spawns.md](11_Encounter_Spawns.md)|Enemy Codex, AI|
|Enemy baseline, rewards, and exact material drops|[12_Enemy_Codex.md](12_Enemy_Codex.md)|Loot resolver, encounters|
|Enemy behavior|[13_Enemy_AI_Patterns.md](13_Enemy_AI_Patterns.md)|Combat AI|
|Boss phases|[14_Boss_Patterns.md](14_Boss_Patterns.md)|Combat AI and quest gates|

## Normalized rank names

|Display label in source data|Implementation class|Meaning|
|---|---|---|
|Normal|Normal|Standard encounter target.|
|Elite|Elite|Stronger target; may use the Elite equipment pool.|
|Story Unique / Contract Unique / Story-Contract Unique|Mini Boss|Scripted or contract-gated single target.|
|Regional Boss / Repeatable Boss|Boss|Area-final or repeatable high-tier fight.|
|Final Boss|Final Boss|Dragon King only; no ordinary reward table.|

## Reward resolution order

```text
1. Defeat enemy and resolve combat victory.
2. Grant fixed XP and fixed Gold from Enemy Codex.
3. Grant every listed guaranteed material quantity.
4. Resolve every linked supplemental crafting-material roll.
5. Resolve the named equipment-pool roll.
6. Resolve the linked Quest Item only if its exact objective is active and incomplete.
7. Save after all rewards and quest state changes are fully resolved.
```

The exact values and active-only drops are in [12_Enemy_Codex.md](12_Enemy_Codex.md).

## Balance 2.0 system overrides

- Crafting inputs now have a direct Monster Loot source and exact chance in [Crafting Loot, Recipes, and Potion Effects](03_Status_Effects_and_Consumables.md).
- Only Small Health Potion and Small Mana Potion are normally sold; every stronger consumable has a craft recipe and may additionally appear as a quest/chest reward. See [Market and Alchemy 2.0](07_Economy_Market_and_Alchemy.md).
- The final Dragon King challenge is balanced for Level 95–100; see [Progression, XP, and Level Balance](02_Attributes_and_Combat.md).
- Per-enemy AI links are in the Enemy Codex and resolve to [Individual Enemy Pattern Links](13_Enemy_AI_Patterns.md).

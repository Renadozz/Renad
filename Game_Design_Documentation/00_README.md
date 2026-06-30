# Game Design Documentation

## Canonical documentation map

This package is intentionally organized by game-system ownership. There are no separate “added” design files: additions and balance corrections are integrated into the system document that owns them.

|Document|Owns|
|---|---|
|[01 System Overview](01_System_Overview.md)|High-level rules, architecture, and navigation.|
|[02 Attributes and Combat](02_Attributes_and_Combat.md)|Shared/unique attributes, formulas, action gauge, damage, healing, XP curve, and balance checkpoints.|
|[03 Status Effects and Consumables](03_Status_Effects_and_Consumables.md)|Effects, Potion values/durations, recipes, and direct ingredient sources.|
|[04 Player and Skills](04_Player_and_Skills.md)|Every Player Active Skill, Passive, Tier unlock, Skill Point rule, and equipment/passive validity rule.|
|[05 Equipment and Drop Pools](05_Equipment_and_Drop_Pools.md)|All Equipment, Pools, Builds, Accessory rules, Grade Effects, Traits, and Grade Passives.|
|[06 Item Price Catalog](06_Item_Price_Catalog.md)|Reference values, Buy/Sell values, anti-arbitrage, and price validation.|
|[07 Economy, Market and Alchemy](07_Economy_Market_and_Alchemy.md)|Market stock, restock rules, starter gear, and crafting loop.|
|[08 Blacksmith and Enchanter](08_Blacksmith_and_Enchanter.md)|Upgrades, grades, materials, salvage/disenchant, Traits, and rerolls.|
|[09 Town, Quests and Contracts](09_Town_Quests_and_Contracts.md)|Services, complete Story Quest/Contract catalog, rewards, and campaign pace analysis.|
|[10 Map, Regions and Progression](10_Map_Regions_and_Progression.md)|World structure and locks.|
|[11 Encounter Spawns](11_Encounter_Spawns.md)|Templates, validation, weights, and spawn formula.|
|[12 Enemy Codex](12_Enemy_Codex.md)|Every enemy's stats, XP, Gold, crafting loot, Equipment roll, Quest drop, and Pattern link.|
|[13 Enemy AI Patterns](13_Enemy_AI_Patterns.md)|Every enemy Skill explanation and every Pattern, with local Skill links.|
|[14 Boss Patterns](14_Boss_Patterns.md)|Regional boss, Ancient Dragon, and Dragon King phase behavior.|
|[15 Forms and Data Schema](15_Forms_and_Data_Schema.md)|Data forms and implementation fields.|
|[16 Consistency Audit](16_Consistency_Audit.md)|Cross-system verification results.|
|[17 Change Log and Migration](17_Change_Log_and_Migration.md)|Migration history.|
|[19 Documentation Manifest](19_Documentation_Manifest.md)|File inventory and validation summary.|

## Source snapshots

`Source_*.md` files preserve the supplied source documents for traceability. They are historical snapshots; when a source conflicts with a canonical document above, the canonical document wins.

## Key current balance rules

- Only Small Health and Small Mana Potions are purchasable; all stronger recovery, medicine, buff, resistance, and Oil Items are farmed and crafted.
- Low recovery uses fixed values, not percentages; Recovery Items have a 2-own-action cooldown.
- Iron Scrap is an expensive limited emergency purchase, not unlimited cheap progression.
- The XP curve requires 1,820,650 XP from Level 1 to 100. The intended pre-Dragon-King level is 95–98.
- The Player receives 61 Skill Points at Level 100, insufficient to learn the whole library.
- Every Enemy Codex row directly links to its AI Pattern, and every Pattern's listed Skills link to their explanation.
- Accessories use one slot and never upgrade, grade, salvage, or disenchant.

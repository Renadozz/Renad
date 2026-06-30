# Change Log and Migration Notes

## Linked documents

[Consistency Audit](16_Consistency_Audit.md) · [Documentation index](00_README.md) · [Enemy Codex](12_Enemy_Codex.md)

## Preservation policy

Every supplied Markdown source has been copied in full to a `Source_*.md` file. Each copied source is longer than or equal to its original because a Documentation Links appendix was added. No original information was deleted.

## Added canonical files

|File|Purpose|
|---|---|
|00_README.md|Cross-linked entry point and source index.|
|01_System_Overview.md|Precedence, game loop, data ownership.|
|02_Attributes_and_Combat.md|Normalized action, duration, Freeze, Ward, and formula ownership.|
|03_Status_Effects_and_Consumables.md|Effect register and ingredient fixes.|
|04_Player_and_Skills.md|Player rules and missing passive integration.|
|05_Equipment_and_Drop_Pools.md|75 named weapon/armor/accessory records and explicit regional pools.|
|06_Item_Price_Catalog.md|Sell value / not-sellable status for every named item.|
|07_Economy_Market_and_Alchemy.md|Market/Alchemy implementation.|
|08_Blacksmith_and_Enchanter.md|Upgrade/grade summary and trait boundaries.|
|09_Town_Quests_and_Contracts.md|Contract and Town integration.|
|10_Map_Regions_and_Progression.md|Area route and gates.|
|11_Encounter_Spawns.md|Roster coverage and new encounter templates.|
|12_Enemy_Codex.md|119 enemies with fixed stats and rewards.|
|13_Enemy_AI_Patterns.md|Complete AI coverage and alias normalization.|
|14_Boss_Patterns.md|Eight area-final boss phase designs.|
|15_Forms_and_Data_Schema.md|UI forms and persistence schema.|
|16_Consistency_Audit.md|Detected conflicts and resolutions.|
|04_Player_and_Skills.md|Player Active/Passive Skills and their requirements.|

## Additive content

|Content|Quantity|Reason|
|---|---:|---|
|New current enemies|7|Supply missing active sources for named recipe materials and legacy references.|
|Current enemy AI patterns completed|37|Current loot entries without dedicated source AI rows.|
|Named equipment|75|Replace generic equipment categories with traceable pool entries.|
|Area-final boss patterns|8|Give each final area boss an explicit phase model.|
|New shared enemy skills|7|Support added enemy and Unique behaviors.|
|New player passive|1|Resolve the missing `Alchemist's Pouch` reference.|

## Migration order for implementation

```text
1. Import the source documents for audit/history.
2. Implement canonical Item, Enemy, Equipment, Skill, Quest, Encounter, and Form schemas.
3. Load Item Price Catalog and Equipment Pool IDs.
4. Load Enemy Codex before Encounter Templates.
5. Load Enemy AI and Boss Patterns.
6. Enforce the Quest Item resolver and autosave boundary.
7. Run the audit checks from 16_Consistency_Audit.md.
```

## Balance 2.0 migration

- Rebalanced all 119 Enemy Codex stat rows, Levels, fixed XP, and Gold to a Level 1–100 progression model.
- Added direct AI pattern and full crafting-loot links to all Codex enemy rows.
- Added direct monster sources and exact extra rolls for every crafting input, including containers and Enchantment materials.
- Restricted completed Market Potions to Small Health / Small Mana and added starter weapons/armor for all equipment paths.
- Rescaled 75 catalog equipment items and their base/sell values; added anti-arbitrage sale rule.
- Added Epic/Legendary/Mythic Grade Effects and Grade Passives for Weapons, Shields, and Armor; added special Mythic two-hand totals.
- Added Tier IV–VI Skill progression, expanded active/passive Skills, and detailed requirement rules.
- Added a 99-row XP requirement table and consolidated combat formula reference.
- Enforced one non-upgradeable Accessory slot.

## Balance 2.1 follow-up corrections

- Converted Full, Phoenix, Last Stand, Vampiric, Experience, and Gold Potions to craft-only outputs with endgame/Mythic recipes.
- Added Curse, Magic Ward, and Damage Reduction to the canonical status layer and coverage matrix.
- Reconciled the old two-passive limit with the user-required Mythic two-hand exception: two-hand Mythic Weapons hold three total Grade Passives.
- Raised Dragon King combat stats above Ancient Dragon offensive pressure and documented the target Level 95–99 fight band.



## Revision 3.0 — Canonical consolidation

- Removed standalone additive documentation files from the active navigation; their content was integrated into the owning canonical systems.
- Consolidated all Player Skills and Passives into `04_Player_and_Skills.md`.
- Consolidated formulas, action gauge, attributes, and XP progression into `02_Attributes_and_Combat.md`.
- Consolidated Potion effects, durations, recipes, early countermeasures, and ingredient sources into `03_Status_Effects_and_Consumables.md`.
- Consolidated builds, Grade Effect/Passive rules, direct Epic Trait behavior, and Accessory restrictions into `05_Equipment_and_Drop_Pools.md`.
- Consolidated market restrictions and starter stock into `07_Economy_Market_and_Alchemy.md`.
- Consolidated detailed Quest/Contract catalogue and pace analysis into `09_Town_Quests_and_Contracts.md`.
- Consolidated per-monster supplemental crafting loot into `12_Enemy_Codex.md`.
- Consolidated direct Enemy Pattern anchors and Enemy Skill explanation links into `13_Enemy_AI_Patterns.md`.

## Revision 3.0 final integrity check

- Repaired the Elemental Magic skill table and the Encounter Template final-boss row.
- Verified all Markdown tables in canonical documents and source snapshots: 0 malformed tables.
- Verified local Markdown files and anchors: 0 broken links.
- Verified 119 Enemy Codex Pattern links and 119 Codex material-profile links: all targets exist.

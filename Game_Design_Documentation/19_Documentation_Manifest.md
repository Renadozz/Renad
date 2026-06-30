# Documentation Manifest

## Active canonical files

|File|Purpose|Status|
|---|---|---|
|00_README.md|Navigation and ownership map|Canonical|
|01_System_Overview.md|System overview|Canonical|
|02_Attributes_and_Combat.md|Attributes, formulas, gauge, XP|Canonical|
|03_Status_Effects_and_Consumables.md|Effects, Potions, recipes, input sources|Canonical|
|04_Player_and_Skills.md|Complete Player Active/Passive library|Canonical|
|05_Equipment_and_Drop_Pools.md|Equipment, builds, Traits/Effects/Passives|Canonical|
|06_Item_Price_Catalog.md|Prices and sale relations|Canonical|
|07_Economy_Market_and_Alchemy.md|Market, restocks, Alchemy|Canonical|
|08_Blacksmith_and_Enchanter.md|Upgrade, grade, salvage, rerolls|Canonical|
|09_Town_Quests_and_Contracts.md|Town and complete Quest/Contract catalog|Canonical|
|10_Map_Regions_and_Progression.md|Map and progression|Canonical|
|11_Encounter_Spawns.md|Templates and spawn algorithm|Canonical|
|12_Enemy_Codex.md|Enemy stats, rewards, loot, Pattern links|Canonical|
|13_Enemy_AI_Patterns.md|Enemy Skills and AI Patterns|Canonical|
|14_Boss_Patterns.md|Boss phase plans|Canonical|
|15_Forms_and_Data_Schema.md|Forms and data schema|Canonical|
|16_Consistency_Audit.md|Validation results|Canonical|
|17_Change_Log_and_Migration.md|Migration history|Canonical|
|19_Documentation_Manifest.md|This file|Canonical|

## Source snapshots

The 11 `Source_*.md` files are preserved traceability snapshots. They are not duplicate active systems; canonical rules are owned by the files above.

## Validation statement

- Prior active additive documents `18` and `20–27` were intentionally consolidated into their owning canonical documents and removed from active navigation. `19_Documentation_Manifest.md` remains the canonical manifest.
- Local Markdown links were checked after consolidation.
- Markdown table column consistency was checked after consolidation.
- 119 Enemy Codex Pattern links resolve locally to the Enemy AI register.
- Every craft input has a listed direct Monster or explicit supplemental source.

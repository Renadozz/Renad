# Consistency Audit

## Revision 3.0 verification scope

|Check|Result|Correction / rule|
|---|---|---|
|Shared vs Player-only vs Enemy-only attributes|Pass|[Attributes and Combat](02_Attributes_and_Combat.md) now explicitly identifies ownership for every runtime and definition attribute.|
|Magic Skill table rendering|Pass|All Player Active/Passive tables are consolidated in [Player and Skills](04_Player_and_Skills.md), with valid Markdown table column counts.|
|Potion percentage exploit|Pass|Low/mid recovery now uses fixed values; Full recovery is the only all-missing-HP/MP exception. Recovery Items have a 2-own-action cooldown.|
|Temporary Potion duration|Pass|Every temporary Potion/Oil has an exact own-action or encounter duration.|
|Early status counter availability|Pass|Recipes were moved earlier so each first meaningful pressure has a farmable answer before or at that content.|
|Iron Scrap economy|Pass|Unlimited low-price purchase removed. Market stock: 3 per progress-based restock at 60 Gold.|
|Epic weapon drop Trait|Pass|Direct Epic Weapon/Shield drops roll one random compatible Epic Trait immediately; Epic Armor rolls an Armor Grade Effect.|
|Legendary/Mythic effect and passive counts|Pass|Epic 1 Effect; Legendary +1 Effect +1 Passive; Mythic +1 Effect +1 Passive; Mythic two-hand +2 Effects +2 Passives.|
|Accessory restriction|Pass|Exactly one Slot; cannot upgrade, grade, salvage, or disenchant.|
|Skill point sufficiency|Pass|Max 61 Points versus a library whose full purchase cost exceeds the budget.|
|Skill unlock timing|Pass|Tier I–VI global/regional Area/Boss rules and branch prerequisites are in [Player and Skills](04_Player_and_Skills.md).|
|Quest / enemy XP vs curve|Pass (analytical)|Revised Enemy XP, Quest coefficient, and 1.82M XP curve total **1,820,650 XP** at Level 100; target Level 95–98 before Dragon King.|
|Campaign duration|Analytical only|No executable client exists for a real playtest. Spreadsheet encounter/reward analysis estimates 25–35 hours to final-boss readiness.|
|Spawn formula|Pass|Eligibility filter, weighted template selection, exact composition, stat scaling, and worked example are in [Encounter Spawns](11_Encounter_Spawns.md).|
|Enemy Skill explanation and Pattern links|Pass|[Enemy AI](13_Enemy_AI_Patterns.md) contains skill explanations and local anchors; Codex rows link directly to their Pattern.|
|Ingredient source list|Pass|[Status Effects and Consumables](03_Status_Effects_and_Consumables.md) lists every crafting input, earliest source, and direct Monster source.|
|Blacksmith / Enchanter detail and rerolls|Pass|[Blacksmith and Enchanter](08_Blacksmith_and_Enchanter.md) includes full workflow, material sources, Trait/Passive reroll formulas, and non-resetting per-item counters.|
|Local Markdown table formatting|Pass|Automated table-column audit executed on all 30 Markdown files, including preserved source snapshots.|
|Local Markdown file links|Pass|Automated local file-and-anchor audit executed after consolidation: 0 broken targets.|

## Deliberate design decisions

- A full real-time playtest cannot be claimed until an executable prototype and telemetry exist. The included completion estimate is clearly analytical.
- Source snapshot conflicts are retained for history but do not override canonical documents.
- Direct Epic Weapon/Shield drops follow the random compatible Epic Trait rule; Legendary and Mythic do not drop.

## Final automated integrity result

|Audit|Result|
|---|---|
|Markdown table column counts|0 malformed tables across all 30 Markdown files.|
|Local file and anchor links|0 broken links.|
|Enemy Codex → AI Pattern anchors|119 links; 119 unique target anchors; 0 missing.|
|Enemy Codex → Material profile anchors|119 links; 119 unique target anchors; 0 missing.|
|References to removed additive files|0 references.|

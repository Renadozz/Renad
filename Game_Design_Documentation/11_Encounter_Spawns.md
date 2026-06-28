# Encounter Spawn System

## Linked documents

[Map and regions](10_Map_Regions_and_Progression.md) · [Enemy Codex](12_Enemy_Codex.md) · [Enemy AI](13_Enemy_AI_Patterns.md) · [Boss patterns](14_Boss_Patterns.md)

## Core rules

|Rule|Canonical implementation|
|---|---|
|Prepared templates|An encounter selects one balanced template; do not independently roll each monster.|
|Maximum living enemies|3, including summons.|
|Elite limit|At most one Elite in a normal/elite encounter.|
|Unique/Boss|Scripted: Story Uniques, Contract Uniques, bosses, and final boss use exact templates.|
|Final boss|Dragon King always spawns alone.|
|Quest eligibility|A template with a Story Unique/Contract Unique only exists while its linked quest/contract is valid.|
|Repeatability|Regional Boss Challenges and Ancient Dragon may respawn only through their post-story Contract state.|
|Scaling|Apply area stage and any specified template modifier after selecting the exact composition.|

## Area roster coverage

Every canonical enemy is registered in an area roster. The names in `Normal`, `Elite`, `Unique`, and `Boss` are valid candidates for an appropriately typed template.

|Area|Stage|Normal roster|Elite roster|Story / Contract Unique roster|Boss roster|
|---|---|---|---|---|---|
|Forest Entrance|Stage 1|Forest Rat; Wild Boar|—|Barkhide Boar|—|
|Desert Border|Stage 1|Desert Rat; Sand Beetle|—|Dustrunner Scarab|—|
|Mountain Foothills|Stage 1|Snow Wolf; Ice Bat|—|Whitefang Alpha|—|
|Ashen Border|Stage 1|Ash Lizard; Ember Hound|—|—|—|
|Gloomwood|Stage 1|Shade; Bone Hound|—|Lantern Shade|—|
|Sunlit Road|Stage 1|Sun Acolyte; Temple Squire|—|Sunwing Hawk|—|
|Goblin Forest|Stage 2|Goblin Scout; Goblin Dagger; Goblin Archer; Goblin Bomber|Goblin Shaman|Totem-Bound Goblin; Boneknife Skulk|—|
|Scorching Dunes|Stage 2|Sand Scorpion; Vulture; Sand Wolf|—|Glasswing Vulture|—|
|Mountain Pass|Stage 2|Rock Crawler; Harpy|—|Echo Stalker|—|
|Ashen Border / Ember Fields|Stage 2|—|—|Ashfang Hound|—|
|Ember Fields|Stage 2|Lava Slime; Magma Beetle; Ash Cultist|—|Magmaheart Slime|—|
|Shadow Marsh|Stage 2|Shadow Spider; Dark Wolf|—|Bogshade Huntress|—|
|Temple Gardens|Stage 2|Radiant Hawk; Light Sprite; Sacred Treant|—|Blighted Blossom|—|
|Overgrown Trail|Stage 3|Moss Spider; Thorn Beast; Fungus|—|Thorn Matriarch; Webmother Nyss|—|
|Bandit Camp|Stage 3|Bandit Scout; Sand Raider; Bandit Archer|Bandit Alchemist|Dune Captain Kharif|—|
|Echo Mine|Stage 3|Crystal Beetle; Mine Wraith; Stone Golem|—|Quartzback Golem|—|
|Lava Fissures|Stage 3|Flame Elemental; Cinder Witch; Fire Drake|—|Embermaw Lizard|—|
|Forgotten Crypt|Stage 3|Grave Wraith; Plague Mummy; Night Hag|—|Gravebound Knight Arct|—|
|Sanctum Halls|Stage 3|Stone Guardian; Sun Priest; Inquisitor|—|Veiled Inquisitor Sorn|—|
|Deep Woods|Stage 4|—|Goblin Mage; Treant; Forest Witch|Hollowroot Treant|—|
|Ancient Ruins|Stage 4|Tomb Guardian|Sand Wraith; Desert Shaman; Mummy|Ashen Mummy Scribe|—|
|Ice Caves|Stage 4|Frost Spider; Frost Mage; Frost Wyrm|Ice Elemental|Icebound Scribe; Icefang Matriarch|—|
|Magma Forge|Stage 4|—|Molten Golem; Ember Wyrm|Forged Flame Sentinel|—|
|Void Rift|Stage 4|—|Void Golem; Shadow Drake; Dread Knight|Riftbound Echo|—|
|Dawn Basilica|Stage 4|—|Dawn Seraph; Warden|Fallen Seraph Amon|—|
|Frozen Peak|Stage 5|Mountain Beast|Avalanche Elemental; Peak Guardian|Stormclaw Harpy|—|
|King's Clearing|Stage 6|—|—|—|Goblin King|
|Ruin Guardian Chamber|Stage 6|—|—|—|Ruin Guardian|
|Summit Shrine|Stage 6|—|—|—|Frost Titan|
|Inferno Core|Stage 6|—|—|—|Inferno Lord|
|Dread Throne|Stage 6|—|—|—|Shadow Lord|
|Oracle Chamber|Stage 6|—|—|—|Oracle|
|Dragon Valley|Stage 7|Dragon Servant; Dragon Whelp|—|Redscale Whelp|—|
|Dragon Cave|Stage 8|Wyvern; Dragon Archer|—|Bonewing Remnant|—|
|Dragon Cave / Ancient Nest|Stage 8|—|Bone Dragon|—|—|
|Obsidian Citadel|Stage 9|Dragon Knight; Dragon Priest; Dragon Warlock|Obsidian Guardian|Obsidian Warden Korr|—|
|Ancient Nest|Stage 10|—|Dragon Knight Captain|—|Ancient Dragon|
|Dragon King's Lair|Stage 11|—|—|—|Dragon King|

## Template patterns

|Template class|Exact composition rule|Examples|
|---|---|---|
|Solo normal|One Normal enemy.|Forest Rat; Frost Wyrm.|
|Normal synergy|Two or three Normal enemies with complementary roles.|Tank + caster; controller + archer.|
|Elite support|One Elite plus one or two Normal enemies.|Goblin Shaman + Goblin Dagger; Peak Guardian + Harpy.|
|Story/Contract Unique|The named Unique alone unless its linked quest defines scripted adds.|Totem-Bound Goblin; Barkhide Boar.|
|Regional boss|Boss alone unless its boss pattern specifically summons permitted minions.|Goblin King; Inferno Lord.|
|Final boss|Dragon King alone; no summons.|Dragon King.|

## Added enemy encounter templates

|Area|Template name|Type|Exact enemies|Combat theme|
|---|---|---|---|---|
|Goblin Forest|Explosive Patrol|Normal|Goblin Bomber + Goblin Scout|Evasion pressure plus Fire setup.|
|Scorching Dunes|Dune Pack|Normal|Sand Wolf + Vulture|Bleeding pressure plus Blind.|
|Deep Woods|Coven of Roots|Elite|Forest Witch + Treant|Poison/Curse with a defensive frontline.|
|Ice Caves|Frozen Crosswind|Normal|Frost Wyrm + Frost Spider|Freeze/Winded plus Rooted/Poison.|
|Ancient Ruins|Buried Ward|Normal|Tomb Guardian + Mummy|Defense plus Curse/Poison.|
|Frozen Peak|Stormfall Element|Elite|Avalanche Elemental + Mountain Beast|Slow/Freeze plus heavy Physical pressure.|
|Frozen Peak|Shrine Sentinel|Elite|Peak Guardian + Harpy|Fortify/Barrier plus Air disruption.|

## Validation checklist

```text
- every referenced enemy exists in Enemy Codex
- every conditionally spawned Unique has exact quest/contract state
- encounter contains no more than 3 living enemies
- only one Elite, Mini Boss, or Boss appears unless explicitly scripted
- each group has a useful solo AI fallback
- Monster material, Gold, XP, equipment pool, and Quest Item state resolve from Enemy Codex
```

The fuller original encounter data model and selection algorithm remain in [Source_Encounter_Spawn_System.md](Source_Encounter_Spawn_System.md).


## Detailed weighted selection algorithm

Encounter selection never rolls individual Enemies independently. It selects one complete, prepared Encounter Template and then spawns the exact listed composition.

```text
1. Load all templates for CurrentArea.
2. Remove a template if its Area, progression, quest, one-time, boss, rank-limit,
   enemy-limit, rare-spawn-cooldown, or minimum-level validation fails.
3. If an active scripted Quest/Boss template exists, select it immediately; it has no weight roll.
4. For non-scripted templates, calculate TotalWeight = Sum(Weight of every valid template).
5. Roll Integer R uniformly from 1 through TotalWeight inclusive.
6. Iterate valid templates in stable template-ID order, accumulating their weights.
7. Select the first template where R <= cumulative weight.
8. Spawn the template's exact Enemy Slots. Do not add another random Enemy.
9. Apply AreaStatMultiplier and any documented crossover modifier to the spawned base stats.
10. Start combat with no more than three living Enemies.
```

```text
Spawn Chance(template) = Template Weight / Sum(Weight of all currently valid templates)
```

Weights are relative and do not need to sum to 100.

### Worked spawn example

|Valid template|Weight|Cumulative interval|Chance|
|---|---:|---|---:|
|Forest Rat Pack|25|1–25|25%|
|Boar Hunt|20|26–45|20%|
|Forest Ambush|35|46–80|35%|
|Goblin Scout Patrol|20|81–100|20%|

If `R = 62`, the selected template is `Forest Ambush`. If `Goblin Scout Patrol` is locked by its progression condition, remove its 20 Weight first; the remaining total becomes 80 and the three remaining templates have 31.25%, 25%, and 43.75% chances.

### Validation and scaling

|Validation / modifier|Exact rule|
|---|---|
|Maximum enemies|A template may contain at most 3 living Enemies. Summons count toward this cap.|
|Rank limit|A normal/elite template contains at most 1 Elite; any template contains at most 1 Mini Boss or Boss.|
|Scripted Boss|A Story Boss, Contract Unique, or Quest encounter bypasses weighted selection and uses its fixed template.|
|Repeatable Boss|Eligible only after its Story Boss state is complete and the matching Boss Challenge Contract is active.|
|Area scaling|`Spawned Stat = Floor(Enemy Base Stat × AreaStatMultiplier × CrossoverModifier)` for HP, PAtk, MPow, Def, and MDef. Speed, Accuracy, Evasion, Crit, and Resistance only change when a template explicitly lists a modifier.|
|Crossover modifier|Use only when a template explicitly permits an enemy from another area; default 1.00. A documented template value, e.g. 1.10, is applied once.|
|Rare / Unique cooldown|The template is invalid until its documented cooldown, contract state, or one-time state permits it.|

The following fixed source constraints remain canonical: Dragon King always spawns alone; a Boss can have scripted adds only if its Boss Pattern explicitly creates them; and all Enemy composition must be authored in a template rather than random individual rolls.

# Encounter Spawn System

## Purpose

This system decides which enemies spawn when the Player enters an area or triggers a battle.

The game does not randomly select individual enemies one by one.

Instead, the game selects one prepared `Encounter Template` for the current area. Each template contains an exact enemy combination, its difficulty, its spawn weight, and optional conditions.

This ensures that every encounter is balanced, thematic, and compatible with the enemies' Group AI Priority.

---

# Data Ownership

## Enemy Data

Enemy Data defines what one enemy is.

| Enemy Data Contains | Description                                                                               |
| ------------------- | ----------------------------------------------------------------------------------------- |
| Enemy Name          | Display name of the enemy.                                                                |
| Rank                | Normal,Elite,Mini Boss,Boss,or Final Boss.                                                |
| Combat Role         | Bruiser,Tank,Support,Mage,Archer,Controller,Assassin,or Boss.                             |
| Origin Region       | Region where the enemy is first introduced.                                               |
| Element Types       | One or more elements used by the enemy.                                                   |
| Combat Attributes   | Health,Physical Attack,Magic Power,Defense,Magical Defense,Speed,and other combat values. |
| Skill List          | Skills the enemy can use.                                                                 |
| Group AI Priority   | AI rules used while at least one friendly enemy is alive.                                 |
| Solo AI Priority    | AI rules used while the enemy is alone.                                                   |
| Rewards             | Experience Reward,Gold Reward,Guaranteed Drops,Possible Drops,and Rare Drop Table.        |
| Boss Flags          | Special rules for Bosses or special enemies only.                                         |

> Enemy Data does not decide where an enemy spawns, how often it spawns, or which enemies it appears with.

---

## Area Data

Area Data defines the place where encounters occur.

| Area Data Contains     | Description                                                              |
| ---------------------- | ------------------------------------------------------------------------ |
| Region                 | The larger elemental region containing the area.                         |
| Area Name              | The specific location where encounters can occur.                        |
| Area Depth             | Outer Area,Middle Area,Deep Area,or Boss Area.                           |
| Recommended Difficulty | General difficulty range for the area.                                   |
| Encounter Pool         | List of Encounter Templates available in this area.                      |
| Progress Condition     | Story,quest,key,or Sigil condition required to enter the area.           |
| Area Stat Scaling      | Optional modifier applied to all enemies spawned in this area.           |
| Special Area Rules     | Optional rules such as Cannot Escape,No Random Encounters,or Boss Arena. |

---

## Encounter Template Data

Encounter Template Data defines one exact encounter.

| Encounter Template Contains | Description                                                                 |
| --------------------------- | --------------------------------------------------------------------------- |
| Encounter Name              | Internal name for this encounter combination.                               |
| Area                        | Area where the encounter can spawn.                                         |
| Encounter Type              | Normal,Elite,Mini Boss,Boss,or Scripted.                                    |
| Enemy Slots                 | Exact enemies that spawn.                                                   |
| Total Enemy Count           | Number of enemies in the encounter. Maximum 3.                              |
| Weight                      | Relative chance of this template being selected.                            |
| Difficulty Rating           | Easy,Normal,Hard,Very Hard,or Boss.                                         |
| Combat Theme                | Purpose of the combination,for example Control + Damage.                    |
| Progress Condition          | Optional condition required before this encounter becomes valid.            |
| Respawn Rule                | Normal Respawn,Rare Spawn,Boss Respawn,One-Time Encounter,or Scripted Only. |
| Crossover Rule              | Optional rule for enemies reused from an earlier region.                    |
| Special Rules               | Optional encounter-specific rules.                                          |

> Encounter Templates decide exactly which enemies spawn together.
> They replace individual random enemy rolls.

---

# Core Spawn Rules

| Rule                       | Implementation                                                                                          |
| -------------------------- | ------------------------------------------------------------------------------------------------------- |
| Maximum Enemies            | An encounter can contain a maximum of 3 living enemies.                                                 |
| Prepared Groups            | Every encounter uses one prepared Encounter Template.                                                   |
| No Independent Enemy Rolls | Do not first roll one enemy and then roll additional random enemies.                                    |
| Exact Composition          | When a template is selected,the enemies listed in its Enemy Slots spawn exactly as written.             |
| Duplicate Enemies          | The same enemy can only appear multiple times when the template explicitly lists it multiple times.     |
| Normal Encounter           | Contains 1-3 Normal enemies.                                                                            |
| Elite Encounter            | Contains 1 Elite enemy alone,or 1 Elite enemy with 1-2 Normal enemies.                                  |
| Mini Boss Encounter        | Contains 1 Mini Boss alone,or 1 Mini Boss with 1 Normal enemy.                                          |
| Boss Encounter             | Contains 1 Boss alone,or 1 Boss with up to 2 scripted adds.                                             |
| Final Boss Encounter       | Dragon King always spawns alone.                                                                        |
| Elite Limit                | A Normal or Elite Encounter can contain a maximum of 1 Elite enemy.                                     |
| Mini Boss Limit            | An encounter can contain a maximum of 1 Mini Boss.                                                      |
| Boss Limit                 | An encounter can contain a maximum of 1 Boss.                                                           |
| Scripted Encounter         | Quest fights,Mini Bosses,and Bosses use fixed Encounter Templates instead of normal weighted selection. |
| Summoned Enemies           | Summoned enemies count toward the global maximum of 3 living enemies.                                   |

---

# Encounter Selection Flow

```text
1. Player enters an area or triggers an encounter.
2. Load every Encounter Template assigned to the current area.
3. Remove every invalid Encounter Template.
4. Check whether a Scripted Encounter is active.
5. If a Scripted Encounter is active,select it immediately.
6. If no Scripted Encounter is active,select one valid template by Weight.
7. Spawn exactly the enemies listed in the selected template.
8. Apply the area's stat scaling.
9. Apply a Crossover Modifier if the template contains crossover enemies.
10. Start combat.
```

---

# Encounter Validation Rules

Before an Encounter Template can be selected, it must be valid.

| Validation Rule     | Template Is Invalid When                                                                                 |
| ------------------- | -------------------------------------------------------------------------------------------------------- |
| Area Check          | The template does not belong to the current area.                                                        |
| Progress Check      | The Player has not met the required quest,story,key,or Sigil condition.                                  |
| One-Time Check      | The template is marked One-Time Encounter and was already completed.                                     |
| Boss Check          | The template contains a defeated non-repeatable Boss.                                                    |
| Quest Check         | The template requires an active quest that is not active.                                                |
| Enemy Limit Check   | The template contains more than 3 enemies.                                                               |
| Rank Limit Check    | The template contains more than 1 Elite,Mini Boss,or Boss.                                               |
| Repeat Check        | The template is prevented by a special cooldown or rare-spawn rule.                                      |
| Minimum Level Check | The optional Minimum Player Level is not reached. Use sparingly because progression is not fully linear. |

---

# Encounter Weight System

## Weight Formula

```text
Spawn Chance = Template Weight / Sum of All Valid Template Weights
```

Weights do not need to add up to `100`.

They only define the relative chance of each valid Encounter Template.

## Example

| Encounter Template  | Weight | Calculation | Spawn Chance |
| ------------------- | -----: | ----------- | -----------: |
| Forest Rat Pack     |     25 | 25 / 100    |          25% |
| Boar Hunt           |     20 | 20 / 100    |          20% |
| Forest Ambush       |     35 | 35 / 100    |          35% |
| Goblin Scout Patrol |     20 | 20 / 100    |          20% |

## Weight Guidelines

| Encounter Type            | Suggested Weight Range | Purpose                                         |
| ------------------------- | ---------------------: | ----------------------------------------------- |
| Easy Normal Encounter     |                  25-40 | Recovery,farming,and low-pressure combat.       |
| Standard Normal Encounter |                  20-35 | Main area encounter type.                       |
| Hard Normal Encounter     |                  10-25 | More difficult but still common combat.         |
| Elite Encounter           |                   5-15 | Rare stronger encounter with better rewards.    |
| Mini Boss Encounter       |                   5-10 | Rare challenge or quest-related combat.         |
| Boss Encounter            |     100 in a Boss Area | Fixed Boss battle.                              |
| Scripted Encounter        |              No Weight | Selected directly when its condition is active. |

> Lower the Weight of encounters that use repeated Stun,heavy healing,or very high burst damage.

---

# Area Depth Rules

| Area Depth  | Purpose                                                                | Recommended Encounter Types                       |
| ----------- | ---------------------------------------------------------------------- | ------------------------------------------------- |
| Outer Area  | Introduces the region's basic enemies and mechanics.                   | Single Normal,2 Normal Enemies,rare Elite.        |
| Middle Area | Combines regional mechanics and introduces stronger enemy roles.       | 2-3 Normal Enemies,Elite + Normal,rare Mini Boss. |
| Deep Area   | Tests Player builds through stronger combinations and advanced AI.     | Hard Normal,Elite + Normal,Mini Boss.             |
| Boss Area   | Prepares the Player for the regional Boss and contains the Boss Arena. | Pre-Boss Elite,Mini Boss,Boss.                    |
| Final Area  | Contains endgame encounters and the Final Boss.                        | Elite,Mini Boss,Ancient Dragon,Dragon King.       |

## Suggested Encounter Distribution

| Area Depth  | Single Normal | 2 Normal Enemies | 3 Normal Enemies | Elite Alone | Elite + Normal | Mini Boss | Boss |
| ----------- | ------------: | ---------------: | ---------------: | ----------: | -------------: | --------: | ---: |
| Outer Area  |           25% |              45% |              15% |         10% |             5% |        0% |   0% |
| Middle Area |           10% |              35% |              25% |         10% |            15% |        5% |   0% |
| Deep Area   |            5% |              20% |              25% |         15% |            25% |       10% |   0% |
| Boss Area   |            0% |               0% |               0% |          0% |             0% |        0% | 100% |

> This is a balancing guide only. Final chances are determined by the Encounter Template Weights.

---

# How to Choose Enemies for an Area

## Step 1: Define the Area Theme

| Area Theme      | Recommended Enemy Types                                                  |
| --------------- | ------------------------------------------------------------------------ |
| Early Forest    | Small animals,simple melee enemies,low-pressure scouts.                  |
| Goblin Forest   | Fast Physical enemies,Bleeding,Blind,and simple support.                 |
| Overgrown Trail | Poison,Rooted,defensive plants,and control enemies.                      |
| Deep Woods      | Magic,sustain,stronger control,and Elite enemies.                        |
| Desert Border   | Fast animals,Air damage,Blind,and simple bruisers.                       |
| Ice Caves       | Wet,Freeze,Rooted,and Water control.                                     |
| Ember Fields    | Burn,Scorched,Fire damage,and aggressive enemies.                        |
| Shadow Marsh    | Poison,Fear,Curse,and Darkness control.                                  |
| Sanctum Halls   | Holy damage,healing,Barrier,and defensive enemies.                       |
| Dragon Valley   | Mixed Elements,high damage,strong buffs,and advanced enemy combinations. |

## Step 2: Choose Different Combat Roles

| Combat Role     | Purpose                                                      | Forest Example             |
| --------------- | ------------------------------------------------------------ | -------------------------- |
| Fast Attacker   | Acts early and applies light pressure.                       | Forest Rat,Goblin Scout    |
| Bruiser         | Deals stronger Physical Damage.                              | Wild Boar,Goblin Dagger    |
| Ranged Attacker | Uses Blind,Slow,Piercing Damage,or consistent ranged damage. | Goblin Archer              |
| Controller      | Applies Rooted,Poison,Stun,Fear,or Silence.                  | Moss Spider                |
| Tank            | Absorbs damage and protects allies indirectly.               | Thorn Beast,Ancient Treant |
| Support         | Heals,buffs,cleanses,or creates Barriers.                    | Goblin Shaman,Fungus Beast |
| Mage            | Deals Magic Damage or applies magical debuffs.               | Goblin Mage                |
| Boss            | Uses advanced AI,phases,summons,or high-impact skills.       | Goblin King                |

## Step 3: Build Functional Enemy Combinations

| Combination                                   | Combat Theme                | Why It Works                                                                                    |
| --------------------------------------------- | --------------------------- | ----------------------------------------------------------------------------------------------- |
| Goblin Dagger + Goblin Archer                 | Blind + Bleeding            | Archer applies Blind before Dagger applies Bleeding.                                            |
| Moss Spider + Thorn Beast                     | Control + Tank              | Spider applies Rooted and Poison while Thorn Beast uses Stun Slam and Heavy Attack.             |
| Fungus Beast + Goblin Mage                    | Poison + Sustain + Magic    | Fungus Beast applies Poison and Regeneration while Goblin Mage applies Rooted and Earth Damage. |
| Goblin Shaman + Goblin Dagger + Goblin Archer | Support + Physical Pressure | Shaman buffs and heals while Dagger and Archer pressure the Player.                             |
| Wild Boar + Goblin Archer                     | Blind + Bruiser             | Archer reduces Accuracy and Boar follows with Charge and Heavy Attack.                          |
| Frost Spider + Frost Mage                     | Rooted + Wet + Freeze       | Spider controls movement while Frost Mage prepares Wet and Freeze.                              |
| Dragon Knight + Dragon Warlock                | Tank + Magic Debuff         | Knight protects the Warlock while Warlock applies Silence and Magic Break.                      |

## Avoid These Combinations

| Combination                              | Why To Avoid It                                                                                 |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Three Tanks                              | Combat becomes slow and lacks pressure.                                                         |
| Three Healers or Supports                | Combat becomes frustrating through repeated sustain.                                            |
| Three Archers                            | Too little role variety and repetitive damage pattern.                                          |
| Three Controllers                        | Can remove too much Player agency through repeated status effects.                              |
| Boss + Two Healers                       | Usually creates excessively long Boss fights.                                                   |
| Multiple Enemies With Repeated Stun      | Can create unfair turn denial.                                                                  |
| High Burst Damage + Strong Healer + Tank | Can be too punishing for a single-character Player unless it is a deliberate endgame encounter. |

---

# Cross-Region Enemy Rules

## Crossover Spawn Rules

| Rule               | Implementation                                                                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| Origin Region      | Every enemy has one Origin Region where it is first introduced.                                                               |
| Native Spawn       | The enemy appears normally in its Origin Region through Encounter Templates.                                                  |
| Crossover Spawn    | An enemy may appear in a later region only through a dedicated Encounter Template.                                            |
| Crossover Purpose  | Used for easier fights,farming earlier materials,story encounters,or familiar enemy combinations.                             |
| Crossover Weight   | Crossover Templates should usually make up no more than `10-25%` of an area's total encounter weight.                         |
| Crossover Strength | A crossover enemy uses the current area's scaling but should have `10-20%` lower base stats than native enemies in that area. |
| No Early Crossover | An enemy should not spawn in an earlier region than its Origin Region except during a story event.                            |
| Boss Crossover     | Bosses do not appear as crossover enemies unless they are repeatable challenge fights.                                        |

## Crossover Example

| Area               | Encounter Template            | Crossover Enemy | Purpose                                                                |
| ------------------ | ----------------------------- | --------------- | ---------------------------------------------------------------------- |
| Mountain Foothills | Vulture + Snow Wolf           | Vulture         | Adds an earlier Air attacker to a Water-region encounter.              |
| Dragon Cave        | Dragon Priest + Shadow Spider | Shadow Spider   | Adds lower-threat control beside a stronger Dragon support unit.       |
| Obsidian Citadel   | Dragon Knight + Goblin Archer | Goblin Archer   | Optional low-threat ranged support in a late-game crossover encounter. |

---

# Encounter Template Format

## Standard Template


### Encounter Template

|Attribute|Value|
|---|---|
|Encounter Name|Forest Ambush|
|Region|Forest|
|Area|Forest Entrance|
|Encounter Type|Normal|
|Enemy Slots|Forest Rat + Wild Boar|
|Total Enemy Count|2|
|Weight|35|
|Difficulty Rating|Normal|
|Combat Theme|Fast Attacker + Bruiser|
|Progress Condition|None|
|Respawn Rule|Normal Respawn|
|Crossover Rule|None|
|Special Rules|None|


## Elite Template


### Encounter Template

|Attribute|Value|
|---|---|
|Encounter Name|Goblin Shaman Escort|
|Region|Forest|
|Area|Goblin Forest|
|Encounter Type|Elite|
|Enemy Slots|Goblin Shaman + Goblin Dagger|
|Total Enemy Count|2|
|Weight|15|
|Difficulty Rating|Hard|
|Combat Theme|Support + Physical Pressure|
|Progress Condition|Complete Forest Entrance|
|Respawn Rule|Rare Spawn|
|Crossover Rule|None|
|Special Rules|Elite rewards enabled|


## Boss Template


### Encounter Template

|Attribute|Value|
|---|---|
|Encounter Name|Goblin King Boss Fight|
|Region|Forest|
|Area|King's Clearing|
|Encounter Type|Boss|
|Enemy Slots|Goblin King|
|Total Enemy Count|1|
|Weight|No Weight|
|Difficulty Rating|Boss|
|Combat Theme|Commander Boss with Summons|
|Progress Condition|Reach King's Clearing|
|Respawn Rule|Boss Respawn|
|Crossover Rule|None|
|Special Rules|Cannot Escape;Goblin King can summon Goblin Dagger and Goblin Archer|


---

# Forest Region Encounter Pools

## Forest Entrance

| Encounter Name      | Encounter Type | Enemy Slots               | Total Enemy Count | Weight | Difficulty Rating | Combat Theme            | Respawn Rule   | Special Rules                          |
| ------------------- | -------------- | ------------------------- | ----------------: | -----: | ----------------- | ----------------------- | -------------- | -------------------------------------- |
| Forest Rat Pack     | Normal         | Forest Rat + Forest Rat   |                 2 |     25 | Easy              | Fast low-damage enemies | Normal Respawn | None                                   |
| Boar Hunt           | Normal         | Wild Boar                 |                 1 |     20 | Easy              | Single Bruiser          | Normal Respawn | None                                   |
| Forest Ambush       | Normal         | Forest Rat + Wild Boar    |                 2 |     35 | Normal            | Fast Attacker + Bruiser | Normal Respawn | None                                   |
| Goblin Scout Patrol | Normal         | Goblin Scout + Forest Rat |                 2 |     20 | Normal            | Fast Physical Pressure  | Normal Respawn | Unlock after first Goblin Forest visit |

## Goblin Forest

| Encounter Name       | Encounter Type | Enemy Slots                                  | Total Enemy Count | Weight | Difficulty Rating | Combat Theme                   | Respawn Rule   | Special Rules |
| -------------------- | -------------- | -------------------------------------------- | ----------------: | -----: | ----------------- | ------------------------------ | -------------- | ------------- |
| Goblin Patrol        | Normal         | Goblin Scout + Goblin Dagger                 |                 2 |     30 | Normal            | Fast Damage + Bleeding         | Normal Respawn | None          |
| Archer Ambush        | Normal         | Goblin Dagger + Goblin Archer                |                 2 |     25 | Normal            | Blind + Bleeding               | Normal Respawn | None          |
| Goblin Skirmish      | Normal         | Goblin Scout + Goblin Dagger + Goblin Archer |                 3 |     15 | Hard              | Fast Damage + Blind + Bleeding | Normal Respawn | None          |
| Goblin Guard Detail  | Elite          | Thorn Beast + Goblin Archer                  |                 2 |     15 | Hard              | Tank + Ranged Damage           | Rare Spawn     | None          |
| Goblin Shaman Escort | Elite          | Goblin Shaman + Goblin Dagger                |                 2 |     15 | Hard              | Support + Physical Pressure    | Rare Spawn     | None          |

## Overgrown Trail

| Encounter Name | Encounter Type | Enemy Slots                 | Total Enemy Count | Weight | Difficulty Rating | Combat Theme     | Respawn Rule   | Special Rules |
| -------------- | -------------- | --------------------------- | ----------------: | -----: | ----------------- | ---------------- | -------------- | ------------- |
| Spider Nest    | Normal         | Moss Spider + Moss Spider   |                 2 |     25 | Normal            | Rooted + Poison  | Normal Respawn | None          |
| Thorn Ambush   | Normal         | Moss Spider + Thorn Beast   |                 2 |     35 | Hard              | Control + Tank   | Normal Respawn | None          |
| Fungal Growth  | Elite          | Fungus Beast + Moss Spider  |                 2 |     20 | Hard              | Poison + Sustain | Rare Spawn     | None          |
| Goblin Trap    | Normal         | Goblin Archer + Moss Spider |                 2 |     20 | Hard              | Blind + Rooted   | Rare Spawn     | None          |

## Deep Woods

| Encounter Name     | Encounter Type | Enemy Slots                   | Total Enemy Count | Weight | Difficulty Rating | Combat Theme                  | Respawn Rule   | Crossover Rule              |
| ------------------ | -------------- | ----------------------------- | ----------------: | -----: | ----------------- | ----------------------------- | -------------- | --------------------------- |
| Cursed Growth      | Elite          | Fungus Beast + Goblin Mage    |                 2 |     30 | Hard              | Poison + Rooted + Earth Magic | Normal Respawn | None                        |
| Dark Hunt          | Elite          | Dark Wolf + Goblin Mage       |                 2 |     25 | Hard              | Fear + Earth Magic            | Normal Respawn | Later Forest enemy          |
| Ancient Guardian   | Mini Boss      | Ancient Treant                |                 1 |     15 | Very Hard         | Tank + Rooted + Sustain       | Rare Spawn     | None                        |
| Treant Protector   | Mini Boss      | Ancient Treant + Fungus Beast |                 2 |     10 | Very Hard         | Tank + Healing + Poison       | Rare Spawn     | None                        |
| Lost Goblin Patrol | Normal         | Goblin Dagger + Goblin Archer |                 2 |     20 | Normal            | Earlier Goblin Combination    | Normal Respawn | Earlier Forest area enemies |

## King's Clearing

| Encounter Name         | Encounter Type | Enemy Slots                                   | Total Enemy Count |    Weight | Difficulty Rating | Combat Theme                | Respawn Rule   | Special Rules      |
| ---------------------- | -------------- | --------------------------------------------- | ----------------: | --------: | ----------------- | --------------------------- | -------------- | ------------------ |
| Royal Guard            | Elite          | Goblin Shaman + Goblin Dagger + Goblin Archer |                 3 |        50 | Very Hard         | Support + Bleeding + Blind  | Normal Respawn | Pre-Boss encounter |
| Thorn Guard            | Elite          | Thorn Beast + Goblin Archer                   |                 2 |        20 | Hard              | Tank + Ranged Damage        | Rare Spawn     | Pre-Boss encounter |
| Ancient Protector      | Mini Boss      | Ancient Treant + Goblin Shaman                |                 2 |        30 | Very Hard         | Tank + Sustain + Support    | Rare Spawn     | Pre-Boss encounter |
| Goblin King Boss Fight | Boss           | Goblin King                                   |                 1 | No Weight | Boss              | Commander Boss with Summons | Boss Respawn   | Cannot Escape      |

---

# Area Creation Checklist

```text
1. Choose the Region and the Area Theme.
2. Decide the Area Depth.
3. Select 3-6 enemies that fit the Area Theme.
4. Ensure the selected enemies cover different Combat Roles.
5. Create 3-7 Encounter Templates.
6. Give every template a clear Combat Theme.
7. Confirm that every template contains no more than 3 enemies.
8. Confirm that each enemy has valid Group AI Priority and Solo AI Priority.
9. Assign Weights based on intended difficulty and frequency.
10. Add rare Elite or Mini Boss templates after normal encounters are balanced.
11. Add Progress Conditions only when they are needed for story or area pacing.
12. Test every template against the Player's expected equipment and potion access.
```

---

# Quick Reference

| Question                                       | Answer                                                                           |
| ---------------------------------------------- | -------------------------------------------------------------------------------- |
| Which enemies can spawn in an area?            | Only enemies included in that area's Encounter Templates.                        |
| How is one enemy selected?                     | It is not selected individually. The game selects a complete Encounter Template. |
| How is the Encounter Template selected?        | A weighted random roll selects one valid template.                               |
| Can two identical enemies spawn?               | Yes,but only when the selected template explicitly lists both.                   |
| Can an Elite spawn with a Boss?                | Only when the Boss Template explicitly uses scripted adds.                       |
| Can enemies from earlier regions return later? | Yes,through dedicated Crossover Templates.                                       |
| Where are spawn weights stored?                | On Encounter Templates,not on individual enemies.                                |
| Where are enemy combinations stored?           | On Encounter Templates,not on individual enemies.                                |
| Where are boss summons stored?                 | In the Boss AI Priority and Skill List.                                          |
| Where are boss phases stored?                  | Directly in AI Priority with conditions such as `HP <= 35%`.                     |

---

## Documentation Links

This preserved source is retained in full. The canonical integrated design is in
[11_Encounter_Spawns.md](11_Encounter_Spawns.md); the documentation index is [00_README.md](00_README.md).
Where this source conflicts with newer documents, see
[16_Consistency_Audit.md](16_Consistency_Audit.md) rather than deleting this record.

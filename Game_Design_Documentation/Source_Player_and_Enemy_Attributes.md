# Player and Enemy Attributes

## Attribute Categories

|Category|Description|
|---|---|
|Shared Combat Attributes|Combat values used by both the Player and Enemies.|
|Conditional Modifiers|Rare or temporary combat modifiers. Only display them when their value is not the default.|
|Player-Only Attributes|Resources, progression, inventory, equipment, and utility values only used by the Player.|
|Equipment Attributes|Values stored on individual equipment items.|
|Enemy-Only Attributes|Identity, AI, combat rewards, and special boss data used only by Enemies.|
|Encounter Template Attributes|Spawn data, exact enemy combinations, area availability, and encounter weights.|

---

# Shared Combat Attributes

## Core Attributes

|Attribute|Player|Enemy|Description|
|---|---|---|---|
|Level|Yes|Yes|Determines stat scaling, skill availability, and difficulty.|
|Health|Yes|Yes|Current HP. A unit is defeated when Health reaches 0.|
|Max Health|Yes|Yes|Maximum HP before temporary buffs or debuffs.|
|Physical Attack|Yes|Yes|Used for Physical attacks and Physical skills.|
|Magic Power|Yes|Yes|Used for Magic attacks and Magic skills.|
|Defense|Yes|Yes|Reduces incoming Physical Damage.|
|Magical Defense|Yes|Yes|Reduces incoming Magic Damage.|
|Speed|Yes|Yes|Determines turn order.|
|Accuracy|Yes|Yes|Used for Physical hit checks against Evasion.|
|Evasion|Yes|Yes|Chance to avoid Physical attacks. Magic attacks ignore Evasion.|
|Critical Chance|Yes|Yes|Chance for an attack to deal Critical Damage.|
|Status Resistance|Yes|Yes|Reduces the final chance of receiving negative status effects.|
|Fire Resistance|Yes|Yes|Reduces incoming Fire Damage.|
|Water Resistance|Yes|Yes|Reduces incoming Water Damage.|
|Earth Resistance|Yes|Yes|Reduces incoming Earth Damage.|
|Air Resistance|Yes|Yes|Reduces incoming Air Damage.|
|Darkness Resistance|Yes|Yes|Reduces incoming Darkness Damage.|
|Holy Resistance|Yes|Yes|Reduces incoming Holy Damage.|

## Conditional Modifiers

> These values exist internally but should only be shown in the status screen when their value differs from the default.

|Attribute|Default Value|Description|
|---|---:|---|
|Critical Damage|150%|Damage multiplier applied on a Critical Hit.|
|Healing Received|100%|Modifies healing from Potions, Heal, Regeneration, Lifesteal, and similar effects.|
|Damage Reduction|0%|Reduces all incoming damage after Defense, Magical Defense, and Elemental Resistance.|
|Barrier Strength|100%|Modifies the amount absorbed by Barriers created by skills, passives, or equipment.|
|Physical Penetration|0%|Ignores part of the target's Defense for an attack.|
|Magic Penetration|0%|Ignores part of the target's Magical Defense for an attack.|
|Fire Damage Bonus|0%|Increases outgoing Fire Damage.|
|Water Damage Bonus|0%|Increases outgoing Water Damage.|
|Earth Damage Bonus|0%|Increases outgoing Earth Damage.|
|Air Damage Bonus|0%|Increases outgoing Air Damage.|
|Darkness Damage Bonus|0%|Increases outgoing Darkness Damage.|
|Holy Damage Bonus|0%|Increases outgoing Holy Damage.|

## Shared Combat Rules

|Rule|Implementation|
|---|---|
|Physical Damage|Uses `Physical Attack` against the target's `Defense`. Physical attacks perform an Accuracy vs. Evasion check.|
|Magic Damage|Uses `Magic Power` against the target's `Magical Defense`. Magic attacks always hit.|
|Critical Hits|A successful attack checks `Critical Chance`. On success, damage is multiplied by `Critical Damage`.|
|Elemental Damage|A skill can have both a Damage Type and an Element. Example: `Fire Bolt` is Magic Damage with the Fire element.|
|Elemental Resistance|Resistance reduces matching elemental damage after Physical or Magical mitigation.|
|Status Resistance|Reduces the final chance of receiving a negative status effect.|
|Physical Penetration|Reduces the target's effective Defense for one attack.|
|Magic Penetration|Reduces the target's effective Magical Defense for one attack.|
|Healing Received|Applies to Potions, Heal, Regeneration, Lifesteal, and similar effects.|
|Barrier Strength|Only modifies Barriers created by the unit's own skills, passives, or equipment.|
|Damage Reduction|Applies after Physical or Magical mitigation and Elemental Resistance.|
|Primary Element|A skill with `Primary` element uses the first Element Type listed on the unit. A Neutral unit deals Neutral damage.|

---

# Player-Only Attributes

## Resources and Progression

|Attribute|Description|
|---|---|
|Experience|Current XP toward the next Level.|
|Experience Required|XP needed to reach the next Level.|
|Mana|Current resource used to cast Player skills.|
|Max Mana|Maximum Mana before temporary buffs or debuffs.|
|Mana Regeneration|Mana restored at the end of a turn, after battle, or through effects.|
|Skill Points|Points used to unlock or improve Player skills. Optional.|
|Attribute Points|Points used to increase selected base attributes on Level Up. Optional.|
|Known Skills|Skills unlocked through Level, quests, equipment, passives, or class progression.|
|Passive Skills|Permanent effects granted by equipment, class progression, quests, or special items.|
|Potion Uses Per Turn|Maximum number of Potions the Player may use during one turn. Default: `1`.|

## Potion Usage Rules

|Rule|Implementation|
|---|---|
|Default Limit|The Player can use `1` Potion per turn.|
|Potion Uses Per Turn|This value may be increased by a Passive Skill, Accessory, rare equipment effect, or special reward.|
|No Potion Capacity|The Player can carry every Potion stored in the Inventory. There is no separate Potion Capacity attribute.|
|No Potion Power|Potion strength is defined directly by the Potion's recipe and effect.|
|No Potion Cooldown|Potions do not use individual cooldowns.|
|No Per-Battle Potion Attribute|Do not use a separate Potion Uses Per Battle or Potion Capacity value.|
|Smoke Bomb|Uses its own battle rule and does not count as a Potion.|
|Recall Potion|Cannot be used in battle unless a special effect explicitly allows it.|
|Example Passive|`Alchemist's Pouch`: Potion Uses Per Turn `+1`.|

## Inventory and Equipment

|Attribute|Description|
|---|---|
|Gold|Currency used for shops, crafting, smithing, and enchanting.|
|Inventory|Contains Potions, crafting materials, equipment, quest items, and loot.|
|Main Hand Slot|Can equip a One-Hand Weapon, Shield, or Two-Hand Weapon.|
|Off Hand Slot|Can equip a One-Hand Weapon or Shield. Locked while a Two-Hand Weapon is equipped.|
|Armor Slot|Equipped Light Armor, Normal Armor, Heavy Armor, or Robe.|
|Helmet Slot|Equipped Helmet with defensive or utility bonuses.|
|Accessory Slot|Optional slot for Rings, Amulets, Charms, or special quest equipment.|
|Equipment Passives|Passive Skills granted by equipped items.|
|Equipment Elements|Elemental Attributes granted by equipped weapons, armor, helmets, and accessories.|

## Optional Reward Modifiers

> These are not core Player Attributes. Only add them when an item, Passive Skill, Potion, or quest reward grants them.

|Modifier|Description|
|---|---|
|Gold Find|Increases Gold received after battle.|
|Item Find|Increases the chance to receive extra materials, equipment, or rare drops.|
|Experience Gain|Increases XP received after battle.|

---

# Equipment System

## Hand Slots

|Slot|Allowed Equipment|
|---|---|
|Main Hand|One-Hand Weapon, Shield, or Two-Hand Weapon|
|Off Hand|One-Hand Weapon or Shield|
|Two-Hand Rule|A Two-Hand Weapon occupies both Hand Slots and locks the Off Hand.|

## Hand Requirement

|Hand Requirement|Description|Examples|
|---|---|---|
|One-Hand|Uses one Hand Slot. Can be equipped with another One-Hand Weapon or a Shield.|Sword,Dagger,One-Hand Axe,One-Hand Hammer,Shield|
|Two-Hand|Uses both Hand Slots. Cannot be combined with another Weapon or Shield.|Great Sword,Bow,most Staves,Two-Hand Axe,Two-Hand Hammer|

> Hand Requirement belongs to the individual item. An Axe or Hammer can exist in both One-Hand and Two-Hand versions.

## Valid Equipment Combinations

|Main Hand|Off Hand|Valid|Notes|
|---|---|---|---|
|Sword|Shield|Yes|Balanced physical build.|
|Sword|Sword|Yes|Dual-wield build.|
|Dagger|Dagger|Yes|Fast dual-wield build.|
|Axe|Shield|Yes|One-Hand Axe build.|
|Hammer|Shield|Yes|One-Hand Hammer build.|
|Shield|Shield|Yes|Very defensive build with reduced offensive power.|
|Great Sword|Locked|Yes|Two-Hand Weapon.|
|Bow|Locked|Yes|Two-Hand Weapon.|
|Staff|Locked|Yes|Two-Hand Weapon.|
|Two-Hand Axe|Locked|Yes|Two-Hand Weapon.|
|Two-Hand Hammer|Locked|Yes|Two-Hand Weapon.|
|Sword|Great Sword|No|Great Sword occupies both Hand Slots.|
|Shield|Bow|No|Bow occupies both Hand Slots.|

## Hand Stat Rules

|Loadout|Rule|
|---|---|
|Two One-Hand Weapons|Main Hand grants `100%` of its offensive values. Off Hand grants `50%` of its Physical Attack and Magic Power values. Both items grant their full passive skills, effects, and elemental attributes.|
|Weapon + Shield|Weapon grants `100%` of its offensive values. Shield grants its full Defense, Magical Defense, passive skills, effects, and elemental attributes.|
|Two Shields|Both Shields grant their full defensive values. The Player's Basic Attack becomes `Shield Bash`, which uses base Physical Attack and deals reduced damage.|
|Two-Hand Weapon|The Weapon grants `100%` of all its values and may have stronger base attributes or effects because it occupies both Hand Slots.|

## Equipment Item Attributes

|Attribute|Applies To|Description|Example|
|---|---|---|---|
|Item Name|All Equipment|Display name of the equipment item.|Iron Sword|
|Item Type|All Equipment|Weapon,Shield,Armor,Helmet,or Accessory.|Weapon|
|Weapon Type|Weapons and Shields|Sword,Dagger,Bow,Staff,Axe,Hammer,Great Sword,or Shield.|Sword|
|Hand Requirement|Weapons and Shields|One-Hand or Two-Hand.|One-Hand|
|Grade|Weapons by default|Common,Uncommon,Rare,Epic,Legendary,or Mythic.|Rare|
|Upgrade Level|Weapons by default|Smith Upgrade Level from `+0` to `+5`.|+3|
|Base Attributes|All Equipment|Normal stat bonuses granted by the item.|Physical Attack +18|
|Elemental Attributes|All Equipment|Elements,Damage Bonuses,or Resistances granted by the item.|Fire Damage Bonus +10%|
|Effects|All Equipment|Special combat effects such as Bleeding Chance or Stun Chance.|Bleeding Chance +15%|
|Passive Skills|All Equipment|Passive Skills granted while equipped.|Quick Draw|

> Grade and Upgrade Level belong to individual equipment items, never to the Player.  
> Shields may use Grade and Upgrade Level only if they are treated as upgradeable hand equipment in your system.

## Equipment Display Examples

|Equipment|Display Name|
|---|---|
|Common unupgraded Sword|Common Iron Sword +0|
|Rare upgraded Sword|Rare Iron Sword +3|
|Epic Two-Hand Great Sword|Epic Flamebrand Great Sword +5|
|Legendary Shield|Legendary Holy Aegis +2|
|Mythic Staff|Mythic Celestial Staff +5|

---

# Enemy-Only Attributes

## Enemy Identity and AI

|Attribute|Description|
|---|---|
|Enemy Name|Display name of the enemy.|
|Rank|Normal,Elite,Mini Boss,Boss,or Final Boss.|
|Combat Role|Example: Bruiser,Tank,Support,Mage,Archer,Controller,Assassin,or Boss.|
|Origin Region|The region where the enemy is primarily introduced.|
|Element Types|One or more elements used by the enemy. Example: `Fire,Air`.|
|Group AI Priority|Complete AI rules used while at least one other friendly enemy is alive.|
|Solo AI Priority|Complete AI rules used while the enemy is the only living enemy.|
|Boss Flags|Only used by Bosses or special enemies. Example: Cannot Escape,Repeatable Boss,Final Boss.|

> Target selection, low-HP reactions, phase changes, enrage behaviour, and summon conditions are written directly into Group AI Priority or Solo AI Priority. They are not stored as separate enemy attributes.

## Enemy Rewards

|Attribute|Description|
|---|---|
|Experience Reward|XP granted when the enemy is defeated.|
|Gold Reward|Minimum and maximum Gold dropped when the enemy is defeated.|
|Guaranteed Drops|All items that always drop when the enemy is defeated. Includes Boss Materials and Quest Items.|
|Possible Drops|Materials,equipment,or consumables that may drop.|
|Rare Drop Table|Rare equipment,special consumables,rare crafting materials,or special rewards.|

## Enemy Fields Not Used

|Removed Field|Reason|
|---|---|
|Primary Element|Derived automatically from the first listed Element Type.|
|AI Profile|Not needed. Group AI Priority and Solo AI Priority contain the complete behaviour.|
|Phase Thresholds|Written directly into AI Priority with conditions such as `HP <= 35%`.|
|Enrage Behaviour|Written directly into AI Priority through skills such as `Phase Rage`.|
|Spawn Areas|Stored only in Encounter Templates to avoid duplicate spawn information.|
|Compatible Allies|Stored only in Encounter Templates as exact designed combinations.|
|Encounter Weight|Stored only in Encounter Templates.|
|Minimum Spawn Count|Stored only in Encounter Templates.|
|Maximum Spawn Count|Stored only in Encounter Templates.|
|Encounter Type|Stored only in Encounter Templates.|
|Respawn Type|Stored only in Encounter Templates.|
|Summon List|Written directly into the summoning enemy's AI Priority.|
|Summon Limit|Written directly into the summoning enemy's AI Priority.|
|Summon Condition|Written directly into the summoning enemy's AI Priority.|
|Final Boss Reward|Quest Items belong under Guaranteed Drops.|

## Final Boss Reward Rule

|Enemy|Experience Reward|Gold Reward|Guaranteed Drops|Possible Drops|Rare Drop Table|
|---|---:|---:|---|---|---|
|Dragon King|0 XP|0 Gold|Dragon King's Seal|None|None|

> `Dragon King's Seal` is a Quest Item stored under Guaranteed Drops. The Dragon King drops no crafting materials,equipment,Gold,or Potions.

---

# Encounter Spawn System

## Parallel Region Progression

|Rule|Implementation|
|---|---|
|Elemental Regions|Forest,Desert,Mountain,Ember Wastes,Umbral Region,and Sanctum Region are the six elemental regions.|
|Final Region|Dragon King's Dominion is the seventh and final region.|
|Outer Area Access|The outer areas of almost all elemental regions can be visited early.|
|Soft Progression|Each region becomes significantly harder in deeper areas. When progress stops in one region,the Player can explore another region,collect materials,upgrade equipment,and return later.|
|Overlapping Difficulty|Area difficulty ranges overlap instead of following one fixed linear path.|
|Deep Area Access|Deep areas may use story keys,quest progress,or difficulty as soft progression gates.|
|Final Region Access|Dragon King's Dominion opens only after collecting the six Elemental Sigils.|
|Maximum Enemies|An encounter can contain a maximum of 3 living enemies. Summoned enemies also count toward this limit.|

## Core Spawn Rules

|Rule|Implementation|
|---|---|
|Encounter Selection|The game selects one prepared Encounter Template from the current area's encounter pool.|
|No Independent Monster Rolls|Do not randomly select each monster separately. Every encounter uses a prepared and balanced monster combination.|
|Exact Composition|The enemies listed in the selected Encounter Template spawn exactly as written.|
|Normal Encounter|Contains 1-3 Normal enemies.|
|Elite Encounter|Contains 1 Elite enemy alone,or 1 Elite enemy with 1-2 Normal enemies.|
|Mini Boss Encounter|Contains 1 Mini Boss alone,or 1 Mini Boss with 1 Normal enemy.|
|Boss Encounter|Contains 1 Boss alone,or 1 Boss with up to 2 scripted adds.|
|Final Boss Encounter|Dragon King always spawns alone.|
|Elite Limit|A Normal or Elite Encounter may contain a maximum of 1 Elite enemy.|
|Mini Boss Limit|An encounter may contain a maximum of 1 Mini Boss.|
|Boss Limit|An encounter may contain a maximum of 1 Boss.|
|Duplicate Rule|An enemy can only appear multiple times when the selected Encounter Template explicitly lists it more than once.|
|Combat Synergy|Every Encounter Template should contain enemies that work together through damage,control,tanking,or support.|
|Solo Challenge|Every enemy must still have a useful Solo AI Priority and be a small challenge when encountered alone.|
|Scripted Encounters|Quest fights,Mini Bosses,and Bosses use a fixed Encounter Template instead of normal random selection.|

## Encounter Template Attributes

|Attribute|Description|
|---|---|
|Encounter Name|Internal name of the encounter combination.|
|Region|Region where the Encounter Template is available.|
|Area|Specific area where the Encounter Template can appear.|
|Encounter Type|Normal,Elite,Mini Boss,Boss,or Scripted.|
|Enemy Slots|Exact enemies that spawn in this encounter.|
|Total Enemy Count|Number of spawned enemies. Maximum 3.|
|Weight|Relative chance of being selected from the valid encounter pool.|
|Minimum Player Level|Optional minimum recommended Player Level.|
|Progress Condition|Quest,area unlock,or story condition required for the template to become valid.|
|Difficulty Rating|Easy,Normal,Hard,Very Hard,or Boss.|
|Combat Theme|Intended combination such as Tank + Support,Control + Damage,or Fast Pressure.|
|Respawn Rule|Normal Respawn,Boss Respawn,Rare Spawn,One-Time Encounter,or Scripted Only.|
|Crossover Rule|Defines whether the template uses an enemy from an earlier region.|
|Special Rules|Optional rules such as Cannot Escape,First Encounter Only,or Guaranteed Chest.|



## Encounter Selection Algorithm

```text
1. Player enters an area or triggers an encounter.
2. Load every Encounter Template assigned to that area.
3. Remove invalid templates:
   - The Player has not met the required Progress Condition.
   - The Player is below the optional Minimum Player Level.
   - The template is a One-Time Encounter that was already completed.
   - The template is a Boss Encounter that was defeated and is not repeatable.
   - The template requires a quest state that is not currently active.
4. If a Scripted Encounter is active,select it immediately.
5. Otherwise,roll one valid Encounter Template using its Weight.
6. Spawn exactly the enemies listed in that template.
7. Apply the area's stat scaling and the template's optional crossover modifier.
8. Start combat.

---

## Documentation Links

This preserved source is retained in full. The canonical integrated design is in
[02_Attributes_and_Combat.md](02_Attributes_and_Combat.md); the documentation index is [00_README.md](00_README.md).
Where this source conflicts with newer documents, see
[16_Consistency_Audit.md](16_Consistency_Audit.md) rather than deleting this record.

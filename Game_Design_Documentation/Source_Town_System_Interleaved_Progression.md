# Town System

## Town Design Principles

The Town is the Player's permanent safe hub between expeditions. It contains recovery,travel,crafting,upgrades,inventory management,and optional Guild content.

|Rule|Implementation|
|---|---|
|Autosave|The game saves automatically after permanent changes and safe combat checkpoints.|
|Inn|The Inn restores HP and MP. It has no manual Save,Load,or dialogue function.|
|Global Progression|The main story progresses by world tier across all elemental regions instead of completing one region from start to finish.|
|Story Quests|Story Quests are issued by named NPCs,not the Guild.|
|Guild Quests|The Guild offers optional one-time quests and repeatable contracts.|
|Conditional Quest Items|Every Quest Item can only drop or appear while its linked Quest is active.|
|Repeatable Uniques|Repeatable Unique Monsters only spawn while their selected Bounty Contract is active.|
|Equipment Drop Cap|Loot and Quest reward equipment can be Common,Uncommon,Rare,or Epic. Legendary and Mythic equipment never drop.|
|Inventory|The Player starts with a 10-slot Backpack. Quest Items use a separate inventory and do not use Backpack slots.|
|Travel|The City Gate controls safe-area travel and progression locks.|

---

# Available Town Services


|Location|Main Function|Available Actions|
|---|---|---|
|Guild|Optional Quest Hub|Accept Guild Quests;Claim Rewards;Choose Repeatable Contracts;View Bounty Records.|
|Market|Buying,Selling,and Backpack Service|Buy Consumables;Buy Basic Ingredients;Sell Items;Upgrade Backpack;View Prices.|
|Alchemist|Potion Crafting|Craft Potions;View Recipes;Check Ingredients;Batch Craft.|
|Blacksmith|Equipment Upgrade and Salvage|Upgrade Equipment from `+0` to `+5`;Preview Costs;Salvage Equipment for Smithing Materials.|
|Enchanter|Equipment Grade and Disenchanting|Upgrade Grade from Common to Mythic;Preview Costs;Disenchant Equipment for Enchantment Materials.|
|Inn|Recovery Hub|Restore HP;Restore MP;Full Rest;Defeat Return.|
|City Gate|Travel Hub|Access Unlocked Areas;Travel to Discovered Safe Areas;Return to Town.|
|Player Menu|Character Management|Manage Inventory;Equip Items;View Stats;View Skills;View Quest Log.|

---

# Autosave System


## Core Rule

The game saves automatically. The Player never selects a manual Save or Load command.


|Trigger|When the Game Saves|
|---|---|
|Town Arrival|Immediately after the Player returns to Town.|
|Travel|Immediately after entering a Region or discovered Safe Area.|
|Quest State|After accepting,advancing,completing,abandoning,or claiming any Quest.|
|Inventory Change|After buying,selling,crafting,equipping,upgrading,disenchanting,or enchanting an Item.|
|Backpack Upgrade|Immediately after purchasing a Backpack capacity upgrade.|
|Rest|Immediately after the Inn restores HP and MP.|
|Combat Start|Immediately before a battle begins.|
|Combat Checkpoint|After every fully resolved Player Action or Enemy Action.|
|Combat End|Immediately after victory,defeat,escape,or surrender.|
|Boss or Unique Defeat|Immediately after defeating a Boss,Story Unique,or Contract Unique.|


|Safety Rule|Implementation|
|---|---|
|No Mid-Resolution Save|Do not save while Damage,Status Effects,or AI resolution is still processing.|
|Combat Checkpoint|Save only after an Action Lifecycle fully ends.|
|Quest Item Safety|Save immediately after a conditional Quest Item is acquired.|
|One-Time Boss Safety|A defeated one-time Story Boss stays defeated after loading.|
|No Manual Save|Do not show Save Game or Load Game options anywhere in Town.|

---

# Inventory and Backpack System


## Backpack Rules


|Rule|Implementation|
|---|---|
|Starting Capacity|The Player starts with 10 Backpack slots.|
|Slot Use|Each Equipment Item uses 1 slot. Each stackable item type uses 1 slot per stack.|
|Stack Limit|Consumables,Materials,and Ingredients stack up to 99 per slot.|
|Quest Items|Quest Items have a separate Quest Item inventory and use 0 Backpack slots.|
|Gold|Gold does not use Backpack slots.|
|Full Backpack|The Player cannot collect normal loot until a slot is freed. Quest Items can still be received.|
|Upgrade Source|Backpack upgrades are purchased from the Market Pack Merchant with Gold.|
|Maximum Capacity|Backpack capacity is capped at 40 slots.|

## Market Backpack Upgrades


|Upgrade|Capacity|Gold Cost|Unlock Condition|
|---|---|---|---|
|Starter Backpack|10 Slots|Free|Game Start.|
|Traveler Pack I|15 Slots|250 Gold|Available after `S-T1-01`.|
|Traveler Pack II|20 Slots|700 Gold|Available after `S-T2-01`.|
|Explorer Pack I|25 Slots|1,500 Gold|Available after `S-T3-01`.|
|Explorer Pack II|30 Slots|3,000 Gold|Available after `S-T4-01`.|
|Expedition Pack|35 Slots|5,500 Gold|Available after `S-T5-01`.|
|Dominion Pack|40 Slots|9,000 Gold|Available after `S-DRAGON-00`.|

---

# Quest System


## Quest Sources


|Quest Source|Purpose|Quest Types|
|---|---|---|
|Story NPC|Main progression and world narrative.|Story Quest;Area Quest;Boss Quest.|
|Guild|Optional one-time objectives.|Hunt Quest;Collection Quest;Unique Bounty;Crafting Quest.|
|Repeatable Contract Board|Selected repeatable farming content.|Per-Mob Kill Contract;Area Collection Contract;Repeatable Unique Bounty;Boss Challenge.|

## Quest Item Rules


|Rule|Implementation|
|---|---|
|Active Quest Requirement|A Quest Item can drop,spawn,or be interactable only while its exact linked Quest is active.|
|No Pre-Farming|Enemies never drop a future Story or Contract Quest Item before the Quest is accepted.|
|Guaranteed Contract Drops|A valid enemy drops 1 required Contract Quest Item with 100% chance while the linked Collection Contract is active until the required quantity is reached.|
|Guaranteed Unique Proof|A Contract Unique drops its listed Bounty Proof with 100% chance only while its Bounty Contract is active.|
|Story Item Source|Story Quest Items come from fixed interactions,scripted encounters,or Story Uniques only while the Story Quest is active.|
|Quest Item Inventory|Quest Items use a separate category and never consume Backpack slots.|
|No Selling|Quest Items cannot be sold,discarded,upgraded,or used as normal crafting material.|
|Duplicate Protection|After a linked objective is complete,the corresponding Quest Item stops dropping.|
|Turn-In|Quest Items are removed only when the Quest requires turn-in. Sigils and major relics remain permanently.|

## Repeatable Contract Board Rules


|Rule|Implementation|
|---|---|
|Board Choices|The Board shows 3 valid Contracts from unlocked Areas.|
|Active Limit|The Player may have 1 Repeatable Contract active at a time.|
|Per-Mob Contracts|Every normal enemy in an Area has its own repeatable Kill Contract.|
|Area Collection Contracts|Each non-boss Area has one repeatable shared-item Contract. Only listed carrier mobs drop that item while active.|
|Repeatable Unique Bounties|Each non-boss Area has one named Contract Unique. It spawns only while its Bounty Contract is active.|
|Boss Challenges|After its Story Boss is defeated,each regional Boss Area offers a repeatable Boss Challenge Contract. Sigils never drop again.|
|Final Boss Exception|Dragon King’s Lair has no repeatable contract. The Dragon King is a one-time final Story Boss.|
|Refresh|A completed or abandoned Contract is replaced after the Player returns to Town.|
|No Permanent Rewards|Repeatables award XP,Gold,materials,and at most consumables. They never award Sigils,permanent recipes,or Legendary/Mythic equipment.|
|Shared Progress|A defeat can advance any active Story or Guild objective that names that enemy.|

## Equipment Drop Rules


|Source|Maximum Equipment Grade|Rule|
|---|---|---|
|Normal Enemy|Rare|Normal enemies can drop Common,Uncommon,or Rare equipment.|
|Elite,Contract Unique,Regional Boss|Epic|These encounters can drop up to Epic equipment.|
|Quest Reward|Epic|Quest equipment rewards are capped at Epic.|
|Market|Epic|The Market may sell equipment up to Epic only if equipment stock is later added.|
|Legendary Equipment|No Drop|Legendary equipment is created only by Enchanter grade upgrades.|
|Mythic Equipment|No Drop|Mythic equipment is created only by Enchanter grade upgrades.|
|Dragon King|No Equipment Drop|The final Dragon King only awards the Dragon King's Seal and XP.|

---

# Global World Progression


The main story does not clear one entire element region at a time. It moves through all regions by shared World Tiers.


The fixed order inside every shared World Tier is:

```text
Earth → Air → Water → Fire → Darkness → Holy
```


The Player may freely revisit every previously cleared Area for farming. The next Story Quest unlocks only after the immediately previous Story Quest in the global order is complete.


## World Tier Order


|World Tier|Earth|Air|Water|Fire|Darkness|Holy|
|---|---|---|---|---|---|---|
|1|Forest Entrance|Desert Border|Mountain Foothills|Ashen Border|Gloomwood|Sunlit Road|
|2|Goblin Forest|Scorching Dunes|Mountain Pass|Ember Fields|Shadow Marsh|Temple Gardens|
|3|Overgrown Trail|Bandit Camp|Echo Mine|Lava Fissures|Forgotten Crypt|Sanctum Halls|
|4|Deep Woods|Ancient Ruins|Ice Caves|Magma Forge|Void Rift|Dawn Basilica|
|5|King's Clearing|Ruin Guardian Chamber|Frozen Peak|Inferno Core|Dread Throne|Oracle Chamber|
|6|Goblin King|Ruin Guardian|Summit Shrine / Frost Titan|Inferno Lord|Shadow Lord|Oracle|

After World Tier 6,the Player holds all six Regional Sigils and unlocks Dragon King's Dominion. Dragon quests are always completed last.


## Story Quest Rules


|Rule|Implementation|
|---|---|
|Quest Givers|Every Story Quest is given by a named NPC in Town or the active Area.|
|Story Limit|Only the next global Story Quest can be accepted or advanced.|
|Area Unlock|Completing a Story Quest unlocks the next Area in the global World Tier order.|
|Farming|Previously cleared Areas remain accessible through the City Gate.|
|Boss Gate|Regional Bosses are unavailable until their World Tier 6 Story Quest is active.|
|Sigils|Each regional boss awards its Sigil once. Sigils are permanent Quest Items.|
|Dragon Unlock|All six Sigils are required for `S-DRAGON-00`.|

## Prologue


|ID|Quest|Giver|Area|Description|Objectives|Rewards|
|---|---|---|---|---|---|---|
|S-000|The Fractured Compass|Archivist Mira Vale|Town Archive|Mira reveals that the Wayfinder Compass reacts to six elemental Sigils.|Speak with Mira;Receive the `Wayfinder Compass`;Travel to Forest Entrance.|100 XP;75 Gold;`Wayfinder Compass`.|


## World Tier 1 — Outer Routes


|ID|Quest|Giver|Area|Description|Objectives|Rewards|
|---|---|---|---|---|---|---|
|S-T1-01|Missing Surveyors|Ranger Elian Mossward|Forest Entrance|Elian needs proof that the first forest route can be reopened.|Recover 3 `Surveyor Markers`;Defeat 4 Forest Rats;Return to Elian.|100 XP;75 Gold;3x Forest Herb;1x Empty Bottle.|
|S-T1-02|The Silent Caravan|Scout Zahra Naim|Desert Border|Zahra needs the lost caravan ledger before the wind erases its trail.|Recover the `Caravan Ledger`;Defeat 3 Desert Rats;Return to Zahra.|130 XP;100 Gold;2x Cactus Sap;1x Empty Bottle.|
|S-T1-03|The Lost Climber|Climber Sera Holt|Mountain Foothills|Sera needs her partner's locket to identify the route toward the mountain pass.|Recover the `Frostbitten Locket`;Defeat 3 Snow Wolves;Return to Sera.|160 XP;125 Gold;2x Ice Moss;1x Bandage.|
|S-T1-04|Ash on the Wind|Refugee Sellen Marr|Ashen Border|Sellen needs a scout report to guide refugees away from the spreading fires.|Recover the `Cinder Scout Report`;Defeat 3 Ash Lizards;Return to Sellen.|190 XP;150 Gold;2x Forest Herb;1x Ember Core.|
|S-T1-05|Lanterns for the Lost|Sister Maren Vey|Gloomwood|Maren asks you to recover a lantern that still remembers the path of missing pilgrims.|Recover the `Lantern of Lost Names`;Defeat 3 Shades;Return to Maren.|220 XP;175 Gold;2x Cursed Twig;1x Mana Mushroom.|
|S-T1-06|The Unrung Bell|Novice Auri Sol|Sunlit Road|Auri needs the ceremonial bell before the dawn procession can continue.|Recover the `Dawn Processional Bell`;Defeat 3 Radiant Hawks;Return to Auri.|250 XP;200 Gold;2x Forest Herb;1x Holy Crystal.|


## World Tier 2 — Inner Trails


|ID|Quest|Giver|Area|Description|Objectives|Rewards|
|---|---|---|---|---|---|---|
|S-T2-01|The Broken Totem|Goblin Exile Rukk|Goblin Forest|Rukk asks you to break the totem binding forest creatures to the Goblin King's will.|Defeat the `Totem-Bound Goblin`;Recover the `Earthen Totem Shard`;Report to Rukk.|330 XP;280 Gold;2x Iron Scrap;1x Magic Crystal.|
|S-T2-02|Dunes Without Song|Windcaller Fari|Scorching Dunes|Fari needs a sample of singing sand from the creature silencing the desert wind.|Defeat the `Glasswing Vulture`;Recover the `Singing Sand Vial`;Return to Fari.|370 XP;320 Gold;2x Harpy Feather;1x Air Crystal.|
|S-T2-03|Echoes in Stone|Miner Doran Vale|Mountain Pass|Doran asks you to silence an echo that lures travelers toward dangerous cliffs.|Defeat the `Echo Stalker`;Recover the `Resonance Crystal`;Bring it to Doran.|410 XP;360 Gold;2x Crystal Shard;1x Frost Crystal.|
|S-T2-04|The Ashfang Hunt|Tracker Kora Flint|Ember Fields|Kora needs proof that the scarred hound driving creatures toward the refugees is gone.|Defeat the `Ashfang Hound`;Recover the `Ember Collar`;Return to Kora.|450 XP;400 Gold;2x Beast Claw;1x Ember Core.|
|S-T2-05|The Bogshade Trail|Tracker Rovan Kells|Shadow Marsh|Rovan needs the token of the hunter who marks travelers before they vanish in the reeds.|Defeat the `Bogshade Huntress`;Recover the `Marsh Hunter's Token`;Return to Rovan.|490 XP;440 Gold;2x Venom Sac;1x Dark Crystal.|
|S-T2-06|Seeds Beneath the Ash|Gardener Isolde Venn|Temple Gardens|Isolde asks you to restore a sacred seed bed corrupted beneath the garden soil.|Defeat the `Blighted Blossom`;Recover the `Sunroot Seed`;Return to Isolde.|530 XP;480 Gold;2x Holy Crystal;1x Magic Crystal.|


## World Tier 3 — Contested Grounds


|ID|Quest|Giver|Area|Description|Objectives|Rewards|
|---|---|---|---|---|---|---|
|S-T3-01|A Trail Choked by Thorns|Herbalist Nessa Reed|Overgrown Trail|Nessa needs the core of the living thorn knot that has sealed the old forest trail.|Defeat the `Thorn Matriarch`;Recover the `Thornheart Knot`;Bring it to Nessa.|700 XP;600 Gold;3x Spider Silk;`Thornward Ring` (Rare).|
|S-T3-02|The Stolen Standard|Captain Nadir Qasr|Bandit Camp|Nadir needs the stormbound standard returned before the ruins can be entered safely.|Recover the `Stormbound Standard`;Defeat 4 Bandit enemies;Return to Nadir.|760 XP;650 Gold;3x Iron Ore;`Dune Watcher's Charm` (Rare).|
|S-T3-03|The Collapsed Shaft|Foreman Brann Orevein|Echo Mine|Brann needs the drill key hidden beyond the blocked evacuation shaft.|Recover the `Miner's Drill Key`;Defeat 4 Rock Crawlers or Crystal Beetles;Return to Brann.|820 XP;700 Gold;3x Iron Ore;1x Stone Core.|
|S-T3-04|Pressure Below|Engineer Rusk Vale|Lava Fissures|Rusk needs an intact pressure valve to stabilize the ancient lava-control network.|Recover the `Molten Pressure Valve`;Defeat 3 Lava Fissure enemies;Return to Rusk.|880 XP;750 Gold;2x Obsidian Fragment;1x Molten Core.|
|S-T3-05|Names on the Epitaph|Gravekeeper Oren Vale|Forgotten Crypt|Oren needs the stolen royal seal returned before the crypt's wards collapse.|Recover the `Epitaph Seal`;Defeat 3 Grave Wraiths or Plague Mummies;Return to Oren.|940 XP;800 Gold;2x Cursed Twig;2x Crystal Shard.|
|S-T3-06|The Sanctum Cipher|Archivist Cael Ardent|Sanctum Halls|Cael needs a cipher plate that explains why the Oracle sealed herself away.|Recover the `Sanctum Cipher Plate`;Defeat 3 Stone Guardians or Inquisitors;Return to Cael.|1,000 XP;850 Gold;2x Ancient Coin;2x Crystal Shard.|


## World Tier 4 — Deep Sanctums


|ID|Quest|Giver|Area|Description|Objectives|Rewards|
|---|---|---|---|---|---|---|
|S-T4-01|Roots of the Old Grove|Druid Aelor Greenbark|Deep Woods|Aelor asks you to prove that the Goblin King's ritual is draining the old grove.|Inspect the Grove Shrine;Recover the `Ancient Sap Vial`;Defeat 2 Treants or Fungus enemies;Return to Aelor.|1,250 XP;1,050 Gold;1x Stone Core;2x Crystal Shard.|
|S-T4-02|The Sealed Observatory|Scholar Iram Voss|Ancient Ruins|Iram needs the observatory lens restored to reveal the path toward the guardian chamber.|Activate 3 Wind Seals;Recover the `Astral Lens`;Defeat 2 Sand Wraiths or Mummies.|1,340 XP;1,130 Gold;2x Magic Crystal;1x Ancient Coin.|
|S-T4-03|Beneath the Ice|Scholar Lyra Fen|Ice Caves|Lyra seeks a frozen chart that records the Titan's route to the summit shrine.|Defeat the `Icebound Scribe`;Recover the `Frozen Star Chart`;Return to Lyra.|1,430 XP;1,210 Gold;2x Frost Crystal;`Echo Miner Pendant` (Rare).|
|S-T4-04|The Forge That Remembers|Forgemaster Nyra Vale|Magma Forge|Nyra needs the forge control key before the Inferno Lord can arm more servants.|Defeat the `Forged Flame Sentinel`;Recover the `Forge Heart Key`;Return to Nyra.|1,520 XP;1,290 Gold;2x Molten Core;`Forgehand Bracer` (Epic).|
|S-T4-05|The Rift Compass|Arcanist Veil Ordan|Void Rift|Veil needs a living echo from the shifting rift to calibrate a path to the Dread Throne.|Defeat the `Riftbound Echo`;Recover the `Void Compass`;Return to Veil.|1,610 XP;1,370 Gold;2x Dark Crystal;`Mourning Veil` (Epic).|
|S-T4-06|A Fallen Wing|High Deacon Tal Rhyse|Dawn Basilica|Tal asks you to release a fallen seraph and recover the oath feather that anchors the Basilica wards.|Defeat the `Fallen Seraph Amon`;Recover the `Oath Feather`;Return to Tal.|1,700 XP;1,450 Gold;2x Holy Crystal;`Dawnkeeper Brooch` (Epic).|


## World Tier 5 — Sigil Approaches


|ID|Quest|Giver|Area|Description|Objectives|Rewards|
|---|---|---|---|---|---|---|
|S-T5-01|The King's Ritual|Ranger Elian Mossward|King's Clearing|Elian asks you to disrupt the ritual surrounding the Goblin King's arena before the final duel.|Destroy 3 Royal Totems;Recover the `Royal Clearing Key`;Return to Elian.|2,000 XP;1,700 Gold;2x Magic Crystal;1x Enchantment Fragment.|
|S-T5-02|The Guardian's Oath|Scholar Iram Voss|Ruin Guardian Chamber|The restored observatory reveals the guardian's oath. Iram needs its oath plate to open the trial.|Recover the `Guardian Oath Plate`;Defeat 2 Ruin Chamber sentries;Return to Iram.|2,100 XP;1,790 Gold;2x Air Crystal;1x Enchantment Fragment.|
|S-T5-03|The Peak's Whisper|Priestess Asha Mire|Frozen Peak|Asha asks you to restore the final prayer beacon before the path to Summit Shrine can open.|Light 3 Prayer Beacons;Recover the `Shrine Prayer Cord`;Defeat 2 Frozen Peak enemies.|2,200 XP;1,880 Gold;2x Ice Moss;2x Magic Crystal.|
|S-T5-04|Heart of the Inferno|Forgemaster Nyra Vale|Inferno Core|Nyra needs you to bind the erupting core long enough to challenge the Inferno Lord.|Install the `Forge Heart Key`;Recover the `Core Binding Chain`;Return to Nyra.|2,300 XP;1,970 Gold;1x Molten Core;2x Obsidian Fragment.|
|S-T5-05|The Throne's Last Veil|Arcanist Veil Ordan|Dread Throne|Veil asks you to pierce the final veil that prevents entry to the Shadow Lord's court.|Use the `Void Compass`;Recover the `Veilbreaker Sigil`;Return to Veil.|2,400 XP;2,060 Gold;2x Dark Crystal;1x Enchantment Crystal.|
|S-T5-06|The Oracle's Trial|High Deacon Tal Rhyse|Oracle Chamber|Tal asks you to place the restored cipher and open the Oracle's final trial.|Use the `Sanctum Cipher Plate`;Recover the `Dawn Trial Seal`;Return to Tal.|2,500 XP;2,150 Gold;2x Holy Crystal;1x Enchantment Crystal.|


## World Tier 6 — Regional Sigils


|ID|Quest|Giver|Area|Description|Objectives|Rewards|
|---|---|---|---|---|---|---|
|S-T6-01|Crown of the Clearing|Ranger Elian Mossward|King's Clearing|The royal ritual is broken. Defeat the Goblin King and recover the Earth Sigil.|Defeat the Goblin King;Obtain the `Earth Sigil`;Speak with Elian.|2,850 XP;2,450 Gold;`Earth Sigil`;3x Crystal Shard;1x Magic Crystal.|
|S-T6-02|The Ruin Guardian|Scholar Iram Voss|Ruin Guardian Chamber|The oath plate opens the chamber. Defeat the Ruin Guardian and recover the Air Sigil.|Defeat the Ruin Guardian;Obtain the `Air Sigil`;Speak with Iram.|3,000 XP;2,600 Gold;`Air Sigil`;2x Air Crystal;2x Crystal Shard.|
|S-T6-03|Shrine of the Titan|Priestess Asha Mire|Summit Shrine|The shrine is open. Defeat the Frost Titan and recover the Water Sigil.|Defeat the Frost Titan;Obtain the `Water Sigil`;Speak with Asha.|3,150 XP;2,750 Gold;`Water Sigil`;2x Frost Crystal;1x Magic Crystal.|
|S-T6-04|Lord of the Inferno|Forgemaster Nyra Vale|Inferno Core|The core is bound. Defeat the Inferno Lord and recover the Fire Sigil.|Defeat the Inferno Lord;Obtain the `Fire Sigil`;Speak with Nyra.|3,300 XP;2,900 Gold;`Fire Sigil`;1x Molten Core;2x Obsidian Fragment.|
|S-T6-05|The Lord Behind the Veil|Arcanist Veil Ordan|Dread Throne|The final veil is open. Defeat the Shadow Lord and recover the Darkness Sigil.|Defeat the Shadow Lord;Obtain the `Darkness Sigil`;Speak with Veil.|3,450 XP;3,050 Gold;`Darkness Sigil`;2x Dark Crystal;1x Dragon Rune.|
|S-T6-06|The Oracle's Choice|High Deacon Tal Rhyse|Oracle Chamber|The trial is open. Defeat the Oracle and recover the Holy Sigil.|Defeat the Oracle;Obtain the `Holy Sigil`;Speak with Tal.|3,600 XP;3,200 Gold;`Holy Sigil`;2x Holy Crystal;1x Dragon Rune.|


## Dragon King's Dominion — Final Story


|ID|Quest|Giver|Area|Description|Objectives|Rewards|
|---|---|---|---|---|---|---|
|S-DRAGON-00|The Seventh Path|Archivist Mira Vale|Town Archive|With all six Regional Sigils restored,the Wayfinder Compass opens a path to Dragon King's Dominion.|Show all six Regional Sigils;Receive the `Dominion Map`;Travel to Dragon Valley.|4,000 XP;3,500 Gold;`Dominion Map`;Unlocks Dragon King's Dominion.|
|S-DRAGON-01|Signal Across the Valley|Commander Varek Thorne|Dragon Valley|Varek needs a signal horn to guide the remaining scouts through Dragon Valley.|Recover the `Dragonwatch Signal Horn`;Defeat 3 Dragon Whelps;Return to Varek.|4,350 XP;3,800 Gold;2x Dragon Rune;1x Obsidian Fragment.|
|S-DRAGON-02|Words in Ash|Draconic Exile Seraphine|Dragon Cave|Seraphine seeks an old tablet that reveals how the Dragon King bound the Dominion to the Sigils.|Recover the `Ashen Draconic Tablet`;Defeat 3 Dragon Servants or Dragon Archers;Return to Seraphine.|4,700 XP;4,100 Gold;1x Ancient Dragon Scale;2x Dragon Rune.|
|S-DRAGON-03|The Citadel Gate|Captain Orin Hale|Obsidian Citadel|Orin needs the lost command sigil used by the Obsidian Citadel's warden.|Defeat the `Obsidian Warden Korr`;Recover the `Citadel Gate Sigil`;Return to Orin.|5,050 XP;4,400 Gold;1x Ancient Dragon Fang;`Dragonwatch Band` (Epic).|
|S-DRAGON-04|The Ancient Witness|Archivist Mira Vale|Ancient Nest|Mira asks you to obtain a memory scale from the Ancient Dragon before the final assault.|Defeat the Ancient Dragon once;Recover the `Ancient Memory Scale`;Return to Mira.|5,400 XP;4,700 Gold;1x Mythic Ember;1x Dragon Rune;Unlocks Ancient Dragon repeatable farming.|
|S-DRAGON-05|Seal the Dominion|Commander Varek Thorne|Dragon King's Lair|Defeat the Dragon King and claim the proof that the Dominion is sealed.|Defeat the Dragon King;Obtain the `Dragon King's Seal`.|6,500 XP;`Dragon King's Seal`.|

> `S-DRAGON-05` awards no Gold,materials,equipment,or potions.

---

# Repeatable Contract Catalogue


## Repeatable Reward Scale


|Tier|Kill Contract|Collection Contract|Unique Bounty / Boss Challenge|
|---|---|---|---|
|1|80 XP;65 Gold;1x Iron Scrap.|105 XP;85 Gold;2x Basic Ingredient.|175 XP;145 Gold;1x Iron Scrap;1x Enchantment Dust.|
|2|180 XP;150 Gold;1x Iron Ore.|230 XP;190 Gold;2x Regional Ingredient.|350 XP;300 Gold;1x Iron Ore;1x Enchantment Fragment.|
|3|400 XP;340 Gold;1x Crystal Shard.|510 XP;430 Gold;1x Magic Crystal.|720 XP;610 Gold;1x Crystal Shard;1x Enchantment Crystal.|
|4|780 XP;660 Gold;1x Magic Crystal.|980 XP;830 Gold;1x Enchantment Fragment.|1,350 XP;1,150 Gold;1x Magic Crystal;1x Enchantment Crystal.|
|5|1,300 XP;1,100 Gold;1x Enchantment Fragment.|1,600 XP;1,350 Gold;1x Enchantment Crystal.|2,200 XP;1,850 Gold;1x Enchantment Crystal;1x Regional Upgrade Material.|
|6|2,500 XP;2,100 Gold;1x Enchantment Crystal.|3,000 XP;2,550 Gold;1x Dragon Rune.|3,600 XP;3,050 Gold;1x Dragon Rune;1x Regional Boss Material.|
|Dragon|2,650 XP;2,250 Gold;1x Dragon Rune.|3,150 XP;2,700 Gold;1x Ancient Dragon Scale.|4,300 XP;3,650 Gold;1x Dragon Rune;1x High-Tier Material.|

## Contract Generation Rules


|Contract Type|Objective Rule|Quest Item Rule|
|---|---|---|
|Per-Mob Kill Contract|Defeat the named target count in the listed Area.|No Quest Item is required.|
|Area Collection Contract|Defeat eligible carrier mobs until the required shared Area Contract Item count is reached.|The shared item drops only while that exact Contract is active.|
|Repeatable Unique Bounty|Defeat the named Contract Unique and obtain 1 Bounty Proof.|The Unique spawns and drops its Proof only while that exact Bounty Contract is active.|
|Boss Challenge|Defeat the named Regional Boss after its Story Quest is complete.|The Boss drops a Challenge Proof only while the Challenge Contract is active. Sigils never drop again.|


## World Tier 1 Repeatable Contracts


### Forest Entrance (Earth)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-EFE-K01|Kill Contract|Forest Rat Hunt|Defeat 8 Forest Rat in Forest Entrance.|None|80 XP;65 Gold;1x Iron Scrap.|
|R-EFE-K02|Kill Contract|Wild Boar Hunt|Defeat 8 Wild Boar in Forest Entrance.|None|80 XP;65 Gold;1x Iron Scrap.|
|R-EFE-C01|Collection Contract|Forest Entrance Evidence|Collect 6 `Trail Survey Tag` from eligible carrier mobs in Forest Entrance.|`Trail Survey Tag` drops from Forest Rat, Wild Boar only while this Contract is active.|105 XP;85 Gold;1x Iron Scrap.|
|R-EFE-B01|Unique Bounty|Barkhide Boar Bounty|Defeat Barkhide Boar in Forest Entrance;Collect `Barkhide Tusk`.|Barkhide Boar spawns only while this Bounty Contract is active. `Barkhide Tusk` drops only while this Contract is active.|175 XP;145 Gold;1x Iron Scrap;1x Enchantment Dust.|


### Desert Border (Air)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-ADB-K01|Kill Contract|Desert Rat Hunt|Defeat 8 Desert Rat in Desert Border.|None|80 XP;65 Gold;1x Cactus Sap.|
|R-ADB-K02|Kill Contract|Sand Beetle Hunt|Defeat 8 Sand Beetle in Desert Border.|None|80 XP;65 Gold;1x Cactus Sap.|
|R-ADB-C01|Collection Contract|Desert Border Evidence|Collect 6 `Caravan Wheel Seal` from eligible carrier mobs in Desert Border.|`Caravan Wheel Seal` drops from Desert Rat, Sand Beetle only while this Contract is active.|105 XP;85 Gold;1x Cactus Sap.|
|R-ADB-B01|Unique Bounty|Dustrunner Scarab Bounty|Defeat Dustrunner Scarab in Desert Border;Collect `Dustrunner Carapace`.|Dustrunner Scarab spawns only while this Bounty Contract is active. `Dustrunner Carapace` drops only while this Contract is active.|175 XP;145 Gold;1x Cactus Sap;1x Enchantment Dust.|


### Mountain Foothills (Water)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-WMF-K01|Kill Contract|Snow Wolf Hunt|Defeat 8 Snow Wolf in Mountain Foothills.|None|80 XP;65 Gold;1x Ice Moss.|
|R-WMF-K02|Kill Contract|Ice Bat Hunt|Defeat 8 Ice Bat in Mountain Foothills.|None|80 XP;65 Gold;1x Ice Moss.|
|R-WMF-C01|Collection Contract|Mountain Foothills Evidence|Collect 6 `Climber Route Flag` from eligible carrier mobs in Mountain Foothills.|`Climber Route Flag` drops from Snow Wolf, Ice Bat only while this Contract is active.|105 XP;85 Gold;1x Ice Moss.|
|R-WMF-B01|Unique Bounty|Whitefang Alpha Bounty|Defeat Whitefang Alpha in Mountain Foothills;Collect `Whitefang Pelt`.|Whitefang Alpha spawns only while this Bounty Contract is active. `Whitefang Pelt` drops only while this Contract is active.|175 XP;145 Gold;1x Ice Moss;1x Enchantment Dust.|


### Ashen Border (Fire)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-FAB-K01|Kill Contract|Ash Lizard Hunt|Defeat 8 Ash Lizard in Ashen Border.|None|80 XP;65 Gold;1x Ember Core.|
|R-FAB-K02|Kill Contract|Ember Hound Hunt|Defeat 8 Ember Hound in Ashen Border.|None|80 XP;65 Gold;1x Ember Core.|
|R-FAB-C01|Collection Contract|Ashen Border Evidence|Collect 6 `Evacuation Route Token` from eligible carrier mobs in Ashen Border.|`Evacuation Route Token` drops from Ash Lizard, Ember Hound only while this Contract is active.|105 XP;85 Gold;1x Ember Core.|
|R-FAB-B01|Unique Bounty|Ashfang Hound Bounty|Defeat Ashfang Hound in Ashen Border;Collect `Ashfang Collar`.|Ashfang Hound spawns only while this Bounty Contract is active. `Ashfang Collar` drops only while this Contract is active.|175 XP;145 Gold;1x Ember Core;1x Enchantment Dust.|


### Gloomwood (Darkness)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DG-K01|Kill Contract|Shade Hunt|Defeat 8 Shade in Gloomwood.|None|80 XP;65 Gold;1x Cursed Twig.|
|R-DG-K02|Kill Contract|Bone Hound Hunt|Defeat 8 Bone Hound in Gloomwood.|None|80 XP;65 Gold;1x Cursed Twig.|
|R-DG-C01|Collection Contract|Gloomwood Evidence|Collect 6 `Pilgrim Name Strip` from eligible carrier mobs in Gloomwood.|`Pilgrim Name Strip` drops from Shade, Bone Hound only while this Contract is active.|105 XP;85 Gold;1x Cursed Twig.|
|R-DG-B01|Unique Bounty|Lantern Shade Bounty|Defeat Lantern Shade in Gloomwood;Collect `Lantern Wick`.|Lantern Shade spawns only while this Bounty Contract is active. `Lantern Wick` drops only while this Contract is active.|175 XP;145 Gold;1x Cursed Twig;1x Enchantment Dust.|


### Sunlit Road (Holy)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-HSR-K01|Kill Contract|Sun Acolyte Hunt|Defeat 8 Sun Acolyte in Sunlit Road.|None|80 XP;65 Gold;1x Holy Crystal.|
|R-HSR-K02|Kill Contract|Temple Squire Hunt|Defeat 8 Temple Squire in Sunlit Road.|None|80 XP;65 Gold;1x Holy Crystal.|
|R-HSR-C01|Collection Contract|Sunlit Road Evidence|Collect 6 `Procession Ribbon` from eligible carrier mobs in Sunlit Road.|`Procession Ribbon` drops from Sun Acolyte, Temple Squire only while this Contract is active.|105 XP;85 Gold;1x Holy Crystal.|
|R-HSR-B01|Unique Bounty|Sunwing Hawk Bounty|Defeat Sunwing Hawk in Sunlit Road;Collect `Sunwing Feather`.|Sunwing Hawk spawns only while this Bounty Contract is active. `Sunwing Feather` drops only while this Contract is active.|175 XP;145 Gold;1x Holy Crystal;1x Enchantment Dust.|


## World Tier 2 Repeatable Contracts


### Goblin Forest (Earth)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-EGF-K01|Kill Contract|Goblin Scout Hunt|Defeat 8 Goblin Scout in Goblin Forest.|None|180 XP;150 Gold;1x Iron Ore.|
|R-EGF-K02|Kill Contract|Goblin Dagger Hunt|Defeat 8 Goblin Dagger in Goblin Forest.|None|180 XP;150 Gold;1x Iron Ore.|
|R-EGF-K03|Kill Contract|Goblin Archer Hunt|Defeat 8 Goblin Archer in Goblin Forest.|None|180 XP;150 Gold;1x Iron Ore.|
|R-EGF-K04|Kill Contract|Goblin Shaman Hunt|Defeat 8 Goblin Shaman in Goblin Forest.|None|180 XP;150 Gold;1x Iron Ore.|
|R-EGF-C01|Collection Contract|Goblin Forest Evidence|Collect 6 `Goblin Patrol Token` from eligible carrier mobs in Goblin Forest.|`Goblin Patrol Token` drops from Goblin Scout, Goblin Dagger, Goblin Archer only while this Contract is active.|230 XP;190 Gold;1x Iron Ore.|
|R-EGF-B01|Unique Bounty|Boneknife Skulk Bounty|Defeat Boneknife Skulk in Goblin Forest;Collect `Boneknife Insignia`.|Boneknife Skulk spawns only while this Bounty Contract is active. `Boneknife Insignia` drops only while this Contract is active.|350 XP;300 Gold;1x Iron Ore;1x Enchantment Fragment.|


### Scorching Dunes (Air)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-ASD-K01|Kill Contract|Sand Scorpion Hunt|Defeat 8 Sand Scorpion in Scorching Dunes.|None|180 XP;150 Gold;1x Air Crystal.|
|R-ASD-K02|Kill Contract|Vulture Hunt|Defeat 8 Vulture in Scorching Dunes.|None|180 XP;150 Gold;1x Air Crystal.|
|R-ASD-C01|Collection Contract|Scorching Dunes Evidence|Collect 6 `Singing Sand Packet` from eligible carrier mobs in Scorching Dunes.|`Singing Sand Packet` drops from Sand Scorpion, Vulture only while this Contract is active.|230 XP;190 Gold;1x Air Crystal.|
|R-ASD-B01|Unique Bounty|Glasswing Vulture Bounty|Defeat Glasswing Vulture in Scorching Dunes;Collect `Glasswing Feather`.|Glasswing Vulture spawns only while this Bounty Contract is active. `Glasswing Feather` drops only while this Contract is active.|350 XP;300 Gold;1x Air Crystal;1x Enchantment Fragment.|


### Mountain Pass (Water)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-WMP-K01|Kill Contract|Rock Crawler Hunt|Defeat 8 Rock Crawler in Mountain Pass.|None|180 XP;150 Gold;1x Crystal Shard.|
|R-WMP-K02|Kill Contract|Harpy Hunt|Defeat 8 Harpy in Mountain Pass.|None|180 XP;150 Gold;1x Crystal Shard.|
|R-WMP-C01|Collection Contract|Mountain Pass Evidence|Collect 6 `Pass Supply Tag` from eligible carrier mobs in Mountain Pass.|`Pass Supply Tag` drops from Rock Crawler, Harpy only while this Contract is active.|230 XP;190 Gold;1x Crystal Shard.|
|R-WMP-B01|Unique Bounty|Echo Stalker Bounty|Defeat Echo Stalker in Mountain Pass;Collect `Echo Fragment`.|Echo Stalker spawns only while this Bounty Contract is active. `Echo Fragment` drops only while this Contract is active.|350 XP;300 Gold;1x Crystal Shard;1x Enchantment Fragment.|


### Ember Fields (Fire)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-FEF-K01|Kill Contract|Lava Slime Hunt|Defeat 8 Lava Slime in Ember Fields.|None|180 XP;150 Gold;1x Obsidian Fragment.|
|R-FEF-K02|Kill Contract|Magma Beetle Hunt|Defeat 8 Magma Beetle in Ember Fields.|None|180 XP;150 Gold;1x Obsidian Fragment.|
|R-FEF-K03|Kill Contract|Ash Cultist Hunt|Defeat 8 Ash Cultist in Ember Fields.|None|180 XP;150 Gold;1x Obsidian Fragment.|
|R-FEF-C01|Collection Contract|Ember Fields Evidence|Collect 6 `Heatproof Sample` from eligible carrier mobs in Ember Fields.|`Heatproof Sample` drops from Lava Slime, Magma Beetle only while this Contract is active.|230 XP;190 Gold;1x Obsidian Fragment.|
|R-FEF-B01|Unique Bounty|Magmaheart Slime Bounty|Defeat Magmaheart Slime in Ember Fields;Collect `Magmaheart Core`.|Magmaheart Slime spawns only while this Bounty Contract is active. `Magmaheart Core` drops only while this Contract is active.|350 XP;300 Gold;1x Obsidian Fragment;1x Enchantment Fragment.|


### Shadow Marsh (Darkness)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DSM-K01|Kill Contract|Shadow Spider Hunt|Defeat 8 Shadow Spider in Shadow Marsh.|None|180 XP;150 Gold;1x Venom Sac.|
|R-DSM-K02|Kill Contract|Dark Wolf Hunt|Defeat 8 Dark Wolf in Shadow Marsh.|None|180 XP;150 Gold;1x Venom Sac.|
|R-DSM-C01|Collection Contract|Shadow Marsh Evidence|Collect 6 `Marsh Trail Marker` from eligible carrier mobs in Shadow Marsh.|`Marsh Trail Marker` drops from Shadow Spider, Dark Wolf only while this Contract is active.|230 XP;190 Gold;1x Venom Sac.|
|R-DSM-B01|Unique Bounty|Bogshade Huntress Bounty|Defeat Bogshade Huntress in Shadow Marsh;Collect `Bogshade Token`.|Bogshade Huntress spawns only while this Bounty Contract is active. `Bogshade Token` drops only while this Contract is active.|350 XP;300 Gold;1x Venom Sac;1x Enchantment Fragment.|


### Temple Gardens (Holy)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-HTG-K01|Kill Contract|Radiant Hawk Hunt|Defeat 8 Radiant Hawk in Temple Gardens.|None|180 XP;150 Gold;1x Holy Crystal.|
|R-HTG-K02|Kill Contract|Light Sprite Hunt|Defeat 8 Light Sprite in Temple Gardens.|None|180 XP;150 Gold;1x Holy Crystal.|
|R-HTG-K03|Kill Contract|Sacred Treant Hunt|Defeat 8 Sacred Treant in Temple Gardens.|None|180 XP;150 Gold;1x Holy Crystal.|
|R-HTG-C01|Collection Contract|Temple Gardens Evidence|Collect 6 `Sunroot Pollen` from eligible carrier mobs in Temple Gardens.|`Sunroot Pollen` drops from Radiant Hawk, Light Sprite only while this Contract is active.|230 XP;190 Gold;1x Holy Crystal.|
|R-HTG-B01|Unique Bounty|Blighted Blossom Bounty|Defeat Blighted Blossom in Temple Gardens;Collect `Blighted Petal`.|Blighted Blossom spawns only while this Bounty Contract is active. `Blighted Petal` drops only while this Contract is active.|350 XP;300 Gold;1x Holy Crystal;1x Enchantment Fragment.|


## World Tier 3 Repeatable Contracts


### Overgrown Trail (Earth)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-EOT-K01|Kill Contract|Moss Spider Hunt|Defeat 10 Moss Spider in Overgrown Trail.|None|400 XP;340 Gold;1x Crystal Shard.|
|R-EOT-K02|Kill Contract|Thorn Beast Hunt|Defeat 10 Thorn Beast in Overgrown Trail.|None|400 XP;340 Gold;1x Crystal Shard.|
|R-EOT-K03|Kill Contract|Fungus Hunt|Defeat 10 Fungus in Overgrown Trail.|None|400 XP;340 Gold;1x Crystal Shard.|
|R-EOT-C01|Collection Contract|Overgrown Trail Evidence|Collect 8 `Thorn Sap Sample` from eligible carrier mobs in Overgrown Trail.|`Thorn Sap Sample` drops from Moss Spider, Thorn Beast, Fungus only while this Contract is active.|510 XP;430 Gold;1x Crystal Shard.|
|R-EOT-B01|Unique Bounty|Webmother Nyss Bounty|Defeat Webmother Nyss in Overgrown Trail;Collect `Webmother Gland`.|Webmother Nyss spawns only while this Bounty Contract is active. `Webmother Gland` drops only while this Contract is active.|720 XP;610 Gold;1x Crystal Shard;1x Enchantment Crystal.|


### Bandit Camp (Air)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-ABC-K01|Kill Contract|Bandit Scout Hunt|Defeat 10 Bandit Scout in Bandit Camp.|None|400 XP;340 Gold;1x Magic Crystal.|
|R-ABC-K02|Kill Contract|Sand Raider Hunt|Defeat 10 Sand Raider in Bandit Camp.|None|400 XP;340 Gold;1x Magic Crystal.|
|R-ABC-K03|Kill Contract|Bandit Archer Hunt|Defeat 10 Bandit Archer in Bandit Camp.|None|400 XP;340 Gold;1x Magic Crystal.|
|R-ABC-K04|Kill Contract|Bandit Alchemist Hunt|Defeat 10 Bandit Alchemist in Bandit Camp.|None|400 XP;340 Gold;1x Magic Crystal.|
|R-ABC-C01|Collection Contract|Bandit Camp Evidence|Collect 8 `Bandit Supply Seal` from eligible carrier mobs in Bandit Camp.|`Bandit Supply Seal` drops from Bandit Scout, Sand Raider, Bandit Archer only while this Contract is active.|510 XP;430 Gold;1x Magic Crystal.|
|R-ABC-B01|Unique Bounty|Dune Captain Kharif Bounty|Defeat Dune Captain Kharif in Bandit Camp;Collect `Captain's Badge`.|Dune Captain Kharif spawns only while this Bounty Contract is active. `Captain's Badge` drops only while this Contract is active.|720 XP;610 Gold;1x Magic Crystal;1x Enchantment Crystal.|


### Echo Mine (Water)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-WEM-K01|Kill Contract|Crystal Beetle Hunt|Defeat 10 Crystal Beetle in Echo Mine.|None|400 XP;340 Gold;1x Crystal Shard.|
|R-WEM-K02|Kill Contract|Mine Wraith Hunt|Defeat 10 Mine Wraith in Echo Mine.|None|400 XP;340 Gold;1x Crystal Shard.|
|R-WEM-K03|Kill Contract|Stone Golem Hunt|Defeat 10 Stone Golem in Echo Mine.|None|400 XP;340 Gold;1x Crystal Shard.|
|R-WEM-C01|Collection Contract|Echo Mine Evidence|Collect 8 `Mine Claim Stamp` from eligible carrier mobs in Echo Mine.|`Mine Claim Stamp` drops from Crystal Beetle, Mine Wraith, Stone Golem only while this Contract is active.|510 XP;430 Gold;1x Crystal Shard.|
|R-WEM-B01|Unique Bounty|Quartzback Golem Bounty|Defeat Quartzback Golem in Echo Mine;Collect `Quartzback Core`.|Quartzback Golem spawns only while this Bounty Contract is active. `Quartzback Core` drops only while this Contract is active.|720 XP;610 Gold;1x Crystal Shard;1x Enchantment Crystal.|


### Lava Fissures (Fire)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-FLF-K01|Kill Contract|Flame Elemental Hunt|Defeat 10 Flame Elemental in Lava Fissures.|None|400 XP;340 Gold;1x Molten Core.|
|R-FLF-K02|Kill Contract|Cinder Witch Hunt|Defeat 10 Cinder Witch in Lava Fissures.|None|400 XP;340 Gold;1x Molten Core.|
|R-FLF-K03|Kill Contract|Fire Drake Hunt|Defeat 10 Fire Drake in Lava Fissures.|None|400 XP;340 Gold;1x Molten Core.|
|R-FLF-C01|Collection Contract|Lava Fissures Evidence|Collect 8 `Fissure Heat Sample` from eligible carrier mobs in Lava Fissures.|`Fissure Heat Sample` drops from Flame Elemental, Cinder Witch only while this Contract is active.|510 XP;430 Gold;1x Molten Core.|
|R-FLF-B01|Unique Bounty|Embermaw Lizard Bounty|Defeat Embermaw Lizard in Lava Fissures;Collect `Embermaw Fang`.|Embermaw Lizard spawns only while this Bounty Contract is active. `Embermaw Fang` drops only while this Contract is active.|720 XP;610 Gold;1x Molten Core;1x Enchantment Crystal.|


### Forgotten Crypt (Darkness)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DFC-K01|Kill Contract|Grave Wraith Hunt|Defeat 10 Grave Wraith in Forgotten Crypt.|None|400 XP;340 Gold;1x Dark Crystal.|
|R-DFC-K02|Kill Contract|Plague Mummy Hunt|Defeat 10 Plague Mummy in Forgotten Crypt.|None|400 XP;340 Gold;1x Dark Crystal.|
|R-DFC-K03|Kill Contract|Night Hag Hunt|Defeat 10 Night Hag in Forgotten Crypt.|None|400 XP;340 Gold;1x Dark Crystal.|
|R-DFC-C01|Collection Contract|Forgotten Crypt Evidence|Collect 8 `Crypt Seal Fragment` from eligible carrier mobs in Forgotten Crypt.|`Crypt Seal Fragment` drops from Grave Wraith, Plague Mummy only while this Contract is active.|510 XP;430 Gold;1x Dark Crystal.|
|R-DFC-B01|Unique Bounty|Gravebound Knight Arct Bounty|Defeat Gravebound Knight Arct in Forgotten Crypt;Collect `Gravebound Crest`.|Gravebound Knight Arct spawns only while this Bounty Contract is active. `Gravebound Crest` drops only while this Contract is active.|720 XP;610 Gold;1x Dark Crystal;1x Enchantment Crystal.|


### Sanctum Halls (Holy)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-HSH-K01|Kill Contract|Stone Guardian Hunt|Defeat 10 Stone Guardian in Sanctum Halls.|None|400 XP;340 Gold;1x Ancient Coin.|
|R-HSH-K02|Kill Contract|Sun Priest Hunt|Defeat 10 Sun Priest in Sanctum Halls.|None|400 XP;340 Gold;1x Ancient Coin.|
|R-HSH-K03|Kill Contract|Inquisitor Hunt|Defeat 10 Inquisitor in Sanctum Halls.|None|400 XP;340 Gold;1x Ancient Coin.|
|R-HSH-C01|Collection Contract|Sanctum Halls Evidence|Collect 8 `Sanctum Archive Seal` from eligible carrier mobs in Sanctum Halls.|`Sanctum Archive Seal` drops from Stone Guardian, Sun Priest only while this Contract is active.|510 XP;430 Gold;1x Ancient Coin.|
|R-HSH-B01|Unique Bounty|Veiled Inquisitor Sorn Bounty|Defeat Veiled Inquisitor Sorn in Sanctum Halls;Collect `Veiled Seal`.|Veiled Inquisitor Sorn spawns only while this Bounty Contract is active. `Veiled Seal` drops only while this Contract is active.|720 XP;610 Gold;1x Ancient Coin;1x Enchantment Crystal.|


## World Tier 4 Repeatable Contracts


### Deep Woods (Earth)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-EDW-K01|Kill Contract|Goblin Mage Hunt|Defeat 10 Goblin Mage in Deep Woods.|None|780 XP;660 Gold;1x Magic Crystal.|
|R-EDW-K02|Kill Contract|Treant Hunt|Defeat 10 Treant in Deep Woods.|None|780 XP;660 Gold;1x Magic Crystal.|
|R-EDW-K03|Kill Contract|Fungus Hunt|Defeat 10 Fungus in Deep Woods.|None|780 XP;660 Gold;1x Magic Crystal.|
|R-EDW-C01|Collection Contract|Deep Woods Evidence|Collect 8 `Grove Memory Shard` from eligible carrier mobs in Deep Woods.|`Grove Memory Shard` drops from Goblin Mage, Treant only while this Contract is active.|980 XP;830 Gold;1x Magic Crystal.|
|R-EDW-B01|Unique Bounty|Hollowroot Treant Bounty|Defeat Hollowroot Treant in Deep Woods;Collect `Hollowroot Bark`.|Hollowroot Treant spawns only while this Bounty Contract is active. `Hollowroot Bark` drops only while this Contract is active.|1,350 XP;1,150 Gold;1x Magic Crystal;1x Enchantment Crystal.|


### Ancient Ruins (Air)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-AAR-K01|Kill Contract|Sand Wraith Hunt|Defeat 10 Sand Wraith in Ancient Ruins.|None|780 XP;660 Gold;1x Air Crystal.|
|R-AAR-K02|Kill Contract|Desert Shaman Hunt|Defeat 10 Desert Shaman in Ancient Ruins.|None|780 XP;660 Gold;1x Air Crystal.|
|R-AAR-K03|Kill Contract|Mummy Hunt|Defeat 10 Mummy in Ancient Ruins.|None|780 XP;660 Gold;1x Air Crystal.|
|R-AAR-C01|Collection Contract|Ancient Ruins Evidence|Collect 8 `Observatory Gear Segment` from eligible carrier mobs in Ancient Ruins.|`Observatory Gear Segment` drops from Sand Wraith, Desert Shaman, Mummy only while this Contract is active.|980 XP;830 Gold;1x Air Crystal.|
|R-AAR-B01|Unique Bounty|Ashen Mummy Scribe Bounty|Defeat Ashen Mummy Scribe in Ancient Ruins;Collect `Scribe's Tablet`.|Ashen Mummy Scribe spawns only while this Bounty Contract is active. `Scribe's Tablet` drops only while this Contract is active.|1,350 XP;1,150 Gold;1x Air Crystal;1x Enchantment Crystal.|


### Ice Caves (Water)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-WIC-K01|Kill Contract|Frost Spider Hunt|Defeat 10 Frost Spider in Ice Caves.|None|780 XP;660 Gold;1x Frost Crystal.|
|R-WIC-K02|Kill Contract|Frost Mage Hunt|Defeat 10 Frost Mage in Ice Caves.|None|780 XP;660 Gold;1x Frost Crystal.|
|R-WIC-K03|Kill Contract|Ice Elemental Hunt|Defeat 10 Ice Elemental in Ice Caves.|None|780 XP;660 Gold;1x Frost Crystal.|
|R-WIC-C01|Collection Contract|Ice Caves Evidence|Collect 8 `Ice Cave Survey Chip` from eligible carrier mobs in Ice Caves.|`Ice Cave Survey Chip` drops from Frost Spider, Frost Mage only while this Contract is active.|980 XP;830 Gold;1x Frost Crystal.|
|R-WIC-B01|Unique Bounty|Icefang Matriarch Bounty|Defeat Icefang Matriarch in Ice Caves;Collect `Icefang Fang`.|Icefang Matriarch spawns only while this Bounty Contract is active. `Icefang Fang` drops only while this Contract is active.|1,350 XP;1,150 Gold;1x Frost Crystal;1x Enchantment Crystal.|


### Magma Forge (Fire)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-FMF-K01|Kill Contract|Molten Golem Hunt|Defeat 10 Molten Golem in Magma Forge.|None|780 XP;660 Gold;1x Molten Core.|
|R-FMF-K02|Kill Contract|Ember Wyrm Hunt|Defeat 10 Ember Wyrm in Magma Forge.|None|780 XP;660 Gold;1x Molten Core.|
|R-FMF-K03|Kill Contract|Fire Drake Hunt|Defeat 10 Fire Drake in Magma Forge.|None|780 XP;660 Gold;1x Molten Core.|
|R-FMF-C01|Collection Contract|Magma Forge Evidence|Collect 8 `Forge Calibration Plate` from eligible carrier mobs in Magma Forge.|`Forge Calibration Plate` drops from Molten Golem, Ember Wyrm only while this Contract is active.|980 XP;830 Gold;1x Molten Core.|
|R-FMF-B01|Unique Bounty|Forged Flame Sentinel Bounty|Defeat Forged Flame Sentinel in Magma Forge;Collect `Sentinel Core`.|Forged Flame Sentinel spawns only while this Bounty Contract is active. `Sentinel Core` drops only while this Contract is active.|1,350 XP;1,150 Gold;1x Molten Core;1x Enchantment Crystal.|


### Void Rift (Darkness)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DVR-K01|Kill Contract|Void Golem Hunt|Defeat 10 Void Golem in Void Rift.|None|780 XP;660 Gold;1x Dark Crystal.|
|R-DVR-K02|Kill Contract|Shadow Drake Hunt|Defeat 10 Shadow Drake in Void Rift.|None|780 XP;660 Gold;1x Dark Crystal.|
|R-DVR-K03|Kill Contract|Dread Knight Hunt|Defeat 10 Dread Knight in Void Rift.|None|780 XP;660 Gold;1x Dark Crystal.|
|R-DVR-C01|Collection Contract|Void Rift Evidence|Collect 8 `Rift Stabilizer Fragment` from eligible carrier mobs in Void Rift.|`Rift Stabilizer Fragment` drops from Void Golem, Shadow Drake only while this Contract is active.|980 XP;830 Gold;1x Dark Crystal.|
|R-DVR-B01|Unique Bounty|Riftbound Echo Bounty|Defeat Riftbound Echo in Void Rift;Collect `Rift Echo Shard`.|Riftbound Echo spawns only while this Bounty Contract is active. `Rift Echo Shard` drops only while this Contract is active.|1,350 XP;1,150 Gold;1x Dark Crystal;1x Enchantment Crystal.|


### Dawn Basilica (Holy)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-HDB-K01|Kill Contract|Dawn Seraph Hunt|Defeat 10 Dawn Seraph in Dawn Basilica.|None|780 XP;660 Gold;1x Holy Crystal.|
|R-HDB-K02|Kill Contract|Warden Hunt|Defeat 10 Warden in Dawn Basilica.|None|780 XP;660 Gold;1x Holy Crystal.|
|R-HDB-C01|Collection Contract|Dawn Basilica Evidence|Collect 8 `Basilica Ward Fragment` from eligible carrier mobs in Dawn Basilica.|`Basilica Ward Fragment` drops from Dawn Seraph, Warden only while this Contract is active.|980 XP;830 Gold;1x Holy Crystal.|
|R-HDB-B01|Unique Bounty|Fallen Seraph Amon Bounty|Defeat Fallen Seraph Amon in Dawn Basilica;Collect `Oath Feather`.|Fallen Seraph Amon spawns only while this Bounty Contract is active. `Oath Feather` drops only while this Contract is active.|1,350 XP;1,150 Gold;1x Holy Crystal;1x Enchantment Crystal.|


## World Tier 5 Repeatable Contracts


### King's Clearing (Earth)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-EKC-B01|Boss Challenge|Goblin King Challenge|Defeat Goblin King in King's Clearing;Collect `King's Crown Shard`.|`King's Crown Shard` drops from Goblin King only while this Challenge Contract is active. The Regional Sigil never drops again.|3,600 XP;3,050 Gold;1x Enchantment Fragment;1x Enchantment Crystal.|


### Ruin Guardian Chamber (Air)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-ARGC-B01|Boss Challenge|Ruin Guardian Challenge|Defeat Ruin Guardian in Ruin Guardian Chamber;Collect `Guardian Core Plate`.|`Guardian Core Plate` drops from Ruin Guardian only while this Challenge Contract is active. The Regional Sigil never drops again.|3,600 XP;3,050 Gold;1x Enchantment Fragment;1x Enchantment Crystal.|


### Frozen Peak (Water)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-WFP-K01|Kill Contract|Mountain Beast Hunt|Defeat 12 Mountain Beast in Frozen Peak.|None|1,300 XP;1,100 Gold;1x 1x Enchantment Fragment.|
|R-WFP-K02|Kill Contract|Harpy Hunt|Defeat 12 Harpy in Frozen Peak.|None|1,300 XP;1,100 Gold;1x 1x Enchantment Fragment.|
|R-WFP-C01|Collection Contract|Frozen Peak Evidence|Collect 10 `Peak Prayer Bead` from eligible carrier mobs in Frozen Peak.|`Peak Prayer Bead` drops from Mountain Beast, Harpy only while this Contract is active.|1,600 XP;1,350 Gold;1x Dragon Rune.|
|R-WFP-B01|Unique Bounty|Stormclaw Harpy Bounty|Defeat Stormclaw Harpy in Frozen Peak;Collect `Stormclaw Plume`.|Stormclaw Harpy spawns only while this Bounty Contract is active. `Stormclaw Plume` drops only while this Contract is active.|2,200 XP;1,850 Gold;1x Frost Crystal;1x Enchantment Crystal.|


### Inferno Core (Fire)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-FIC-B01|Boss Challenge|Inferno Lord Challenge|Defeat Inferno Lord in Inferno Core;Collect `Inferno Ember`.|`Inferno Ember` drops from Inferno Lord only while this Challenge Contract is active. The Regional Sigil never drops again.|3,600 XP;3,050 Gold;1x Obsidian Fragment;1x Enchantment Crystal.|


### Dread Throne (Darkness)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DDT-B01|Boss Challenge|Shadow Lord Challenge|Defeat Shadow Lord in Dread Throne;Collect `Dread Veil Fragment`.|`Dread Veil Fragment` drops from Shadow Lord only while this Challenge Contract is active. The Regional Sigil never drops again.|3,600 XP;3,050 Gold;1x Enchantment Crystal;1x Enchantment Crystal.|


### Oracle Chamber (Holy)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-HOC-B01|Boss Challenge|Oracle Challenge|Defeat Oracle in Oracle Chamber;Collect `Oracle's Trial Seal`.|`Oracle's Trial Seal` drops from Oracle only while this Challenge Contract is active. The Regional Sigil never drops again.|3,600 XP;3,050 Gold;1x Enchantment Crystal;1x Enchantment Crystal.|


## World Tier 6 Repeatable Contracts


### Summit Shrine (Water)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-WSS-B01|Boss Challenge|Frost Titan Challenge|Defeat Frost Titan in Summit Shrine;Collect `Titan Glacier Heart`.|`Titan Glacier Heart` drops from Frost Titan only while this Challenge Contract is active. The Regional Sigil never drops again.|3,600 XP;3,050 Gold;1x Frost Crystal;1x Enchantment Crystal.|


## Dragon Endgame Repeatable Contracts


### Dragon Valley (Dragon)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DRDV-K01|Kill Contract|Dragon Servant Hunt|Defeat 12 Dragon Servant in Dragon Valley.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DRDV-K02|Kill Contract|Dragon Whelp Hunt|Defeat 12 Dragon Whelp in Dragon Valley.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DRDV-C01|Collection Contract|Dragon Valley Evidence|Collect 10 `Dragonwatch Route Mark` from eligible carrier mobs in Dragon Valley.|`Dragonwatch Route Mark` drops from Dragon Servant, Dragon Whelp only while this Contract is active.|3,150 XP;2,700 Gold;1x Ancient Dragon Scale.|
|R-DRDV-B01|Unique Bounty|Redscale Whelp Bounty|Defeat Redscale Whelp in Dragon Valley;Collect `Redscale Horn`.|Redscale Whelp spawns only while this Bounty Contract is active. `Redscale Horn` drops only while this Contract is active.|4,300 XP;3,650 Gold;1x Dragon Rune;1x Enchantment Crystal.|


### Dragon Cave (Dragon)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DRDC-K01|Kill Contract|Wyvern Hunt|Defeat 12 Wyvern in Dragon Cave.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DRDC-K02|Kill Contract|Dragon Archer Hunt|Defeat 12 Dragon Archer in Dragon Cave.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DRDC-K03|Kill Contract|Bone Dragon Hunt|Defeat 12 Bone Dragon in Dragon Cave.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DRDC-C01|Collection Contract|Dragon Cave Evidence|Collect 10 `Cave Binding Fragment` from eligible carrier mobs in Dragon Cave.|`Cave Binding Fragment` drops from Wyvern, Dragon Archer only while this Contract is active.|3,150 XP;2,700 Gold;1x Ancient Dragon Scale.|
|R-DRDC-B01|Unique Bounty|Bonewing Remnant Bounty|Defeat Bonewing Remnant in Dragon Cave;Collect `Bonewing Scale`.|Bonewing Remnant spawns only while this Bounty Contract is active. `Bonewing Scale` drops only while this Contract is active.|4,300 XP;3,650 Gold;1x Dragon Rune;1x Enchantment Crystal.|


### Obsidian Citadel (Dragon)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DROC-K01|Kill Contract|Dragon Knight Hunt|Defeat 12 Dragon Knight in Obsidian Citadel.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DROC-K02|Kill Contract|Dragon Priest Hunt|Defeat 12 Dragon Priest in Obsidian Citadel.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DROC-K03|Kill Contract|Dragon Warlock Hunt|Defeat 12 Dragon Warlock in Obsidian Citadel.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DROC-K04|Kill Contract|Obsidian Guardian Hunt|Defeat 12 Obsidian Guardian in Obsidian Citadel.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DROC-C01|Collection Contract|Obsidian Citadel Evidence|Collect 10 `Citadel Armory Tag` from eligible carrier mobs in Obsidian Citadel.|`Citadel Armory Tag` drops from Dragon Knight, Dragon Priest, Dragon Warlock only while this Contract is active.|3,150 XP;2,700 Gold;1x Ancient Dragon Scale.|
|R-DROC-B01|Unique Bounty|Obsidian Warden Korr Bounty|Defeat Obsidian Warden Korr in Obsidian Citadel;Collect `Warden Command Sigil`.|Obsidian Warden Korr spawns only while this Bounty Contract is active. `Warden Command Sigil` drops only while this Contract is active.|4,300 XP;3,650 Gold;1x Ancient Dragon Scale;1x Enchantment Crystal.|


### Ancient Nest (Dragon)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DRAN-K01|Kill Contract|Dragon Knight Captain Hunt|Defeat 12 Dragon Knight Captain in Ancient Nest.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DRAN-K02|Kill Contract|Bone Dragon Hunt|Defeat 12 Bone Dragon in Ancient Nest.|None|2,650 XP;2,250 Gold;1x 1x Dragon Rune.|
|R-DRAN-C01|Collection Contract|Ancient Nest Evidence|Collect 10 `Nest Survey Fragment` from eligible carrier mobs in Ancient Nest.|`Nest Survey Fragment` drops from Dragon Knight Captain, Bone Dragon only while this Contract is active.|3,150 XP;2,700 Gold;1x Ancient Dragon Scale.|
|R-DRAN-B01|Boss Challenge|Ancient Dragon Challenge|Defeat Ancient Dragon in Ancient Nest;Collect `Ancient Dragon Memory Scale`.|`Ancient Dragon Memory Scale` drops from Ancient Dragon only while this Challenge Contract is active. The Regional Sigil never drops again.|4,300 XP;3,650 Gold;1x Ancient Dragon Scale;1x Ancient Dragon Fang;1x Dragon Rune or 1x Mythic Ember.|


### Dragon King's Lair (Dragon)


|ID|Type|Quest|Objectives|Conditional Quest Item / Spawn|Rewards|
|---|---|---|---|---|---|
|R-DRDKL-X01|No Repeatable Contract|Final Boss Exception|Dragon King is a one-time final Story Boss.|No Contract Item.|No reward after `S-DRAGON-05` beyond normal completion state.|


---

# Upgrade and Enchantment Material Sources


## Blacksmith Upgrade Materials


The Blacksmith uses Smithing Materials. These materials come from enemy drops,Area contracts,unique bounties,boss challenges,and Blacksmith salvage.


|Material|Used For|Primary Sources|Secondary Sources|Market Rule|
|---|---|---|---|---|
|Iron Scrap|+0 → +1 and +1 → +2|Tier 1 normal enemies;Tier 1 Kill Contracts;Blacksmith Salvage from Common equipment.|Forest Entrance through Sunlit Road outer Areas.|Sold by Market without limit at a high price.|
|Iron Ore|+1 → +2|Tier 2 normal enemies;Echo Mine;Tier 2 Contracts;Blacksmith Salvage from Uncommon equipment.|Bandit Camp;Goblin Forest;Mountain Pass.|Sold in limited stock after `S-T2-03`.|
|Crystal Shard|+2 → +3|Tier 3 normal and elite enemies;Echo Mine;Ice Caves;Tier 3 Contracts.|Blacksmith Salvage from Rare equipment;Regional Boss Challenges.|Sold in limited stock after `S-T3-03`.|
|Magic Crystal|+2 → +3|Magic and elemental enemies in Tier 3–4 Areas;Unique Bounties;Story rewards.|Blacksmith Salvage from Epic equipment;Boss Challenges.|Not sold normally.|
|Obsidian Fragment|+3 → +4|Lava Fissures;Magma Forge;Inferno Core;Fire Contracts.|Obsidian Citadel enemies;Blacksmith Salvage from Epic Fire equipment.|Not sold normally.|
|Molten Core|+3 → +4|Magma Forge Unique Bounty;Inferno Core Boss Challenge;high-tier Fire Contracts.|Rare reward from Molten Golem and Ember Wyrm loot tables.|Not sold normally.|
|Obsidian Core|+4 → +5|Obsidian Citadel Unique Bounty;Ancient Nest Contracts.|Rare Obsidian Guardian or Obsidian Warden Korr reward.|Not sold normally.|
|Ancient Dragon Scale|+4 → +5|Ancient Dragon repeatable Bounty after `S-DRAGON-04`.|Dragon endgame Contracts and selected Dragon rewards.|Not sold normally.|
|Ancient Dragon Fang|+4 → +5|Ancient Dragon repeatable Bounty after `S-DRAGON-04`.|Rare Ancient Dragon reward only.|Not sold normally.|

## Blacksmith Upgrade Requirements


|Upgrade|Success Chance|Required Materials|Gold Cost|
|---|---|---|---|
|+0 → +1|90%|3x Iron Scrap|50 Gold|
|+1 → +2|80%|2x Iron Scrap;2x Iron Ore|150 Gold|
|+2 → +3|65%|3x Crystal Shard;1x Magic Crystal|350 Gold|
|+3 → +4|45%|2x Obsidian Fragment;1x Molten Core|700 Gold|
|+4 → +5|25%|1x Ancient Dragon Scale;1x Ancient Dragon Fang;1x Obsidian Core|1,500 Gold|

## Blacksmith Salvage


|Equipment Grade|Blacksmith Salvage Result|Rule|
|---|---|---|
|Common|1–2x Iron Scrap|The Player chooses Salvage instead of selling.|
|Uncommon|1x Iron Ore;1x Iron Scrap|The Player chooses Salvage instead of selling.|
|Rare|1–2x Crystal Shard|The Player chooses Salvage instead of selling.|
|Epic|1x Magic Crystal or 1x Obsidian Fragment|The Player chooses Salvage instead of selling.|
|Legendary|1x Molten Core or 1x Obsidian Core|Only player-created Legendary gear can be salvaged.|
|Mythic|1x Obsidian Core;1x Ancient Dragon Scale|Only player-created Mythic gear can be salvaged.|

## Enchanter Grade Materials


The Enchanter uses Enchantment Materials. Their main source is disenchanting equipment. This gives dropped gear a purpose even when it is not equipped.


|Material|Used For|Primary Sources|Secondary Sources|Market Rule|
|---|---|---|---|---|
|Enchantment Dust|Common → Uncommon|Disenchant Common equipment;Tier 1 Unique Bounties;Tier 1 Contract rewards.|Rare low-tier Guild rewards.|Not sold.|
|Enchantment Fragment|Uncommon → Rare|Disenchant Uncommon equipment;Tier 2 Unique Bounties;Tier 3 Collection Contracts.|Regional Boss Challenge rewards.|Not sold.|
|Enchantment Crystal|Rare → Epic|Disenchant Rare or Epic equipment;Tier 3–5 Unique Bounties;Boss Challenges.|Late Guild reward bundles.|Not sold.|
|Dragon Rune|Epic → Legendary and Legendary → Mythic|Dragon Valley;Dragon Cave;Obsidian Citadel;Ancient Nest Contracts.|Regional World Tier 6 Boss Challenges;Ancient Dragon.|Not sold.|
|Ancient Dragon Scale|Epic → Legendary|Ancient Dragon repeatable Bounty.|Dragon endgame Contract reward.|Not sold.|
|Ancient Dragon Fang|Legendary → Mythic|Ancient Dragon repeatable Bounty.|Rare Ancient Dragon reward only.|Not sold.|
|Mythic Ember|Legendary → Mythic|Ancient Dragon repeatable Bounty.|Rare Ancient Dragon reward only.|Not sold.|

## Enchanter Grade Requirements


|Grade Upgrade|Success Chance|Required Materials|Gold Cost|
|---|---|---|---|
|Common → Uncommon|80%|2x Enchantment Dust|100 Gold|
|Uncommon → Rare|60%|2x Enchantment Fragment|300 Gold|
|Rare → Epic|40%|2x Enchantment Crystal|700 Gold|
|Epic → Legendary|20%|2x Dragon Rune;1x Ancient Dragon Scale|1,500 Gold|
|Legendary → Mythic|8%|3x Dragon Rune;1x Mythic Ember;1x Ancient Dragon Fang|3,000 Gold|

## Enchanter Disenchanting


|Equipment Grade|Disenchant Result|Rule|
|---|---|---|
|Common|1–2x Enchantment Dust|The Player chooses Disenchant instead of selling or Smithing Salvage.|
|Uncommon|1x Enchantment Fragment;1x Enchantment Dust|The Player chooses Disenchant instead of selling or Smithing Salvage.|
|Rare|1–2x Enchantment Crystal|The Player chooses Disenchant instead of selling or Smithing Salvage.|
|Epic|1x Enchantment Crystal;25% chance for 1x Dragon Rune|The Player chooses Disenchant instead of selling or Smithing Salvage.|
|Legendary|1x Dragon Rune;1x Ancient Dragon Scale|Only player-created Legendary gear can be disenchanted.|
|Mythic|2x Dragon Rune;1x Mythic Ember|Only player-created Mythic gear can be disenchanted.|

## Upgrade and Grade Rules


|Rule|Implementation|
|---|---|
|Independent Systems|Upgrade Level and Equipment Grade are separate values on every Equipment Item.|
|Failure|A failed Blacksmith or Enchanter attempt consumes listed Gold and Materials but never breaks or downgrades the Item.|
|Quest Items|Quest Items,Regional Sigils,and Dragon King's Seal cannot be upgraded,salvaged,or disenchanted.|
|Drop Limit|Legendary and Mythic equipment are never found as loot. They only exist through Enchanter upgrades.|

---

# Market


The Market sells basic recovery items,utility items,low-tier ingredients,and Backpack upgrades. It does not sell high-tier upgrade or enchantment materials.


## Market Functions


|Function|Description|
|---|---|
|Buy Consumables|Purchase basic recovery and status-removal items.|
|Buy Utility|Purchase Smoke Bombs and Recall Potions.|
|Buy Ingredients|Purchase basic potion ingredients and low-tier Smithing materials.|
|Sell Items|Sell sellable Equipment,Materials,and Consumables.|
|Upgrade Backpack|Buy permanent Backpack capacity upgrades from the Pack Merchant.|
|View Stock|Show effect,price,stock limit,and unlock condition before purchase.|

## Selling Rules


|Rule|Implementation|
|---|---|
|Standard Sell Value|Sell value is 25% of buy price,rounded down.|
|Equipment Sell Value|Sell value is 25% of the Equipment Base Value,rounded down.|
|Quest Items|Quest Items,Sigils,and special Story relics cannot be sold.|
|High-Tier Materials|High-tier materials can be sold but should normally be saved for upgrades.|
|Salvage Alternative|Before selling equipment,the Player may instead choose Blacksmith Salvage or Enchanter Disenchanting.|

## Always Available Stock


|Item|Category|Effect or Use|Buy Price|Stock|
|---|---|---|---|---|
|Small Health Potion|Consumable|Restore a small amount of HP.|25 Gold|Unlimited|
|Health Potion|Consumable|Restore a moderate amount of HP.|75 Gold|Unlimited|
|Small Mana Potion|Consumable|Restore a small amount of MP.|30 Gold|Unlimited|
|Mana Potion|Consumable|Restore a moderate amount of MP.|85 Gold|Unlimited|
|Antidote|Consumable|Remove Poison.|40 Gold|Unlimited|
|Bandage|Consumable|Remove Bleeding.|35 Gold|Unlimited|
|Empty Bottle|Crafting Utility|Required for most Potion recipes.|5 Gold|Unlimited|
|Smoke Bomb|Battle Utility|Attempt to escape a normal battle. Does not count as a Potion.|80 Gold|3 per restock|
|Recall Potion|Travel Utility|Return to Town outside battle. Does not count as a Potion.|150 Gold|2 per restock|
|Forest Herb|Ingredient|Basic healing ingredient.|12 Gold|Unlimited|
|Mana Mushroom|Ingredient|Basic mana ingredient.|18 Gold|Unlimited|
|Iron Scrap|Smithing Material|Low-tier Blacksmith material.|15 Gold|Unlimited|
|Redcap|Ingredient|Mid-tier healing ingredient.|25 Gold|10 per restock|
|Spider Silk|Ingredient|Bandage and utility ingredient.|30 Gold|10 per restock|
|Beast Claw|Ingredient|Strength and critical-related ingredient.|35 Gold|8 per restock|
|Cactus Sap|Ingredient|Healing and burn-related ingredient.|30 Gold|10 per restock|

## Progression Stock


|Unlock Condition|Item|Category|Effect or Use|Buy Price|Stock|
|---|---|---|---|---|---|
|Complete `S-T2-03`|Iron Ore|Smithing Material|Used for early Blacksmith upgrades.|50 Gold|5 per restock|
|Complete `S-T3-03`|Crystal Shard|Smithing Material|Used for mid Blacksmith upgrades.|85 Gold|3 per restock|
|Complete `S-T2-02`|Harpy Feather|Ingredient|Air,Precision,and Evasion recipes.|45 Gold|8 per restock|
|Complete `S-T2-02`|Desert Spirit Dust|Ingredient|Purifying recipes.|55 Gold|6 per restock|
|Complete `S-T3-02`|Air Crystal|Ingredient|Air resistance and utility recipes.|70 Gold|5 per restock|
|Complete `S-T2-03`|Ice Moss|Ingredient|Mana and Freeze-related recipes.|60 Gold|6 per restock|
|Complete `S-T4-03`|Frost Crystal|Ingredient|Water resistance and Awakening recipes.|80 Gold|5 per restock|
|Complete `S-T2-05`|Venom Sac|Ingredient|Antidote and Poison-related recipes.|65 Gold|6 per restock|
|Complete `S-T3-05`|Cursed Twig|Ingredient|Mind and Darkness-related recipes.|85 Gold|5 per restock|
|Complete `S-T3-06`|Ancient Coin|Ingredient|Precision and critical-related recipes.|120 Gold|4 per restock|
|Complete `S-T4-06`|Holy Crystal|Ingredient|Holy resistance and Purifying recipes.|150 Gold|3 per restock|

## Market Restrictions


|Item Category|Market Rule|
|---|---|
|Magic Crystal|Not sold normally. Obtain from magic and elemental enemies,contracts,bosses,or salvage.|
|Obsidian Fragment and Molten Core|Not sold normally. Obtain from Fire and endgame sources.|
|Enchantment Materials|Not sold. Obtain from disenchanting,contracts,unique bounties,and bosses.|
|Dragon Rune|Not sold. Obtain from World Tier 6 and Dragon content.|
|Ancient Dragon Scale,Fang,and Mythic Ember|Not sold. Obtain from Ancient Dragon repeatable content.|
|Legendary and Mythic Equipment|Never sold or dropped. Create through Enchanter upgrades.|
|Quest Items and Sigils|Never sold.|

---

# Alchemist


|Function|Description|
|---|---|
|Craft Potions|Create Potions from Ingredients and Empty Bottles.|
|View Recipes|Show unlocked Potion recipes and required materials.|
|Recipe Unlocks|Unlock stronger recipes through Regions,Quests,Bosses,and special discoveries.|
|Ingredient Check|Show owned and missing Ingredients before crafting.|
|Batch Crafting|Craft multiple copies when enough materials are available.|


|Rule|Implementation|
|---|---|
|Crafting Success|Potion crafting always succeeds.|
|Potion Drops|Craftable Potions do not normally drop from enemies. Ingredients drop instead.|
|Market Relationship|The Market sells basic emergency supplies. The Alchemist is the efficient long-term potion source.|
|Backpack|Crafted Potions use normal Backpack slots and stack to 99.|

---

# Blacksmith


|Function|Description|
|---|---|
|Upgrade Equipment|Upgrade one Equipment Item from `+0` to `+5`.|
|Preview Upgrade|Show current values,next values,success chance,materials,and Gold cost.|
|Smithing Salvage|Destroy an unwanted Equipment Item to obtain Smithing Materials.|
|Confirm Attempt|Confirm the Item before consuming Gold and Materials.|


|Rule|Implementation|
|---|---|
|Upgrade Target|Every Equipment Item tracks its own Upgrade Level.|
|Maximum Upgrade|The normal maximum is `+5`.|
|Failure Safety|Failure consumes requirements but never destroys or downgrades the Item.|
|Eligible Items|Weapons,Shields,Armor,and Accessories may be upgraded if the Item supports upgrades.|
|Quest Item Restriction|Quest Items,Sigils,and Dragon King's Seal cannot be upgraded or salvaged.|

---

# Enchanter


|Function|Description|
|---|---|
|Upgrade Equipment Grade|Increase one Equipment Item from Common to Mythic.|
|Preview Grade Upgrade|Show current Grade,next Grade,success chance,materials,and Gold cost.|
|Disenchant Equipment|Destroy an unwanted Equipment Item to obtain Enchantment Materials.|
|Confirm Attempt|Confirm the Item before consuming Gold and Materials.|


|Rule|Implementation|
|---|---|
|Grade Path|Common → Uncommon → Rare → Epic → Legendary → Mythic.|
|Drop Limit|Only Common through Epic can be found as equipment drops or quest equipment rewards.|
|Legendary and Mythic|Legendary and Mythic are player-created grades only.|
|Failure Safety|Failure consumes requirements but never destroys or downgrades the Item.|
|Quest Item Restriction|Quest Items,Sigils,and Dragon King's Seal cannot be enchanted or disenchanted.|

---

# Inn


The Inn is only a recovery location. It has no manual saving,loading,or dialogue function.


|Inn Function|Description|
|---|---|
|Restore HP|Restore the Player to maximum Health.|
|Restore MP|Restore the Player to maximum Mana.|
|Full Rest|Restore both HP and MP to maximum values.|
|Defeat Return|Serve as the default Town return location after defeat when applicable.|


|Rule|Implementation|
|---|---|
|Recovery Result|Full Rest restores HP and MP to maximum values.|
|Battle Effects|Battle-only Buffs,Debuffs,Barriers,and Status Effects do not persist outside combat.|
|Autosave|The game autosaves after Rest.|
|Cost|Recommended: Full Rest is free.|
|Defeat Penalty|Recommended: no Equipment loss and no Item destruction. Optionally lose a small amount of unspent Gold.|

---

# City Gate


|City Gate Function|Description|
|---|---|
|World Map|Show Regions,Areas,Story locks,and discovered Safe Areas.|
|Unlocked Areas|Allow direct travel to previously reached Safe Areas.|
|Area Entry|Enter the selected Area and begin exploration.|
|Return to Town|Return from allowed Areas through a Recall Potion,travel point,or map action.|
|Progress Lock|Hide or lock Areas until the next global Story Quest opens them.|


|Rule|Implementation|
|---|---|
|Global Tier Lock|The next Area opens according to the shared World Tier Order.|
|Farming Access|Every previously cleared Area remains available for farming and Repeatable Contracts.|
|Safe Travel|Direct travel is allowed only to discovered Safe Areas.|
|Boss Areas|Boss Arenas require the relevant World Tier 6 Story Quest or post-story Challenge Contract.|
|Dragon Region|Dragon King's Dominion unlocks only after all six Sigils and `S-DRAGON-00`.|
|Final Lair|Dragon King's Lair opens only during `S-DRAGON-05` and has no repeatable contract.|
|Autosave|The game saves after travel completes.|

---

# Player Menu


|Function|Description|
|---|---|
|Backpack|View normal Equipment,Consumables,Ingredients,and Materials.|
|Quest Items|View permanent relics,Sigils,and active Quest Items without using Backpack slots.|
|Equipment|Equip and unequip Weapons,Shields,Armor,and Accessories.|
|Equipment Comparison|Compare current equipment to selected equipment.|
|Character Stats|View Base Stats,Current Stats,Resistances,and Combat Attributes.|
|Skills|View Active Skills,Passive Skills,Mana Costs,and Cooldowns.|
|Quest Log|View Story Quests,Guild Quests,Repeatable Contracts,and objectives.|
|Bestiary|Optional record of encountered enemies,skills,drops,and element types.|

---

# Data Sheet Additions Register


These entries should later be added to the Quest Item,Enemy Data,Encounter Template,and Loot sheets.


## Story Quest Items


|Quest Item|Source Quest|Area|
|---|---|---|
|Wayfinder Compass|S-000|Town Archive|
|Surveyor Marker|S-T1-01|Forest Entrance|
|Caravan Ledger|S-T1-02|Desert Border|
|Frostbitten Locket|S-T1-03|Mountain Foothills|
|Cinder Scout Report|S-T1-04|Ashen Border|
|Lantern of Lost Names|S-T1-05|Gloomwood|
|Dawn Processional Bell|S-T1-06|Sunlit Road|
|Earthen Totem Shard|S-T2-01|Goblin Forest|
|Singing Sand Vial|S-T2-02|Scorching Dunes|
|Resonance Crystal|S-T2-03|Mountain Pass|
|Ember Collar|S-T2-04|Ember Fields|
|Marsh Hunter's Token|S-T2-05|Shadow Marsh|
|Sunroot Seed|S-T2-06|Temple Gardens|
|Thornheart Knot|S-T3-01|Overgrown Trail|
|Stormbound Standard|S-T3-02|Bandit Camp|
|Miner's Drill Key|S-T3-03|Echo Mine|
|Molten Pressure Valve|S-T3-04|Lava Fissures|
|Epitaph Seal|S-T3-05|Forgotten Crypt|
|Sanctum Cipher Plate|S-T3-06|Sanctum Halls|
|Ancient Sap Vial|S-T4-01|Deep Woods|
|Astral Lens|S-T4-02|Ancient Ruins|
|Frozen Star Chart|S-T4-03|Ice Caves|
|Forge Heart Key|S-T4-04|Magma Forge|
|Void Compass|S-T4-05|Void Rift|
|Oath Feather|S-T4-06|Dawn Basilica|
|Royal Clearing Key|S-T5-01|King's Clearing|
|Guardian Oath Plate|S-T5-02|Ruin Guardian Chamber|
|Shrine Prayer Cord|S-T5-03|Frozen Peak|
|Core Binding Chain|S-T5-04|Inferno Core|
|Veilbreaker Sigil|S-T5-05|Dread Throne|
|Dawn Trial Seal|S-T5-06|Oracle Chamber|
|Earth Sigil|S-T6-01|King's Clearing|
|Air Sigil|S-T6-02|Ruin Guardian Chamber|
|Water Sigil|S-T6-03|Summit Shrine|
|Fire Sigil|S-T6-04|Inferno Core|
|Darkness Sigil|S-T6-05|Dread Throne|
|Holy Sigil|S-T6-06|Oracle Chamber|
|Dominion Map|S-DRAGON-00|Town Archive|
|Dragonwatch Signal Horn|S-DRAGON-01|Dragon Valley|
|Ashen Draconic Tablet|S-DRAGON-02|Dragon Cave|
|Citadel Gate Sigil|S-DRAGON-03|Obsidian Citadel|
|Ancient Memory Scale|S-DRAGON-04|Ancient Nest|
|Dragon King's Seal|S-DRAGON-05|Dragon King's Lair|

## Repeatable Area Collection Items


|Quest Item|Contract|Area|Conditional Drop Rule|
|---|---|---|---|
|Trail Survey Tag|R-EFE-C01|Forest Entrance|Drops from: Forest Rat, Wild Boar only while Contract is active.|
|Caravan Wheel Seal|R-ADB-C01|Desert Border|Drops from: Desert Rat, Sand Beetle only while Contract is active.|
|Climber Route Flag|R-WMF-C01|Mountain Foothills|Drops from: Snow Wolf, Ice Bat only while Contract is active.|
|Evacuation Route Token|R-FAB-C01|Ashen Border|Drops from: Ash Lizard, Ember Hound only while Contract is active.|
|Pilgrim Name Strip|R-DG-C01|Gloomwood|Drops from: Shade, Bone Hound only while Contract is active.|
|Procession Ribbon|R-HSR-C01|Sunlit Road|Drops from: Sun Acolyte, Temple Squire only while Contract is active.|
|Goblin Patrol Token|R-EGF-C01|Goblin Forest|Drops from: Goblin Scout, Goblin Dagger, Goblin Archer only while Contract is active.|
|Singing Sand Packet|R-ASD-C01|Scorching Dunes|Drops from: Sand Scorpion, Vulture only while Contract is active.|
|Pass Supply Tag|R-WMP-C01|Mountain Pass|Drops from: Rock Crawler, Harpy only while Contract is active.|
|Heatproof Sample|R-FEF-C01|Ember Fields|Drops from: Lava Slime, Magma Beetle only while Contract is active.|
|Marsh Trail Marker|R-DSM-C01|Shadow Marsh|Drops from: Shadow Spider, Dark Wolf only while Contract is active.|
|Sunroot Pollen|R-HTG-C01|Temple Gardens|Drops from: Radiant Hawk, Light Sprite only while Contract is active.|
|Thorn Sap Sample|R-EOT-C01|Overgrown Trail|Drops from: Moss Spider, Thorn Beast, Fungus only while Contract is active.|
|Bandit Supply Seal|R-ABC-C01|Bandit Camp|Drops from: Bandit Scout, Sand Raider, Bandit Archer only while Contract is active.|
|Mine Claim Stamp|R-WEM-C01|Echo Mine|Drops from: Crystal Beetle, Mine Wraith, Stone Golem only while Contract is active.|
|Fissure Heat Sample|R-FLF-C01|Lava Fissures|Drops from: Flame Elemental, Cinder Witch only while Contract is active.|
|Crypt Seal Fragment|R-DFC-C01|Forgotten Crypt|Drops from: Grave Wraith, Plague Mummy only while Contract is active.|
|Sanctum Archive Seal|R-HSH-C01|Sanctum Halls|Drops from: Stone Guardian, Sun Priest only while Contract is active.|
|Grove Memory Shard|R-EDW-C01|Deep Woods|Drops from: Goblin Mage, Treant only while Contract is active.|
|Observatory Gear Segment|R-AAR-C01|Ancient Ruins|Drops from: Sand Wraith, Desert Shaman, Mummy only while Contract is active.|
|Ice Cave Survey Chip|R-WIC-C01|Ice Caves|Drops from: Frost Spider, Frost Mage only while Contract is active.|
|Forge Calibration Plate|R-FMF-C01|Magma Forge|Drops from: Molten Golem, Ember Wyrm only while Contract is active.|
|Rift Stabilizer Fragment|R-DVR-C01|Void Rift|Drops from: Void Golem, Shadow Drake only while Contract is active.|
|Basilica Ward Fragment|R-HDB-C01|Dawn Basilica|Drops from: Dawn Seraph, Warden only while Contract is active.|
|Peak Prayer Bead|R-WFP-C01|Frozen Peak|Drops from: Mountain Beast, Harpy only while Contract is active.|
|Dragonwatch Route Mark|R-DRDV-C01|Dragon Valley|Drops from: Dragon Servant, Dragon Whelp only while Contract is active.|
|Cave Binding Fragment|R-DRDC-C01|Dragon Cave|Drops from: Wyvern, Dragon Archer only while Contract is active.|
|Citadel Armory Tag|R-DROC-C01|Obsidian Citadel|Drops from: Dragon Knight, Dragon Priest, Dragon Warlock only while Contract is active.|
|Nest Survey Fragment|R-DRAN-C01|Ancient Nest|Drops from: Dragon Knight Captain, Bone Dragon only while Contract is active.|

## Story Unique Monsters

|Story Unique Monster|Source Quest|Area|Enemy Data Note|
|---|---|---|---|
|Totem-Bound Goblin|S-T2-01|Goblin Forest|Unique Goblin Shaman or Goblin Mage variant.|
|Glasswing Vulture|S-T2-02|Scorching Dunes|Unique Vulture variant. Also used as a repeatable Contract Unique.|
|Echo Stalker|S-T2-03|Mountain Pass|Unique Mine Wraith variant. Also used as a repeatable Contract Unique.|
|Ashfang Hound|S-T2-04|Ember Fields|Unique Ember Hound variant. Also used as a repeatable Contract Unique.|
|Bogshade Huntress|S-T2-05|Shadow Marsh|Unique Shadow Spider variant. Also used as a repeatable Contract Unique.|
|Blighted Blossom|S-T2-06|Temple Gardens|Unique Sacred Treant variant. Also used as a repeatable Contract Unique.|
|Thorn Matriarch|S-T3-01|Overgrown Trail|Unique Thorn Beast variant.|
|Icebound Scribe|S-T4-03|Ice Caves|Unique Frost Mage variant.|
|Forged Flame Sentinel|S-T4-04|Magma Forge|Unique Molten Golem variant. Also used as a repeatable Contract Unique.|
|Riftbound Echo|S-T4-05|Void Rift|Unique Void Golem variant. Also used as a repeatable Contract Unique.|
|Fallen Seraph Amon|S-T4-06|Dawn Basilica|Unique Dawn Seraph variant. Also used as a repeatable Contract Unique.|
|Obsidian Warden Korr|S-DRAGON-03|Obsidian Citadel|Unique Obsidian Guardian variant. Also used as a repeatable Contract Unique.|
|Ancient Dragon|S-DRAGON-04|Ancient Nest|Existing repeatable endgame Boss after Story completion.|
|Dragon King|S-DRAGON-05|Dragon King's Lair|One-time final Boss. Never repeatable.|

## Repeatable Unique Monsters and Bounty Proofs


|Unique Monster|Contract Type|Contract|Area|Enemy Data Note|Conditional Proof|
|---|---|---|---|---|---|
|Barkhide Boar|Unique Bounty|R-EFE-B01|Forest Entrance|Base: Wild Boar|Barkhide Tusk|
|Dustrunner Scarab|Unique Bounty|R-ADB-B01|Desert Border|Base: Sand Beetle|Dustrunner Carapace|
|Whitefang Alpha|Unique Bounty|R-WMF-B01|Mountain Foothills|Base: Snow Wolf|Whitefang Pelt|
|Ashfang Hound|Unique Bounty|R-FAB-B01|Ashen Border|Base: Ember Hound|Ashfang Collar|
|Lantern Shade|Unique Bounty|R-DG-B01|Gloomwood|Base: Shade|Lantern Wick|
|Sunwing Hawk|Unique Bounty|R-HSR-B01|Sunlit Road|Base: Radiant Hawk|Sunwing Feather|
|Boneknife Skulk|Unique Bounty|R-EGF-B01|Goblin Forest|Base: Goblin Dagger|Boneknife Insignia|
|Glasswing Vulture|Unique Bounty|R-ASD-B01|Scorching Dunes|Base: Vulture|Glasswing Feather|
|Echo Stalker|Unique Bounty|R-WMP-B01|Mountain Pass|Base: Mine Wraith|Echo Fragment|
|Magmaheart Slime|Unique Bounty|R-FEF-B01|Ember Fields|Base: Lava Slime|Magmaheart Core|
|Bogshade Huntress|Unique Bounty|R-DSM-B01|Shadow Marsh|Base: Shadow Spider|Bogshade Token|
|Blighted Blossom|Unique Bounty|R-HTG-B01|Temple Gardens|Base: Sacred Treant|Blighted Petal|
|Webmother Nyss|Unique Bounty|R-EOT-B01|Overgrown Trail|Base: Moss Spider|Webmother Gland|
|Dune Captain Kharif|Unique Bounty|R-ABC-B01|Bandit Camp|Base: Sand Raider|Captain's Badge|
|Quartzback Golem|Unique Bounty|R-WEM-B01|Echo Mine|Base: Stone Golem|Quartzback Core|
|Embermaw Lizard|Unique Bounty|R-FLF-B01|Lava Fissures|Base: Ash Lizard|Embermaw Fang|
|Gravebound Knight Arct|Unique Bounty|R-DFC-B01|Forgotten Crypt|Base: Dread Knight|Gravebound Crest|
|Veiled Inquisitor Sorn|Unique Bounty|R-HSH-B01|Sanctum Halls|Base: Inquisitor|Veiled Seal|
|Hollowroot Treant|Unique Bounty|R-EDW-B01|Deep Woods|Base: Treant|Hollowroot Bark|
|Ashen Mummy Scribe|Unique Bounty|R-AAR-B01|Ancient Ruins|Base: Mummy|Scribe's Tablet|
|Icefang Matriarch|Unique Bounty|R-WIC-B01|Ice Caves|Base: Frost Spider|Icefang Fang|
|Forged Flame Sentinel|Unique Bounty|R-FMF-B01|Magma Forge|Base: Molten Golem|Sentinel Core|
|Riftbound Echo|Unique Bounty|R-DVR-B01|Void Rift|Base: Void Golem|Rift Echo Shard|
|Fallen Seraph Amon|Unique Bounty|R-HDB-B01|Dawn Basilica|Base: Dawn Seraph|Oath Feather|
|Goblin King|Boss Challenge|R-EKC-B01|King's Clearing|Base: Goblin King|King's Crown Shard|
|Ruin Guardian|Boss Challenge|R-ARGC-B01|Ruin Guardian Chamber|Base: Ruin Guardian|Guardian Core Plate|
|Stormclaw Harpy|Unique Bounty|R-WFP-B01|Frozen Peak|Base: Harpy|Stormclaw Plume|
|Inferno Lord|Boss Challenge|R-FIC-B01|Inferno Core|Base: Inferno Lord|Inferno Ember|
|Shadow Lord|Boss Challenge|R-DDT-B01|Dread Throne|Base: Shadow Lord|Dread Veil Fragment|
|Oracle|Boss Challenge|R-HOC-B01|Oracle Chamber|Base: Oracle|Oracle's Trial Seal|
|Frost Titan|Boss Challenge|R-WSS-B01|Summit Shrine|Base: Frost Titan|Titan Glacier Heart|
|Redscale Whelp|Unique Bounty|R-DRDV-B01|Dragon Valley|Base: Dragon Whelp|Redscale Horn|
|Bonewing Remnant|Unique Bounty|R-DRDC-B01|Dragon Cave|Base: Bone Dragon|Bonewing Scale|
|Obsidian Warden Korr|Unique Bounty|R-DROC-B01|Obsidian Citadel|Base: Obsidian Guardian|Warden Command Sigil|
|Ancient Dragon|Boss Challenge|R-DRAN-B01|Ancient Nest|Base: Ancient Dragon|Ancient Dragon Memory Scale|

## Quest Equipment Rewards


|Item|Source|Grade|Suggested Purpose|
|---|---|---|---|
|Thornward Ring|S-T3-01|Rare|Earth Resistance and Poison Resistance.|
|Dune Watcher's Charm|S-T3-02|Rare|Accuracy and Air Resistance.|
|Echo Miner Pendant|S-T4-03|Rare|Magical Defense and Freeze Resistance.|
|Forgehand Bracer|S-T4-04|Epic|Physical Attack and Fire Resistance.|
|Mourning Veil|S-T4-05|Epic|Darkness Resistance and Magic Power.|
|Dawnkeeper Brooch|S-T4-06|Epic|Holy Resistance and Healing Received.|
|Dragonwatch Band|S-DRAGON-03|Epic|Defense,Magical Defense,and a Dragon-related resistance if implemented.|

---

# Recommended Core Gameplay Loop


```text
1. Check the current global Story Quest.
2. Accept the next Story Quest from its named NPC.
3. Optionally choose one Repeatable Contract from the Guild Board.
4. Buy basic supplies or a Backpack upgrade at the Market.
5. Craft Potions at the Alchemist.
6. Upgrade or salvage Equipment at the Blacksmith.
7. Enchant or disenchant Equipment at the Enchanter.
8. Rest at the Inn.
9. Travel through the City Gate to the current Story Area or a previous farming Area.
10. Complete Story objectives,Contracts,and Bounties.
11. Return to Town,claim rewards,and continue to the next global Story step.
```

---

## Documentation Links

This preserved source is retained in full. The canonical integrated design is in
[09_Town_Quests_and_Contracts.md](09_Town_Quests_and_Contracts.md); the documentation index is [00_README.md](00_README.md).
Where this source conflicts with newer documents, see
[16_Consistency_Audit.md](16_Consistency_Audit.md) rather than deleting this record.

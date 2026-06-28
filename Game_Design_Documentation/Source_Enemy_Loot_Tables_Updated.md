# Enemy and Loot Tables

This document replaces the previous region enemy and loot tables. It includes the Story Uniques,Repeatable Contract Uniques,Conditional Quest Items,and Boss Challenge Proofs introduced by the Town System.

## Global Loot Rules

|Rule|Implementation|
|---|---|
|Normal Equipment Drop Cap|Normal Enemies can drop Common,Uncommon,or Rare Equipment.|
|Elite,Unique,and Boss Equipment Drop Cap|Elites,Story Uniques,Contract Uniques,and Regional Bosses can drop up to Epic Equipment.|
|Legendary and Mythic|Legendary and Mythic Equipment never drop. They are created only through Enchanter Grade Upgrades.|
|Craftable Potions|Craftable Potions do not normally drop from Enemies. Enemies drop Ingredients and Materials instead.|
|Quest Item Rule|Every Story Item,Collection Item,Bounty Proof,and Boss Challenge Proof exists only while its exact linked Quest or Contract is active.|
|Quest Item Inventory|Quest Items use the separate Quest Item inventory and consume 0 Backpack slots.|
|Quest Item Safety|Quest Items cannot be sold,discarded,upgraded,salvaged,or disenchanted.|
|Duplicate Protection|A conditional Quest Item stops dropping as soon as its linked objective is complete.|
|Dragon King|The Dragon King drops only the `Dragon King's Seal` during `S-DRAGON-05`. It drops no Gold,Equipment,Materials,or Potions.|
|Regional Sigils|Each Regional Sigil drops once during its linked Story Boss Quest. Repeatable Boss Challenges never drop Sigils.|

## Conditional Quest Drop Resolution

```text
1. Enemy is defeated or a fixed interaction is used.
2. Check whether a linked Story Quest or Repeatable Contract is active.
3. Check whether the linked objective still needs this Quest Item.
4. If both checks are true,grant exactly 1 listed Quest Item.
5. If either check is false,the Quest Item does not exist in the loot result.
6. Resolve normal Material,Gold,and Equipment loot separately.
```

## Upgrade and Enchantment Material Loot Sources

|Material|Primary Enemy Sources|Additional Sources|Drop Rule|
|---|---|---|---|
|Iron Scrap|Forest Rat,Wild Boar,Goblin Scout,Goblin Dagger|Early contracts;Common and Uncommon Equipment Salvage|Early Smithing Material.|
|Iron Ore|Goblin Shaman,Sand Beetle,Rock Crawler,Stone Golem|Tier 2 contracts;Uncommon/Rare Equipment Salvage|Mid Smithing Material.|
|Crystal Shard|Crystal Beetle,Mine Wraith,Thorn Beast,Stone Guardian|Tier 3 contracts;Rare/Epic Equipment Salvage|Mid Smithing Material.|
|Magic Crystal|Goblin Mage,Desert Shaman,Frost Mage,Sun Priest|Story rewards;Elite encounters;Epic Equipment Salvage|Mid Smithing Material.|
|Obsidian Fragment|Lava Slime,Magma Beetle,Molten Golem,Dragon Knight|Fire and Dragon contracts|Late Smithing Material.|
|Molten Core|Fire Drake,Ember Wyrm,Molten Golem,Inferno Lord Challenge|Fire Unique Bounties|Late Smithing Material.|
|Obsidian Core|Obsidian Guardian,Obsidian Warden Korr|Rare Dominion Bounty reward|Late Smithing Material;not sold normally.|
|Enchantment Dust|Contract Unique rewards;Common/Uncommon Equipment Disenchanting|Early repeatable contracts|Enchanter Material.|
|Enchantment Fragment|Tier 2-5 Unique Bounties;Rare Equipment Disenchanting|Regional contracts|Enchanter Material.|
|Enchantment Crystal|Tier 3+ Unique Bounties,Boss Challenges;Epic Equipment Disenchanting|Regional Boss Challenges|Enchanter Material.|
|Dragon Rune|Dragon content;Ancient Dragon;late Boss Challenges|Dragon contracts|Late Enchanter Material.|
|Ancient Dragon Scale|Ancient Dragon|Ancient Nest collection contract reward|Required for Legendary and Mythic Enchanting.|
|Ancient Dragon Fang|Ancient Dragon|Ancient Nest rewards|Required for Mythic Enchanting.|
|Mythic Ember|Ancient Dragon|Very rare Ancient Nest reward|Required for Mythic Enchanting.|

---

# Earth Region

Primary Element: Earth

## Areas

|Order|Area|
|---|---|
|1|Forest Entrance|
|2|Goblin Forest|
|3|Overgrown Trail|
|4|Deep Woods|
|5|King's Clearing|

## Enemies and Loot

|Enemy|Area|Rank|Element Types|Combat Role|Standard Loot|Conditional Quest Loot|
|---|---|---|---|---|---|---|
|Forest Rat|Forest Entrance|Normal|Earth|Fast physical attacker|Forest Herb;Iron Scrap;Common-Uncommon Equipment;Gold|`Trail Survey Tag` during `R-EFE-C01` only.|
|Wild Boar|Forest Entrance|Normal|Earth|Durable physical attacker|Beast Claw;Forest Herb;Common-Uncommon Equipment;Gold|`Trail Survey Tag` during `R-EFE-C01` only.|
|Barkhide Boar|Forest Entrance|Contract Unique|Earth|Wild Boar variant with Fortify|Beast Claw;Iron Scrap;Equipment up to Epic;Gold|Spawns only during `R-EFE-B01`;drops `Barkhide Tusk`.|
|Goblin Scout|Goblin Forest|Normal|Earth|Fast physical attacker|Forest Herb;Iron Scrap;Common-Rare Equipment;Gold|`Goblin Patrol Token` during `R-EGF-C01` only.|
|Goblin Dagger|Goblin Forest|Normal|Earth|Physical Bleeding attacker|Beast Claw;Iron Scrap;Common-Rare Equipment;Gold|`Goblin Patrol Token` during `R-EGF-C01` only.|
|Goblin Archer|Goblin Forest|Normal|Air|Ranged Blind attacker|Harpy Feather;Iron Scrap;Common-Rare Equipment;Gold|`Goblin Patrol Token` during `R-EGF-C01` only.|
|Goblin Shaman|Goblin Forest|Elite|Earth,Darkness|Support and control caster|Iron Ore;Mana Mushroom;Magic Crystal;Equipment up to Epic;Gold|None.|
|Totem-Bound Goblin|Goblin Forest|Story Unique|Earth,Darkness|Goblin Shaman or Goblin Mage variant|Iron Ore;Magic Crystal;Equipment up to Epic;Gold|Spawns only during `S-T2-01`;drops `Earthen Totem Shard`.|
|Boneknife Skulk|Goblin Forest|Contract Unique|Earth|Goblin Dagger variant|Iron Ore;Beast Claw;Equipment up to Epic;Gold|Spawns only during `R-EGF-B01`;drops `Boneknife Insignia`.|
|Moss Spider|Overgrown Trail|Normal|Earth|Poison and Rooted controller|Spider Silk;Venom Sac;Common-Rare Equipment;Gold|`Thorn Sap Sample` during `R-EOT-C01` only.|
|Thorn Beast|Overgrown Trail|Normal|Earth|Defensive physical attacker|Forest Herb;Beast Claw;Crystal Shard;Common-Rare Equipment;Gold|`Thorn Sap Sample` during `R-EOT-C01` only.|
|Fungus|Overgrown Trail|Normal|Earth,Darkness|Poison and Magic controller|Mana Mushroom;Redcap;Cursed Twig;Common-Rare Equipment;Gold|`Thorn Sap Sample` during `R-EOT-C01` only.|
|Thorn Matriarch|Overgrown Trail|Story Unique|Earth|Thorn Beast variant with Stun|Spider Silk;Stone Core;Equipment up to Epic;Gold|Spawns only during `S-T3-01`;drops `Thornheart Knot`.|
|Webmother Nyss|Overgrown Trail|Contract Unique|Earth,Darkness|Moss Spider variant with Poison|Spider Silk;Venom Sac;Equipment up to Epic;Gold|Spawns only during `R-EOT-B01`;drops `Webmother Gland`.|
|Goblin Mage|Deep Woods|Elite|Earth|Earth magic and Rooted controller|Magic Crystal;Mana Mushroom;Equipment up to Epic;Gold|`Grove Memory Shard` during `R-EDW-C01` only.|
|Treant|Deep Woods|Elite|Earth|Fortify and Regeneration defender|Forest Herb;Stone Core;Crystal Shard;Equipment up to Epic;Gold|`Grove Memory Shard` during `R-EDW-C01` only.|
|Hollowroot Treant|Deep Woods|Contract Unique|Earth,Darkness|Treant variant with stronger Barrier|Stone Core;Magic Crystal;Equipment up to Epic;Gold|Spawns only during `R-EDW-B01`;drops `Hollowroot Bark`.|
|Goblin King|King's Clearing|Regional Boss|Earth|Summoning physical and Earth boss|Crystal Shard;Magic Crystal;Equipment up to Epic;Gold|Drops `Earth Sigil` during `S-T6-01`;drops `King's Crown Shard` only during `R-EKC-B01`.|

---

# Air Region

Primary Element: Air

## Areas

|Order|Area|
|---|---|
|1|Desert Border|
|2|Scorching Dunes|
|3|Bandit Camp|
|4|Ancient Ruins|
|5|Ruin Guardian Chamber|

## Enemies and Loot

|Enemy|Area|Rank|Element Types|Combat Role|Standard Loot|Conditional Quest Loot|
|---|---|---|---|---|---|---|
|Desert Rat|Desert Border|Normal|Air|Fast physical attacker|Cactus Sap;Common-Uncommon Equipment;Gold|`Caravan Wheel Seal` during `R-ADB-C01` only.|
|Sand Beetle|Desert Border|Normal|Earth|Defensive physical enemy|Iron Ore;Beetle Shell;Common-Uncommon Equipment;Gold|`Caravan Wheel Seal` during `R-ADB-C01` only.|
|Dustrunner Scarab|Desert Border|Contract Unique|Earth,Air|Sand Beetle variant with Haste|Iron Ore;Air Crystal;Equipment up to Epic;Gold|Spawns only during `R-ADB-B01`;drops `Dustrunner Carapace`.|
|Sand Scorpion|Scorching Dunes|Normal|Earth|Poison and Rooted attacker|Venom Sac;Scorpion Tail;Common-Rare Equipment;Gold|`Singing Sand Packet` during `R-ASD-C01` only.|
|Vulture|Scorching Dunes|Normal|Air|Blind and fast ranged attacker|Harpy Feather;Air Crystal;Common-Rare Equipment;Gold|`Singing Sand Packet` during `R-ASD-C01` only.|
|Glasswing Vulture|Scorching Dunes|Story/Contract Unique|Air|Vulture variant with stronger Blind|Harpy Feather;Air Crystal;Equipment up to Epic;Gold|During `S-T2-02`,drops `Singing Sand Vial`;during `R-ASD-B01`,spawns as Bounty and drops `Glasswing Feather`.|
|Bandit Scout|Bandit Camp|Normal|Air|Fast physical attacker|Iron Ore;Tattered Cloth;Common-Rare Equipment;Gold|`Bandit Supply Seal` during `R-ABC-C01` only.|
|Sand Raider|Bandit Camp|Normal|Air|Berserk physical attacker|Iron Ore;Beast Claw;Common-Rare Equipment;Gold|`Bandit Supply Seal` during `R-ABC-C01` only.|
|Bandit Archer|Bandit Camp|Normal|Air|Pinning and Piercing ranged attacker|Harpy Feather;Iron Ore;Common-Rare Equipment;Gold|`Bandit Supply Seal` during `R-ABC-C01` only.|
|Bandit Alchemist|Bandit Camp|Elite|Fire,Air|Poison,Blind,and Fire caster|Cactus Sap;Magic Crystal;Equipment up to Epic;Gold|None.|
|Dune Captain Kharif|Bandit Camp|Contract Unique|Air|Sand Raider leader with Armor Break|Iron Ore;Air Crystal;Equipment up to Epic;Gold|Spawns only during `R-ABC-B01`;drops `Captain's Badge`.|
|Sand Wraith|Ancient Ruins|Elite|Darkness,Air|Fear and Blind magic attacker|Desert Spirit Dust;Dark Crystal;Equipment up to Epic;Gold|`Observatory Gear Segment` during `R-AAR-C01` only.|
|Desert Shaman|Ancient Ruins|Elite|Air,Holy|Barrier,Heal,and Gale caster|Air Crystal;Magic Crystal;Equipment up to Epic;Gold|`Observatory Gear Segment` during `R-AAR-C01` only.|
|Mummy|Ancient Ruins|Elite|Darkness|Poison and Curse attacker|Ancient Coin;Cursed Twig;Equipment up to Epic;Gold|`Observatory Gear Segment` during `R-AAR-C01` only.|
|Ashen Mummy Scribe|Ancient Ruins|Contract Unique|Darkness,Air|Mummy variant with Dust Veil|Ancient Coin;Magic Crystal;Equipment up to Epic;Gold|Spawns only during `R-AAR-B01`;drops `Scribe's Tablet`.|
|Ruin Guardian|Ruin Guardian Chamber|Regional Boss|Air,Earth,Holy|Barrier and Stun construct boss|Air Crystal;Crystal Shard;Equipment up to Epic;Gold|Drops `Air Sigil` during `S-T6-02`;drops `Guardian Core Plate` only during `R-ARGC-B01`.|

---

# Water Region

Primary Element: Water

## Areas

|Order|Area|
|---|---|
|1|Mountain Foothills|
|2|Mountain Pass|
|3|Echo Mine|
|4|Ice Caves|
|5|Frozen Peak|
|6|Summit Shrine|

## Enemies and Loot

|Enemy|Area|Rank|Element Types|Combat Role|Standard Loot|Conditional Quest Loot|
|---|---|---|---|---|---|---|
|Snow Wolf|Mountain Foothills|Normal|Water|Haste and Bleeding physical attacker|Ice Moss;Beast Claw;Common-Uncommon Equipment;Gold|`Climber Route Flag` during `R-WMF-C01` only.|
|Ice Bat|Mountain Foothills|Normal|Water,Air|Blind and Frost attacker|Frost Crystal;Ice Moss;Common-Uncommon Equipment;Gold|`Climber Route Flag` during `R-WMF-C01` only.|
|Whitefang Alpha|Mountain Foothills|Contract Unique|Water|Snow Wolf variant with stronger Bleeding|Ice Moss;Beast Claw;Equipment up to Epic;Gold|Spawns only during `R-WMF-B01`;drops `Whitefang Pelt`.|
|Rock Crawler|Mountain Pass|Normal|Earth|High Defense physical attacker|Iron Ore;Stone Core;Common-Rare Equipment;Gold|`Pass Supply Tag` during `R-WMP-C01` only.|
|Harpy|Mountain Pass|Normal|Air|Gale and Blind attacker|Harpy Feather;Air Crystal;Common-Rare Equipment;Gold|`Pass Supply Tag` during `R-WMP-C01` only.|
|Echo Stalker|Mountain Pass|Story/Contract Unique|Darkness,Water|Mine Wraith variant with Fear|Crystal Shard;Dark Crystal;Equipment up to Epic;Gold|During `S-T2-03`,drops `Resonance Crystal`;during `R-WMP-B01`,spawns as Bounty and drops `Echo Fragment`.|
|Crystal Beetle|Echo Mine|Normal|Earth,Water|High Magical Defense enemy|Crystal Shard;Iron Ore;Common-Rare Equipment;Gold|`Mine Claim Stamp` during `R-WEM-C01` only.|
|Mine Wraith|Echo Mine|Normal|Darkness|Fear and Soul Rend caster|Dark Crystal;Crystal Shard;Common-Rare Equipment;Gold|`Mine Claim Stamp` during `R-WEM-C01` only.|
|Stone Golem|Echo Mine|Normal|Earth|High Defense Stun attacker|Stone Core;Iron Ore;Common-Rare Equipment;Gold|`Mine Claim Stamp` during `R-WEM-C01` only.|
|Quartzback Golem|Echo Mine|Contract Unique|Earth,Water|Stone Golem variant with Barrier|Stone Core;Crystal Shard;Equipment up to Epic;Gold|Spawns only during `R-WEM-B01`;drops `Quartzback Core`.|
|Frost Spider|Ice Caves|Normal|Water,Earth|Rooted,Freeze,and Poison attacker|Spider Silk;Venom Sac;Frost Crystal;Common-Rare Equipment;Gold|`Ice Cave Survey Chip` during `R-WIC-C01` only.|
|Frost Mage|Ice Caves|Normal|Water|Freeze and Barrier caster|Frost Crystal;Magic Crystal;Common-Rare Equipment;Gold|`Ice Cave Survey Chip` during `R-WIC-C01` only.|
|Ice Elemental|Ice Caves|Elite|Water|Wet and Freeze magic attacker|Ice Moss;Frost Crystal;Equipment up to Epic;Gold|None.|
|Icebound Scribe|Ice Caves|Story Unique|Water|Frost Mage variant with Frozen Prison|Frost Crystal;Magic Crystal;Equipment up to Epic;Gold|Spawns only during `S-T4-03`;drops `Frozen Star Chart`.|
|Icefang Matriarch|Ice Caves|Contract Unique|Water,Earth|Frost Spider variant with strong Poison|Spider Silk;Frost Crystal;Equipment up to Epic;Gold|Spawns only during `R-WIC-B01`;drops `Icefang Fang`.|
|Mountain Beast|Frozen Peak|Normal|Earth,Water|Heavy physical attacker|Mountain Beast Claw;Beast Claw;Common-Rare Equipment;Gold|`Peak Prayer Bead` during `R-WFP-C01` only.|
|Stormclaw Harpy|Frozen Peak|Contract Unique|Air,Water|Harpy variant with Winded and Haste|Harpy Feather;Frost Crystal;Equipment up to Epic;Gold|Spawns only during `R-WFP-B01`;drops `Stormclaw Plume`.|
|Frost Titan|Summit Shrine|Regional Boss|Water,Earth|Freeze,Slow,and Stun boss|Frost Crystal;Magic Crystal;Equipment up to Epic;Gold|Drops `Water Sigil` during `S-T6-03`;drops `Titan Glacier Heart` only during `R-WSS-B01`.|

---

# Fire Region

Primary Element: Fire

## Areas

|Order|Area|
|---|---|
|1|Ashen Border|
|2|Ember Fields|
|3|Lava Fissures|
|4|Magma Forge|
|5|Inferno Core|

## Enemies and Loot

|Enemy|Area|Rank|Element Types|Combat Role|Standard Loot|Conditional Quest Loot|
|---|---|---|---|---|---|---|
|Ash Lizard|Ashen Border|Normal|Fire|Fast Burn attacker|Ember Core;Beast Claw;Common-Uncommon Equipment;Gold|`Evacuation Route Token` during `R-FAB-C01` only.|
|Ember Hound|Ashen Border|Normal|Fire|Haste physical attacker|Ember Core;Beast Claw;Common-Uncommon Equipment;Gold|`Evacuation Route Token` during `R-FAB-C01` only.|
|Ashfang Hound|Ashen Border / Ember Fields|Story/Contract Unique|Fire|Ember Hound variant with Burn and Haste|Ember Core;Beast Claw;Equipment up to Epic;Gold|During `S-T2-04` in Ember Fields,drops `Ember Collar`;during `R-FAB-B01` in Ashen Border,spawns as Bounty and drops `Ashfang Collar`.|
|Lava Slime|Ember Fields|Normal|Fire|Barrier and Fire caster|Obsidian Fragment;Ember Core;Common-Rare Equipment;Gold|`Heatproof Sample` during `R-FEF-C01` only.|
|Magma Beetle|Ember Fields|Normal|Fire,Earth|Defensive Fire attacker|Obsidian Fragment;Iron Ore;Common-Rare Equipment;Gold|`Heatproof Sample` during `R-FEF-C01` only.|
|Ash Cultist|Ember Fields|Normal|Fire,Darkness|Focus and Fire/Darkness caster|Ember Core;Cursed Twig;Common-Rare Equipment;Gold|None.|
|Magmaheart Slime|Ember Fields|Contract Unique|Fire|Lava Slime variant with stronger Barrier|Obsidian Fragment;Ember Core;Equipment up to Epic;Gold|Spawns only during `R-FEF-B01`;drops `Magmaheart Core`.|
|Flame Elemental|Lava Fissures|Normal|Fire|Fire Bolt and Flame Wave caster|Molten Core;Ember Core;Common-Rare Equipment;Gold|`Fissure Heat Sample` during `R-FLF-C01` only.|
|Cinder Witch|Lava Fissures|Normal|Fire,Darkness|Confusion and Fire caster|Molten Core;Dark Crystal;Common-Rare Equipment;Gold|`Fissure Heat Sample` during `R-FLF-C01` only.|
|Fire Drake|Lava Fissures|Normal|Fire,Air|Burn and Winded attacker|Molten Core;Ember Core;Common-Rare Equipment;Gold|None.|
|Embermaw Lizard|Lava Fissures|Contract Unique|Fire|Ash Lizard variant with Charge|Molten Core;Beast Claw;Equipment up to Epic;Gold|Spawns only during `R-FLF-B01`;drops `Embermaw Fang`.|
|Molten Golem|Magma Forge|Elite|Fire,Earth|High Defense Fire construct|Molten Core;Obsidian Fragment;Equipment up to Epic;Gold|`Forge Calibration Plate` during `R-FMF-C01` only.|
|Ember Wyrm|Magma Forge|Elite|Fire|Charge and Flame Wave attacker|Molten Core;Ember Core;Equipment up to Epic;Gold|`Forge Calibration Plate` during `R-FMF-C01` only.|
|Forged Flame Sentinel|Magma Forge|Story/Contract Unique|Fire,Earth|Molten Golem variant with Flame Wave|Molten Core;Obsidian Fragment;Equipment up to Epic;Gold|During `S-T4-04`,drops `Forge Heart Key`;during `R-FMF-B01`,spawns as Bounty and drops `Sentinel Core`.|
|Inferno Lord|Inferno Core|Regional Boss|Fire,Darkness|Summoning Fire boss with Infernal Nova|Molten Core;Obsidian Fragment;Equipment up to Epic;Gold|Drops `Fire Sigil` during `S-T6-04`;drops `Inferno Ember` only during `R-FIC-B01`.|

---

# Darkness Region

Primary Element: Darkness

## Areas

|Order|Area|
|---|---|
|1|Gloomwood|
|2|Shadow Marsh|
|3|Forgotten Crypt|
|4|Void Rift|
|5|Dread Throne|

## Enemies and Loot

|Enemy|Area|Rank|Element Types|Combat Role|Standard Loot|Conditional Quest Loot|
|---|---|---|---|---|---|---|
|Shade|Gloomwood|Normal|Darkness|Fast Darkness caster|Cursed Twig;Mana Mushroom;Common-Uncommon Equipment;Gold|`Pilgrim Name Strip` during `R-DG-C01` only.|
|Bone Hound|Gloomwood|Normal|Darkness|Fear and Bleeding attacker|Beast Claw;Cursed Twig;Common-Uncommon Equipment;Gold|`Pilgrim Name Strip` during `R-DG-C01` only.|
|Lantern Shade|Gloomwood|Contract Unique|Darkness|Shade variant with Curse|Cursed Twig;Dark Crystal;Equipment up to Epic;Gold|Spawns only during `R-DG-B01`;drops `Lantern Wick`.|
|Shadow Spider|Shadow Marsh|Normal|Darkness|Rooted,Poison,and Shadow Mark attacker|Venom Sac;Spider Silk;Common-Rare Equipment;Gold|`Marsh Trail Marker` during `R-DSM-C01` only.|
|Dark Wolf|Shadow Marsh|Normal|Darkness|Fear,Haste,and Bleeding attacker|Beast Claw;Dark Crystal;Common-Rare Equipment;Gold|`Marsh Trail Marker` during `R-DSM-C01` only.|
|Bogshade Huntress|Shadow Marsh|Story/Contract Unique|Darkness|Shadow Spider variant with Poison and Mark|Venom Sac;Dark Crystal;Equipment up to Epic;Gold|During `S-T2-05`,drops `Marsh Hunter's Token`;during `R-DSM-B01`,spawns as Bounty and drops `Bogshade Token`.|
|Grave Wraith|Forgotten Crypt|Normal|Darkness|Dark Bolt and Fear caster|Cursed Twig;Dark Crystal;Common-Rare Equipment;Gold|`Crypt Seal Fragment` during `R-DFC-C01` only.|
|Plague Mummy|Forgotten Crypt|Normal|Darkness|Poison and Curse attacker|Venom Sac;Cursed Twig;Common-Rare Equipment;Gold|`Crypt Seal Fragment` during `R-DFC-C01` only.|
|Night Hag|Forgotten Crypt|Normal|Darkness|Silence,Confusion,and Life Drain caster|Dark Crystal;Mana Mushroom;Common-Rare Equipment;Gold|None.|
|Gravebound Knight Arct|Forgotten Crypt|Contract Unique|Darkness|Dread Knight variant with Stun|Dark Crystal;Crystal Shard;Equipment up to Epic;Gold|Spawns only during `R-DFC-B01`;drops `Gravebound Crest`.|
|Void Golem|Void Rift|Elite|Darkness,Earth|High Defense void construct|Dark Crystal;Crystal Shard;Equipment up to Epic;Gold|`Rift Stabilizer Fragment` during `R-DVR-C01` only.|
|Shadow Drake|Void Rift|Elite|Darkness,Air|Shadow Mark,Fear,and Gale attacker|Dark Crystal;Shadow Scale;Equipment up to Epic;Gold|`Rift Stabilizer Fragment` during `R-DVR-C01` only.|
|Dread Knight|Void Rift|Elite|Darkness|Armor Break and Stun fighter|Dark Crystal;Iron Ore;Equipment up to Epic;Gold|None.|
|Riftbound Echo|Void Rift|Story/Contract Unique|Darkness|Void Golem variant with Soul Rend|Dark Crystal;Magic Crystal;Equipment up to Epic;Gold|During `S-T4-05`,drops `Void Compass`;during `R-DVR-B01`,spawns as Bounty and drops `Rift Echo Shard`.|
|Shadow Lord|Dread Throne|Regional Boss|Darkness|Summoning Darkness boss with Voidstorm|Dark Crystal;Dragon Rune;Equipment up to Epic;Gold|Drops `Darkness Sigil` during `S-T6-05`;drops `Dread Veil Fragment` only during `R-DDT-B01`.|

---

# Holy Region

Primary Element: Holy

## Areas

|Order|Area|
|---|---|
|1|Sunlit Road|
|2|Temple Gardens|
|3|Sanctum Halls|
|4|Dawn Basilica|
|5|Oracle Chamber|

## Enemies and Loot

|Enemy|Area|Rank|Element Types|Combat Role|Standard Loot|Conditional Quest Loot|
|---|---|---|---|---|---|---|
|Sun Acolyte|Sunlit Road|Normal|Holy|Holy Bolt,Heal,and Regeneration caster|Holy Crystal;Forest Herb;Common-Uncommon Equipment;Gold|`Procession Ribbon` during `R-HSR-C01` only.|
|Temple Squire|Sunlit Road|Normal|Holy|Fortify and Stun defender|Holy Crystal;Iron Ore;Common-Uncommon Equipment;Gold|`Procession Ribbon` during `R-HSR-C01` only.|
|Sunwing Hawk|Sunlit Road|Contract Unique|Holy,Air|Radiant Hawk variant with Blind|Holy Crystal;Harpy Feather;Equipment up to Epic;Gold|Spawns only during `R-HSR-B01`;drops `Sunwing Feather`.|
|Radiant Hawk|Temple Gardens|Normal|Holy,Air|Blind,Gale,and Quick Attack enemy|Harpy Feather;Holy Crystal;Common-Rare Equipment;Gold|`Sunroot Pollen` during `R-HTG-C01` only.|
|Light Sprite|Temple Gardens|Normal|Holy|Focus and Haste support enemy|Holy Crystal;Mana Mushroom;Common-Rare Equipment;Gold|`Sunroot Pollen` during `R-HTG-C01` only.|
|Sacred Treant|Temple Gardens|Normal|Holy,Earth|Barrier and Fortify defender|Holy Crystal;Stone Core;Common-Rare Equipment;Gold|None.|
|Blighted Blossom|Temple Gardens|Story/Contract Unique|Holy,Darkness|Sacred Treant variant with corruption effects|Holy Crystal;Magic Crystal;Equipment up to Epic;Gold|During `S-T2-06`,drops `Sunroot Seed`;during `R-HTG-B01`,spawns as Bounty and drops `Blighted Petal`.|
|Stone Guardian|Sanctum Halls|Normal|Earth,Holy|Barrier and Stun construct|Ancient Coin;Crystal Shard;Common-Rare Equipment;Gold|`Sanctum Archive Seal` during `R-HSH-C01` only.|
|Sun Priest|Sanctum Halls|Normal|Holy|Cleanse,Heal,and Holy caster|Holy Crystal;Magic Crystal;Common-Rare Equipment;Gold|`Sanctum Archive Seal` during `R-HSH-C01` only.|
|Inquisitor|Sanctum Halls|Normal|Holy,Darkness|Silence and Judgment caster|Ancient Coin;Holy Crystal;Common-Rare Equipment;Gold|None.|
|Veiled Inquisitor Sorn|Sanctum Halls|Contract Unique|Holy,Darkness|Inquisitor variant with stronger Silence|Ancient Coin;Holy Crystal;Equipment up to Epic;Gold|Spawns only during `R-HSH-B01`;drops `Veiled Seal`.|
|Dawn Seraph|Dawn Basilica|Elite|Holy,Air|Haste,Barrier,Gale,and Holy caster|Holy Crystal;Harpy Feather;Equipment up to Epic;Gold|`Basilica Ward Fragment` during `R-HDB-C01` only.|
|Warden|Dawn Basilica|Elite|Holy,Earth|Heavy defender with Fortify|Holy Crystal;Stone Core;Equipment up to Epic;Gold|`Basilica Ward Fragment` during `R-HDB-C01` only.|
|Fallen Seraph Amon|Dawn Basilica|Story/Contract Unique|Holy,Darkness|Dawn Seraph variant with Magic Vulnerability|Holy Crystal;Dark Crystal;Equipment up to Epic;Gold|During `S-T4-06`,drops `Oath Feather [Story]`;during `R-HDB-B01`,spawns as Bounty and drops `Oath Feather [Bounty]`.|
|Oracle|Oracle Chamber|Regional Boss|Holy|Barrier,Cleanse,Solar Verdict,and Judgment boss|Holy Crystal;Dragon Rune;Equipment up to Epic;Gold|Drops `Holy Sigil` during `S-T6-06`;drops `Oracle's Trial Seal` only during `R-HOC-B01`.|

---

# Dragon King's Dominion

Primary Element: Multiple

## Areas

|Order|Area|
|---|---|
|1|Dragon Valley|
|2|Dragon Cave|
|3|Obsidian Citadel|
|4|Ancient Nest|
|5|Dragon King's Lair|

## Enemies and Loot

|Enemy|Area|Rank|Element Types|Combat Role|Standard Loot|Conditional Quest Loot|
|---|---|---|---|---|---|---|
|Dragon Servant|Dragon Valley|Normal|Darkness,Fire|Darkness caster with Burn and Berserk|Dragon Rune;Dark Crystal;Common-Rare Equipment;Gold|`Dragonwatch Route Mark` during `R-DRDV-C01` only.|
|Dragon Whelp|Dragon Valley|Normal|Fire|Burn and Quick Attack dragon|Dragon Claw;Dragon Rune;Common-Rare Equipment;Gold|`Dragonwatch Route Mark` during `R-DRDV-C01` only.|
|Redscale Whelp|Dragon Valley|Contract Unique|Fire|Dragon Whelp variant with stronger Burn|Dragon Claw;Dragon Rune;Equipment up to Epic;Gold|Spawns only during `R-DRDV-B01`;drops `Redscale Horn`.|
|Wyvern|Dragon Cave|Normal|Air,Fire|Gale,Bleeding,Burn,and Haste attacker|Dragon Claw;Harpy Feather;Common-Rare Equipment;Gold|`Cave Binding Fragment` during `R-DRDC-C01` only.|
|Dragon Archer|Dragon Cave|Normal|Air|Pinning and Piercing ranged attacker|Dragon Rune;Harpy Feather;Common-Rare Equipment;Gold|`Cave Binding Fragment` during `R-DRDC-C01` only.|
|Bone Dragon|Dragon Cave / Ancient Nest|Elite|Darkness|Shadow Mark,Fear,Barrier,and Dark Bolt enemy|Dragon Bone;Dark Crystal;Equipment up to Epic;Gold|`Nest Survey Fragment` during `R-DRAN-C01` only when encountered in Ancient Nest.|
|Bonewing Remnant|Dragon Cave|Contract Unique|Darkness,Air|Bone Dragon variant with Winded|Dragon Bone;Dark Crystal;Equipment up to Epic;Gold|Spawns only during `R-DRDC-B01`;drops `Bonewing Scale`.|
|Dragon Knight|Obsidian Citadel|Normal|Fire,Darkness|Armor Break,Fortify,Stun,and Heavy Attack fighter|Obsidian Fragment;Dragon Rune;Common-Rare Equipment;Gold|`Citadel Armory Tag` during `R-DROC-C01` only.|
|Dragon Priest|Obsidian Citadel|Normal|Holy,Fire|Cleanse,Regeneration,Heal,and Holy caster|Holy Crystal;Dragon Rune;Common-Rare Equipment;Gold|`Citadel Armory Tag` during `R-DROC-C01` only.|
|Dragon Warlock|Obsidian Citadel|Normal|Darkness,Fire|Silence,Focus,Soul Rend,and Dark Bolt caster|Dark Crystal;Dragon Rune;Common-Rare Equipment;Gold|`Citadel Armory Tag` during `R-DROC-C01` only.|
|Obsidian Guardian|Obsidian Citadel|Elite|Fire,Earth|High Defense construct|Obsidian Core;Obsidian Fragment;Equipment up to Epic;Gold|None.|
|Obsidian Warden Korr|Obsidian Citadel|Story/Contract Unique|Fire,Earth|Obsidian Guardian variant with Barrier and Stun|Obsidian Core;Ancient Dragon Fang;Equipment up to Epic;Gold|During `S-DRAGON-03`,drops `Citadel Gate Sigil`;during `R-DROC-B01`,spawns as Bounty and drops `Warden Command Sigil`.|
|Dragon Knight Captain|Ancient Nest|Elite|Fire,Darkness|Rally,Armor Break,Stun,and Fortify leader|Dragon Rune;Obsidian Fragment;Equipment up to Epic;Gold|`Nest Survey Fragment` during `R-DRAN-C01` only.|
|Ancient Dragon|Ancient Nest|Repeatable Boss|Fire,Air,Darkness|Dragonfire Breath,Storm Wing,Eclipse,and Scale Harden boss|Ancient Dragon Scale;Ancient Dragon Fang;Dragon Rune;Mythic Ember;Equipment up to Epic;Gold|During `S-DRAGON-04`,drops `Ancient Memory Scale`;during `R-DRAN-B01`,drops `Ancient Dragon Memory Scale`.|
|Dragon King|Dragon King's Lair|Final Boss|Fire,Air,Darkness|Final multi-element boss|None|Spawns only for `S-DRAGON-05`;drops only `Dragon King's Seal`.|

---

# Story Quest Item Register

All Story Quest Items are available only while their exact Story Quest is active. `Fixed Search Node` means a scripted interaction,not a normal enemy drop.

|Quest Item|Linked Quest|Area|Source|Conditional Rule|
|---|---|---|---|---|
|Wayfinder Compass|S-000|Town Archive|Archivist Mira Vale|Given by the Story NPC after speaking with Mira.|
|Surveyor Marker|S-T1-01|Forest Entrance|Fixed Search Node|Collect 3 from marked surveyor locations.|
|Caravan Ledger|S-T1-02|Desert Border|Fixed Search Node|Recovered from a scripted caravan trail interaction.|
|Frostbitten Locket|S-T1-03|Mountain Foothills|Fixed Search Node|Recovered from a scripted climber route interaction.|
|Cinder Scout Report|S-T1-04|Ashen Border|Fixed Search Node|Recovered from a scripted scout camp interaction.|
|Lantern of Lost Names|S-T1-05|Gloomwood|Fixed Search Node|Recovered from a scripted lantern shrine.|
|Dawn Processional Bell|S-T1-06|Sunlit Road|Fixed Search Node|Recovered from a scripted procession route.|
|Earthen Totem Shard|S-T2-01|Goblin Forest|Totem-Bound Goblin|Guaranteed after defeating the Story Unique.|
|Singing Sand Vial|S-T2-02|Scorching Dunes|Glasswing Vulture|Guaranteed after defeating the Story Unique.|
|Resonance Crystal|S-T2-03|Mountain Pass|Echo Stalker|Guaranteed after defeating the Story Unique.|
|Ember Collar|S-T2-04|Ember Fields|Ashfang Hound|Guaranteed after defeating the Story Unique.|
|Marsh Hunter's Token|S-T2-05|Shadow Marsh|Bogshade Huntress|Guaranteed after defeating the Story Unique.|
|Sunroot Seed|S-T2-06|Temple Gardens|Blighted Blossom|Guaranteed after defeating the Story Unique.|
|Thornheart Knot|S-T3-01|Overgrown Trail|Thorn Matriarch|Guaranteed after defeating the Story Unique.|
|Stormbound Standard|S-T3-02|Bandit Camp|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Miner's Drill Key|S-T3-03|Echo Mine|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Molten Pressure Valve|S-T3-04|Lava Fissures|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Epitaph Seal|S-T3-05|Forgotten Crypt|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Sanctum Cipher Plate|S-T3-06|Sanctum Halls|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Ancient Sap Vial|S-T4-01|Deep Woods|Grove Shrine|Appears only after inspecting the Story interaction.|
|Astral Lens|S-T4-02|Ancient Ruins|Fixed Quest Cache|Appears only after activating the Wind Seals.|
|Frozen Star Chart|S-T4-03|Ice Caves|Icebound Scribe|Guaranteed after defeating the Story Unique.|
|Forge Heart Key|S-T4-04|Magma Forge|Forged Flame Sentinel|Guaranteed after defeating the Story Unique.|
|Void Compass|S-T4-05|Void Rift|Riftbound Echo|Guaranteed after defeating the Story Unique.|
|Oath Feather [Story]|S-T4-06|Dawn Basilica|Fallen Seraph Amon|Guaranteed after defeating the Story Unique.|
|Royal Clearing Key|S-T5-01|King's Clearing|Royal Totems|Recovered after destroying the three required Story Totems.|
|Guardian Oath Plate|S-T5-02|Ruin Guardian Chamber|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Shrine Prayer Cord|S-T5-03|Frozen Peak|Prayer Beacon Interaction|Appears after lighting the required Prayer Beacons.|
|Core Binding Chain|S-T5-04|Inferno Core|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Veilbreaker Sigil|S-T5-05|Dread Throne|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Dawn Trial Seal|S-T5-06|Oracle Chamber|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Earth Sigil|S-T6-01|King's Clearing|Goblin King|Guaranteed once after the Story Boss defeat.|
|Air Sigil|S-T6-02|Ruin Guardian Chamber|Ruin Guardian|Guaranteed once after the Story Boss defeat.|
|Water Sigil|S-T6-03|Summit Shrine|Frost Titan|Guaranteed once after the Story Boss defeat.|
|Fire Sigil|S-T6-04|Inferno Core|Inferno Lord|Guaranteed once after the Story Boss defeat.|
|Darkness Sigil|S-T6-05|Dread Throne|Shadow Lord|Guaranteed once after the Story Boss defeat.|
|Holy Sigil|S-T6-06|Oracle Chamber|Oracle|Guaranteed once after the Story Boss defeat.|
|Dominion Map|S-DRAGON-00|Town Archive|Archivist Mira Vale|Given after all six Sigils are shown.|
|Dragonwatch Signal Horn|S-DRAGON-01|Dragon Valley|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Ashen Draconic Tablet|S-DRAGON-02|Dragon Cave|Fixed Quest Cache|Appears only while the Story Quest is active.|
|Citadel Gate Sigil|S-DRAGON-03|Obsidian Citadel|Obsidian Warden Korr|Guaranteed after defeating the Story Unique.|
|Ancient Memory Scale|S-DRAGON-04|Ancient Nest|Ancient Dragon|Guaranteed after the first Story defeat.|
|Dragon King's Seal|S-DRAGON-05|Dragon King's Lair|Dragon King|The only final boss drop. No Gold,Materials,Equipment,or Potions.|

---

# Repeatable Area Collection Item Register

Every listed carrier drops exactly 1 shared Collection Item with 100% chance only while the linked Contract is active and its objective still needs more items.

|Quest Item|Linked Contract|Area|Eligible Carrier Mobs|
|---|---|---|---|
|Trail Survey Tag|R-EFE-C01|Forest Entrance|Forest Rat;Wild Boar|
|Caravan Wheel Seal|R-ADB-C01|Desert Border|Desert Rat;Sand Beetle|
|Climber Route Flag|R-WMF-C01|Mountain Foothills|Snow Wolf;Ice Bat|
|Evacuation Route Token|R-FAB-C01|Ashen Border|Ash Lizard;Ember Hound|
|Pilgrim Name Strip|R-DG-C01|Gloomwood|Shade;Bone Hound|
|Procession Ribbon|R-HSR-C01|Sunlit Road|Sun Acolyte;Temple Squire|
|Goblin Patrol Token|R-EGF-C01|Goblin Forest|Goblin Scout;Goblin Dagger;Goblin Archer|
|Singing Sand Packet|R-ASD-C01|Scorching Dunes|Sand Scorpion;Vulture|
|Pass Supply Tag|R-WMP-C01|Mountain Pass|Rock Crawler;Harpy|
|Heatproof Sample|R-FEF-C01|Ember Fields|Lava Slime;Magma Beetle|
|Marsh Trail Marker|R-DSM-C01|Shadow Marsh|Shadow Spider;Dark Wolf|
|Sunroot Pollen|R-HTG-C01|Temple Gardens|Radiant Hawk;Light Sprite|
|Thorn Sap Sample|R-EOT-C01|Overgrown Trail|Moss Spider;Thorn Beast;Fungus|
|Bandit Supply Seal|R-ABC-C01|Bandit Camp|Bandit Scout;Sand Raider;Bandit Archer|
|Mine Claim Stamp|R-WEM-C01|Echo Mine|Crystal Beetle;Mine Wraith;Stone Golem|
|Fissure Heat Sample|R-FLF-C01|Lava Fissures|Flame Elemental;Cinder Witch|
|Crypt Seal Fragment|R-DFC-C01|Forgotten Crypt|Grave Wraith;Plague Mummy|
|Sanctum Archive Seal|R-HSH-C01|Sanctum Halls|Stone Guardian;Sun Priest|
|Grove Memory Shard|R-EDW-C01|Deep Woods|Goblin Mage;Treant|
|Observatory Gear Segment|R-AAR-C01|Ancient Ruins|Sand Wraith;Desert Shaman;Mummy|
|Ice Cave Survey Chip|R-WIC-C01|Ice Caves|Frost Spider;Frost Mage|
|Forge Calibration Plate|R-FMF-C01|Magma Forge|Molten Golem;Ember Wyrm|
|Rift Stabilizer Fragment|R-DVR-C01|Void Rift|Void Golem;Shadow Drake|
|Basilica Ward Fragment|R-HDB-C01|Dawn Basilica|Dawn Seraph;Warden|
|Peak Prayer Bead|R-WFP-C01|Frozen Peak|Mountain Beast;Harpy|
|Dragonwatch Route Mark|R-DRDV-C01|Dragon Valley|Dragon Servant;Dragon Whelp|
|Cave Binding Fragment|R-DRDC-C01|Dragon Cave|Wyvern;Dragon Archer|
|Citadel Armory Tag|R-DROC-C01|Obsidian Citadel|Dragon Knight;Dragon Priest;Dragon Warlock|
|Nest Survey Fragment|R-DRAN-C01|Ancient Nest|Dragon Knight Captain;Bone Dragon|

---

# Repeatable Unique and Boss Challenge Proof Register

A Contract Unique or Boss Challenge target spawns only while its exact Contract is active. It drops exactly 1 Bounty Proof only while the Contract is active and incomplete.

|Target|Linked Contract|Area|Conditional Proof|Type|
|---|---|---|---|---|
|Barkhide Boar|R-EFE-B01|Forest Entrance|Barkhide Tusk|Contract Unique|
|Dustrunner Scarab|R-ADB-B01|Desert Border|Dustrunner Carapace|Contract Unique|
|Whitefang Alpha|R-WMF-B01|Mountain Foothills|Whitefang Pelt|Contract Unique|
|Ashfang Hound|R-FAB-B01|Ashen Border|Ashfang Collar|Contract Unique|
|Lantern Shade|R-DG-B01|Gloomwood|Lantern Wick|Contract Unique|
|Sunwing Hawk|R-HSR-B01|Sunlit Road|Sunwing Feather|Contract Unique|
|Boneknife Skulk|R-EGF-B01|Goblin Forest|Boneknife Insignia|Contract Unique|
|Glasswing Vulture|R-ASD-B01|Scorching Dunes|Glasswing Feather|Contract Unique|
|Echo Stalker|R-WMP-B01|Mountain Pass|Echo Fragment|Contract Unique|
|Magmaheart Slime|R-FEF-B01|Ember Fields|Magmaheart Core|Contract Unique|
|Bogshade Huntress|R-DSM-B01|Shadow Marsh|Bogshade Token|Contract Unique|
|Blighted Blossom|R-HTG-B01|Temple Gardens|Blighted Petal|Contract Unique|
|Webmother Nyss|R-EOT-B01|Overgrown Trail|Webmother Gland|Contract Unique|
|Dune Captain Kharif|R-ABC-B01|Bandit Camp|Captain's Badge|Contract Unique|
|Quartzback Golem|R-WEM-B01|Echo Mine|Quartzback Core|Contract Unique|
|Embermaw Lizard|R-FLF-B01|Lava Fissures|Embermaw Fang|Contract Unique|
|Gravebound Knight Arct|R-DFC-B01|Forgotten Crypt|Gravebound Crest|Contract Unique|
|Veiled Inquisitor Sorn|R-HSH-B01|Sanctum Halls|Veiled Seal|Contract Unique|
|Hollowroot Treant|R-EDW-B01|Deep Woods|Hollowroot Bark|Contract Unique|
|Ashen Mummy Scribe|R-AAR-B01|Ancient Ruins|Scribe's Tablet|Contract Unique|
|Icefang Matriarch|R-WIC-B01|Ice Caves|Icefang Fang|Contract Unique|
|Forged Flame Sentinel|R-FMF-B01|Magma Forge|Sentinel Core|Contract Unique|
|Riftbound Echo|R-DVR-B01|Void Rift|Rift Echo Shard|Contract Unique|
|Fallen Seraph Amon|R-HDB-B01|Dawn Basilica|Oath Feather [Bounty]|Contract Unique|
|Goblin King|R-EKC-B01|King's Clearing|King's Crown Shard|Boss Challenge|
|Ruin Guardian|R-ARGC-B01|Ruin Guardian Chamber|Guardian Core Plate|Boss Challenge|
|Stormclaw Harpy|R-WFP-B01|Frozen Peak|Stormclaw Plume|Contract Unique|
|Inferno Lord|R-FIC-B01|Inferno Core|Inferno Ember|Boss Challenge|
|Shadow Lord|R-DDT-B01|Dread Throne|Dread Veil Fragment|Boss Challenge|
|Oracle|R-HOC-B01|Oracle Chamber|Oracle's Trial Seal|Boss Challenge|
|Frost Titan|R-WSS-B01|Summit Shrine|Titan Glacier Heart|Boss Challenge|
|Redscale Whelp|R-DRDV-B01|Dragon Valley|Redscale Horn|Contract Unique|
|Bonewing Remnant|R-DRDC-B01|Dragon Cave|Bonewing Scale|Contract Unique|
|Obsidian Warden Korr|R-DROC-B01|Obsidian Citadel|Warden Command Sigil|Contract Unique|
|Ancient Dragon|R-DRAN-B01|Ancient Nest|Ancient Dragon Memory Scale|Boss Challenge|

---

# Quest Equipment Reward Register

|Item|Source|Grade|Drop or Reward Rule|Suggested Purpose|
|---|---|---|---|---|
|Thornward Ring|S-T3-01|Rare|Fixed Story Quest Reward;not a random drop.|Earth Resistance and Poison Resistance.|
|Dune Watcher's Charm|S-T3-02|Rare|Fixed Story Quest Reward;not a random drop.|Accuracy and Air Resistance.|
|Echo Miner Pendant|S-T4-03|Rare|Fixed Story Quest Reward;not a random drop.|Magical Defense and Freeze Resistance.|
|Forgehand Bracer|S-T4-04|Epic|Fixed Story Quest Reward;not a random drop.|Physical Attack and Fire Resistance.|
|Mourning Veil|S-T4-05|Epic|Fixed Story Quest Reward;not a random drop.|Darkness Resistance and Magic Power.|
|Dawnkeeper Brooch|S-T4-06|Epic|Fixed Story Quest Reward;not a random drop.|Holy Resistance and Healing Received.|
|Dragonwatch Band|S-DRAGON-03|Epic|Fixed Story Quest Reward;not a random drop.|Defense,Magical Defense,and Dragon-related Resistance if implemented.|

---

# Final Boss Rule

|Boss|Story Quest|Loot|
|---|---|---|
|Dragon King|S-DRAGON-05|`Dragon King's Seal` only.|

> The Dragon King does not drop Gold,Equipment,Potions,Crafting Materials,Dragon Runes,Ancient Dragon Scale,Ancient Dragon Fang,or Mythic Ember.

---

## Documentation Links

This preserved source is retained in full. The canonical integrated design is in
[12_Enemy_Codex.md](12_Enemy_Codex.md); the documentation index is [00_README.md](00_README.md).
Where this source conflicts with newer documents, see
[16_Consistency_Audit.md](16_Consistency_Audit.md) rather than deleting this record.

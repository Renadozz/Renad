# Enemy Codex: Base Stats, Exact Rewards, and Loot

## Linked documents

[Map](10_Map_Regions_and_Progression.md) · [Encounter spawns](11_Encounter_Spawns.md) · [Enemy AI](13_Enemy_AI_Patterns.md) · [Boss patterns](14_Boss_Patterns.md) · [Equipment pools](05_Equipment_and_Drop_Pools.md)

## Fixed reward policy

Each enemy row below is the reward source of truth.

|Reward field|Rule|
|---|---|
|XP|Fixed amount per defeat from the revised slow-progression reward bands. Dragon King enemy XP is 0; `S-DRAGON-05` applies its Quest XP only after victory.|
|Gold|Fixed amount per defeat; no random range.|
|Guaranteed materials|Every listed `1×` material is awarded once on every valid defeat.|
|Equipment|One independent roll. A success grants one item from the linked named pool.|
|Quest / proof|Only resolves if its exact Story Quest or Contract is active and incomplete.|
|No direct ordinary potions|Normal enemies grant materials/ingredients, not craftable potions.|
|Rank|Regional Boss and Repeatable Boss both implement as `Boss`; Story and Contract Unique implement as `Mini Boss`.|

## Base-stat construction

```text
Area Stage → baseline level and stat band
Rank → fixed multiplier
Combat role → deterministic role modifier
Element list → default +25% resistance to each listed element
```

The visible stat sequence is:

```text
Lv / HP / PAtk / MPow / Def / MDef / Spd / Acc / Eva / Crit / SR
```

`SR` = Status Resistance. Stats are generated baseline values before temporary AI buffs, equipment-like boss phases, or encounter-specific scaling.

## Forest Entrance — Earth Region (Stage 1)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Forest Rat|Normal|Earth|Fast physical attacker|Lv 1 / HP 105 / P 16 / M 12 / D 10 / MD 10 / Spd 12 / Acc 80 / Eva 9 / Crit 8 / SR 3|Earth +25%|140 XP|28 Gold|1× Forest Herb; 1× Iron Scrap|10%: 1 item from [Earth Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Trail Survey Tag` during `R-EFE-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-forest-rat)|[Loot](12_Enemy_Codex.md#monster-forest-rat)|
|Wild Boar|Normal|Earth|Durable physical attacker|Lv 1 / HP 145 / P 15 / M 12 / D 13 / MD 11 / Spd 8 / Acc 71 / Eva 3 / Crit 5 / SR 8|Earth +25%|140 XP|28 Gold|1× Beast Claw; 1× Forest Herb|10%: 1 item from [Earth Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Trail Survey Tag` during `R-EFE-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-wild-boar)|[Loot](12_Enemy_Codex.md#monster-wild-boar)|
|Barkhide Boar|Mini Boss|Earth|Wild Boar variant with Fortify|Lv 3 / HP 285 / P 28 / M 26 / D 25 / MD 23 / Spd 9 / Acc 71 / Eva 4 / Crit 3 / SR 8|Earth +25%|360 XP|67 Gold|1× Beast Claw; 1× Iron Scrap|18%: 1 item from [Earth Tier 1 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-EFE-B01`;drops `Barkhide Tusk`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-barkhide-boar)|[Loot](12_Enemy_Codex.md#monster-barkhide-boar)|
## Desert Border — Air Region (Stage 1)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Desert Rat|Normal|Air|Fast physical attacker|Lv 1 / HP 105 / P 16 / M 12 / D 10 / MD 10 / Spd 12 / Acc 80 / Eva 9 / Crit 8 / SR 3|Air +25%|140 XP|28 Gold|1× Cactus Sap|10%: 1 item from [Air Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Caravan Wheel Seal` during `R-ADB-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-desert-rat)|[Loot](12_Enemy_Codex.md#monster-desert-rat)|
|Sand Beetle|Normal|Earth|Defensive physical enemy|Lv 1 / HP 130 / P 13 / M 12 / D 12 / MD 11 / Spd 9 / Acc 71 / Eva 3 / Crit 3 / SR 8|Earth +25%|140 XP|28 Gold|1× Iron Ore; 1× Beetle Shell|10%: 1 item from [Air Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Caravan Wheel Seal` during `R-ADB-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-sand-beetle)|[Loot](12_Enemy_Codex.md#monster-sand-beetle)|
|Dustrunner Scarab|Mini Boss|Earth,Air|Sand Beetle variant with Haste|Lv 3 / HP 205 / P 30 / M 26 / D 20 / MD 20 / Spd 13 / Acc 80 / Eva 10 / Crit 6 / SR 4|Earth +25%; Air +25%|360 XP|67 Gold|1× Iron Ore; 1× Air Crystal|18%: 1 item from [Air Tier 1 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-ADB-B01`;drops `Dustrunner Carapace`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dustrunner-scarab)|[Loot](12_Enemy_Codex.md#monster-dustrunner-scarab)|
## Mountain Foothills — Water Region (Stage 1)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Snow Wolf|Normal|Water|Haste and Bleeding physical attacker|Lv 1 / HP 105 / P 16 / M 12 / D 10 / MD 10 / Spd 12 / Acc 80 / Eva 9 / Crit 8 / SR 3|Water +25%|140 XP|28 Gold|1× Ice Moss; 1× Beast Claw|10%: 1 item from [Water Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Climber Route Flag` during `R-WMF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-snow-wolf)|[Loot](12_Enemy_Codex.md#monster-snow-wolf)|
|Ice Bat|Normal|Water,Air|Blind and Frost attacker|Lv 1 / HP 110 / P 14 / M 12 / D 10 / MD 10 / Spd 11 / Acc 73 / Eva 4 / Crit 3 / SR 3|Water +25%; Air +25%|140 XP|28 Gold|1× Frost Crystal; 1× Ice Moss|10%: 1 item from [Water Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Climber Route Flag` during `R-WMF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ice-bat)|[Loot](12_Enemy_Codex.md#monster-ice-bat)|
|Whitefang Alpha|Mini Boss|Water|Snow Wolf variant with stronger Bleeding|Lv 3 / HP 235 / P 30 / M 26 / D 20 / MD 20 / Spd 11 / Acc 73 / Eva 4 / Crit 3 / SR 4|Water +25%|360 XP|67 Gold|1× Ice Moss; 1× Beast Claw|18%: 1 item from [Water Tier 1 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-WMF-B01`;drops `Whitefang Pelt`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-whitefang-alpha)|[Loot](12_Enemy_Codex.md#monster-whitefang-alpha)|
## Ashen Border — Fire Region (Stage 1)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Ash Lizard|Normal|Fire|Fast Burn attacker|Lv 1 / HP 95 / P 14 / M 12 / D 10 / MD 10 / Spd 13 / Acc 80 / Eva 9 / Crit 6 / SR 3|Fire +25%|140 XP|28 Gold|1× Ember Core; 1× Beast Claw|10%: 1 item from [Fire Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Evacuation Route Token` during `R-FAB-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ash-lizard)|[Loot](12_Enemy_Codex.md#monster-ash-lizard)|
|Ember Hound|Normal|Fire|Haste physical attacker|Lv 1 / HP 105 / P 16 / M 12 / D 10 / MD 10 / Spd 12 / Acc 80 / Eva 9 / Crit 8 / SR 3|Fire +25%|140 XP|28 Gold|1× Ember Core; 1× Beast Claw|10%: 1 item from [Fire Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Evacuation Route Token` during `R-FAB-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ember-hound)|[Loot](12_Enemy_Codex.md#monster-ember-hound)|
## Gloomwood — Darkness Region (Stage 1)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Shade|Normal|Darkness|Fast Darkness caster|Lv 1 / HP 95 / P 10 / M 15 / D 10 / MD 11 / Spd 13 / Acc 80 / Eva 9 / Crit 6 / SR 6|Darkness +25%|140 XP|28 Gold|1× Cursed Twig; 1× Mana Mushroom|10%: 1 item from [Darkness Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Pilgrim Name Strip` during `R-DG-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-shade)|[Loot](12_Enemy_Codex.md#monster-shade)|
|Bone Hound|Normal|Darkness|Fear and Bleeding attacker|Lv 1 / HP 110 / P 14 / M 12 / D 10 / MD 10 / Spd 11 / Acc 73 / Eva 4 / Crit 3 / SR 3|Darkness +25%|140 XP|28 Gold|1× Beast Claw; 1× Cursed Twig|10%: 1 item from [Darkness Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Pilgrim Name Strip` during `R-DG-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-bone-hound)|[Loot](12_Enemy_Codex.md#monster-bone-hound)|
|Lantern Shade|Mini Boss|Darkness|Shade variant with Curse|Lv 3 / HP 235 / P 30 / M 26 / D 20 / MD 20 / Spd 11 / Acc 73 / Eva 4 / Crit 3 / SR 4|Darkness +25%|360 XP|67 Gold|1× Cursed Twig; 1× Dark Crystal|18%: 1 item from [Darkness Tier 1 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-DG-B01`;drops `Lantern Wick`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-lantern-shade)|[Loot](12_Enemy_Codex.md#monster-lantern-shade)|
## Sunlit Road — Holy Region (Stage 1)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Sun Acolyte|Normal|Holy|Holy Bolt,Heal,and Regeneration caster|Lv 1 / HP 110 / P 10 / M 15 / D 10 / MD 11 / Spd 11 / Acc 73 / Eva 4 / Crit 3 / SR 6|Holy +25%|140 XP|28 Gold|1× Holy Crystal; 1× Forest Herb|10%: 1 item from [Holy Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Procession Ribbon` during `R-HSR-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-sun-acolyte)|[Loot](12_Enemy_Codex.md#monster-sun-acolyte)|
|Temple Squire|Normal|Holy|Fortify and Stun defender|Lv 1 / HP 130 / P 13 / M 12 / D 12 / MD 11 / Spd 9 / Acc 71 / Eva 3 / Crit 3 / SR 8|Holy +25%|140 XP|28 Gold|1× Holy Crystal; 1× Iron Ore|10%: 1 item from [Holy Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Procession Ribbon` during `R-HSR-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-temple-squire)|[Loot](12_Enemy_Codex.md#monster-temple-squire)|
|Sunwing Hawk|Mini Boss|Holy,Air|Radiant Hawk variant with Blind|Lv 3 / HP 235 / P 30 / M 26 / D 20 / MD 20 / Spd 11 / Acc 73 / Eva 4 / Crit 3 / SR 4|Holy +25%; Air +25%|360 XP|67 Gold|1× Holy Crystal; 1× Harpy Feather|18%: 1 item from [Holy Tier 1 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-HSR-B01`;drops `Sunwing Feather`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-sunwing-hawk)|[Loot](12_Enemy_Codex.md#monster-sunwing-hawk)|
## Goblin Forest — Earth Region (Stage 2)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Goblin Scout|Normal|Earth|Fast physical attacker|Lv 12 / HP 235 / P 33 / M 25 / D 21 / MD 19 / Spd 14 / Acc 84 / Eva 11 / Crit 9 / SR 5|Earth +25%|320 XP|60 Gold|1× Forest Herb; 1× Iron Scrap|10%: 1 item from [Earth Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Goblin Patrol Token` during `R-EGF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-goblin-scout)|[Loot](12_Enemy_Codex.md#monster-goblin-scout)|
|Goblin Dagger|Normal|Earth|Physical Bleeding attacker|Lv 12 / HP 240 / P 29 / M 25 / D 19 / MD 19 / Spd 12 / Acc 77 / Eva 6 / Crit 4 / SR 5|Earth +25%|320 XP|60 Gold|1× Beast Claw; 1× Iron Scrap|10%: 1 item from [Earth Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Goblin Patrol Token` during `R-EGF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-goblin-dagger)|[Loot](12_Enemy_Codex.md#monster-goblin-dagger)|
|Goblin Archer|Normal|Air|Ranged Blind attacker|Lv 12 / HP 215 / P 29 / M 25 / D 19 / MD 19 / Spd 16 / Acc 84 / Eva 11 / Crit 7 / SR 5|Air +25%|320 XP|60 Gold|1× Harpy Feather; 1× Iron Scrap|10%: 1 item from [Earth Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Goblin Patrol Token` during `R-EGF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-goblin-archer)|[Loot](12_Enemy_Codex.md#monster-goblin-archer)|
|Goblin Shaman|Elite|Earth,Darkness|Support and control caster|Lv 14 / HP 380 / P 31 / M 52 / D 30 / MD 33 / Spd 13 / Acc 78 / Eva 6 / Crit 4 / SR 8|Earth +25%; Darkness +25%|500 XP|93 Gold|1× Iron Ore; 1× Mana Mushroom; 1× Magic Crystal|18%: 1 item from [Earth Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-goblin-shaman)|[Loot](12_Enemy_Codex.md#monster-goblin-shaman)|
|Totem-Bound Goblin|Mini Boss|Earth,Darkness|Goblin Shaman or Goblin Mage variant|Lv 15 / HP 465 / P 37 / M 63 / D 36 / MD 41 / Spd 13 / Acc 78 / Eva 6 / Crit 4 / SR 8|Earth +25%; Darkness +25%|820 XP|144 Gold|1× Iron Ore; 1× Magic Crystal|18%: 1 item from [Earth Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `S-T2-01`;drops `Earthen Totem Shard`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-totem-bound-goblin)|[Loot](12_Enemy_Codex.md#monster-totem-bound-goblin)|
|Boneknife Skulk|Mini Boss|Earth|Goblin Dagger variant|Lv 15 / HP 465 / P 55 / M 50 / D 36 / MD 36 / Spd 13 / Acc 78 / Eva 6 / Crit 4 / SR 5|Earth +25%|820 XP|144 Gold|1× Iron Ore; 1× Beast Claw|18%: 1 item from [Earth Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-EGF-B01`;drops `Boneknife Insignia`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-boneknife-skulk)|[Loot](12_Enemy_Codex.md#monster-boneknife-skulk)|
|Goblin Bomber|Normal|Fire,Earth|Ranged explosive controller|Lv 12 / HP 215 / P 20 / M 33 / D 19 / MD 21 / Spd 16 / Acc 84 / Eva 11 / Crit 7 / SR 8|Fire +25%; Earth +25%|320 XP|60 Gold|1× Bomb Powder; 1× Iron Scrap|10%: 1 item from [Earth Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|No conditional Quest Item. Added as the active source of Bomb Powder.|Added|[Pattern](13_Enemy_AI_Patterns.md#pattern-goblin-bomber)|[Loot](12_Enemy_Codex.md#monster-goblin-bomber)|
## Scorching Dunes — Air Region (Stage 2)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Sand Scorpion|Normal|Earth|Poison and Rooted attacker|Lv 12 / HP 240 / P 29 / M 25 / D 19 / MD 19 / Spd 12 / Acc 77 / Eva 6 / Crit 4 / SR 5|Earth +25%|320 XP|60 Gold|1× Venom Sac; 1× Scorpion Tail|10%: 1 item from [Air Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Singing Sand Packet` during `R-ASD-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-sand-scorpion)|[Loot](12_Enemy_Codex.md#monster-sand-scorpion)|
|Vulture|Normal|Air|Blind and fast ranged attacker|Lv 12 / HP 215 / P 29 / M 25 / D 19 / MD 19 / Spd 16 / Acc 84 / Eva 11 / Crit 7 / SR 5|Air +25%|320 XP|60 Gold|1× Harpy Feather; 1× Air Crystal|10%: 1 item from [Air Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Singing Sand Packet` during `R-ASD-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-vulture)|[Loot](12_Enemy_Codex.md#monster-vulture)|
|Glasswing Vulture|Mini Boss|Air|Vulture variant with stronger Blind|Lv 15 / HP 405 / P 55 / M 50 / D 36 / MD 36 / Spd 16 / Acc 84 / Eva 11 / Crit 7 / SR 5|Air +25%|820 XP|144 Gold|1× Harpy Feather; 1× Air Crystal|18%: 1 item from [Air Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-T2-02`,drops `Singing Sand Vial`;during `R-ASD-B01`,spawns as Bounty and drops `Glasswing Feather`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-glasswing-vulture)|[Loot](12_Enemy_Codex.md#monster-glasswing-vulture)|
|Sand Wolf|Normal|Air,Earth|Fast Bleeding attacker|Lv 12 / HP 215 / P 29 / M 25 / D 19 / MD 19 / Spd 16 / Acc 84 / Eva 11 / Crit 7 / SR 5|Air +25%; Earth +25%|320 XP|60 Gold|1× Beast Claw; 1× Cactus Sap|10%: 1 item from [Air Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Singing Sand Packet` during `R-ASD-C01` only.|Added|[Pattern](13_Enemy_AI_Patterns.md#pattern-sand-wolf)|[Loot](12_Enemy_Codex.md#monster-sand-wolf)|
## Mountain Pass — Water Region (Stage 2)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Rock Crawler|Normal|Earth|High Defense physical attacker|Lv 12 / HP 325 / P 32 / M 25 / D 25 / MD 22 / Spd 10 / Acc 75 / Eva 5 / Crit 6 / SR 10|Earth +25%|320 XP|60 Gold|1× Iron Ore; 1× Stone Core|10%: 1 item from [Water Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Pass Supply Tag` during `R-WMP-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-rock-crawler)|[Loot](12_Enemy_Codex.md#monster-rock-crawler)|
|Harpy|Normal|Air|Gale and Blind attacker|Lv 12 / HP 240 / P 29 / M 25 / D 19 / MD 19 / Spd 12 / Acc 77 / Eva 6 / Crit 4 / SR 5|Air +25%|320 XP|60 Gold|1× Harpy Feather; 1× Air Crystal|10%: 1 item from [Water Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Pass Supply Tag` during `R-WMP-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-harpy)|[Loot](12_Enemy_Codex.md#monster-harpy)|
|Echo Stalker|Mini Boss|Darkness,Water|Mine Wraith variant with Fear|Lv 15 / HP 465 / P 37 / M 63 / D 36 / MD 41 / Spd 13 / Acc 78 / Eva 6 / Crit 4 / SR 8|Darkness +25%; Water +25%|820 XP|144 Gold|1× Crystal Shard; 1× Dark Crystal|18%: 1 item from [Water Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-T2-03`,drops `Resonance Crystal`;during `R-WMP-B01`,spawns as Bounty and drops `Echo Fragment`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-echo-stalker)|[Loot](12_Enemy_Codex.md#monster-echo-stalker)|
## Ashen Border / Ember Fields — Fire Region (Stage 2)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Ashfang Hound|Mini Boss|Fire|Ember Hound variant with Burn and Haste|Lv 15 / HP 405 / P 55 / M 50 / D 36 / MD 36 / Spd 16 / Acc 84 / Eva 11 / Crit 7 / SR 5|Fire +25%|820 XP|144 Gold|1× Ember Core; 1× Beast Claw|18%: 1 item from [Fire Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-T2-04` in Ember Fields,drops `Ember Collar`;during `R-FAB-B01` in Ashen Border,spawns as Bounty and drops `Ashfang Collar`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ashfang-hound)|[Loot](12_Enemy_Codex.md#monster-ashfang-hound)|
## Ember Fields — Fire Region (Stage 2)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Lava Slime|Normal|Fire|Barrier and Fire caster|Lv 12 / HP 295 / P 19 / M 33 / D 24 / MD 24 / Spd 11 / Acc 75 / Eva 5 / Crit 4 / SR 13|Fire +25%|320 XP|60 Gold|1× Obsidian Fragment; 1× Ember Core; 1× Fire Essence|10%: 1 item from [Fire Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Heatproof Sample` during `R-FEF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-lava-slime)|[Loot](12_Enemy_Codex.md#monster-lava-slime)|
|Magma Beetle|Normal|Fire,Earth|Defensive Fire attacker|Lv 12 / HP 295 / P 28 / M 25 / D 24 / MD 22 / Spd 10 / Acc 75 / Eva 5 / Crit 4 / SR 10|Fire +25%; Earth +25%|320 XP|60 Gold|1× Obsidian Fragment; 1× Iron Ore|10%: 1 item from [Fire Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Heatproof Sample` during `R-FEF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-magma-beetle)|[Loot](12_Enemy_Codex.md#monster-magma-beetle)|
|Ash Cultist|Normal|Fire,Darkness|Focus and Fire/Darkness caster|Lv 12 / HP 240 / P 20 / M 33 / D 19 / MD 21 / Spd 13 / Acc 77 / Eva 6 / Crit 4 / SR 8|Fire +25%; Darkness +25%|320 XP|60 Gold|1× Ember Core; 1× Cursed Twig|10%: 1 item from [Fire Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ash-cultist)|[Loot](12_Enemy_Codex.md#monster-ash-cultist)|
|Magmaheart Slime|Mini Boss|Fire|Lava Slime variant with stronger Barrier|Lv 15 / HP 565 / P 52 / M 50 / D 45 / MD 42 / Spd 11 / Acc 76 / Eva 5 / Crit 4 / SR 10|Fire +25%|820 XP|144 Gold|1× Obsidian Fragment; 1× Ember Core|18%: 1 item from [Fire Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-FEF-B01`;drops `Magmaheart Core`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-magmaheart-slime)|[Loot](12_Enemy_Codex.md#monster-magmaheart-slime)|
## Shadow Marsh — Darkness Region (Stage 2)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Shadow Spider|Normal|Darkness|Rooted,Poison,and Shadow Mark attacker|Lv 12 / HP 240 / P 29 / M 25 / D 19 / MD 19 / Spd 12 / Acc 77 / Eva 6 / Crit 4 / SR 5|Darkness +25%|320 XP|60 Gold|1× Venom Sac; 1× Spider Silk|10%: 1 item from [Darkness Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Marsh Trail Marker` during `R-DSM-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-shadow-spider)|[Loot](12_Enemy_Codex.md#monster-shadow-spider)|
|Dark Wolf|Normal|Darkness|Fear,Haste,and Bleeding attacker|Lv 12 / HP 215 / P 29 / M 25 / D 19 / MD 19 / Spd 16 / Acc 84 / Eva 11 / Crit 7 / SR 5|Darkness +25%|320 XP|60 Gold|1× Beast Claw; 1× Dark Crystal|10%: 1 item from [Darkness Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Marsh Trail Marker` during `R-DSM-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dark-wolf)|[Loot](12_Enemy_Codex.md#monster-dark-wolf)|
|Bogshade Huntress|Mini Boss|Darkness|Shadow Spider variant with Poison and Mark|Lv 15 / HP 465 / P 55 / M 50 / D 36 / MD 36 / Spd 13 / Acc 78 / Eva 6 / Crit 4 / SR 5|Darkness +25%|820 XP|144 Gold|1× Venom Sac; 1× Dark Crystal|18%: 1 item from [Darkness Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-T2-05`,drops `Marsh Hunter's Token`;during `R-DSM-B01`,spawns as Bounty and drops `Bogshade Token`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-bogshade-huntress)|[Loot](12_Enemy_Codex.md#monster-bogshade-huntress)|
## Temple Gardens — Holy Region (Stage 2)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Radiant Hawk|Normal|Holy,Air|Blind,Gale,and Quick Attack enemy|Lv 12 / HP 240 / P 29 / M 25 / D 19 / MD 19 / Spd 12 / Acc 77 / Eva 6 / Crit 4 / SR 5|Holy +25%; Air +25%|320 XP|60 Gold|1× Harpy Feather; 1× Holy Crystal|10%: 1 item from [Holy Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Sunroot Pollen` during `R-HTG-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-radiant-hawk)|[Loot](12_Enemy_Codex.md#monster-radiant-hawk)|
|Light Sprite|Normal|Holy|Focus and Haste support enemy|Lv 12 / HP 215 / P 20 / M 33 / D 19 / MD 21 / Spd 16 / Acc 84 / Eva 11 / Crit 7 / SR 8|Holy +25%|320 XP|60 Gold|1× Holy Crystal; 1× Mana Mushroom|10%: 1 item from [Holy Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Sunroot Pollen` during `R-HTG-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-light-sprite)|[Loot](12_Enemy_Codex.md#monster-light-sprite)|
|Sacred Treant|Normal|Holy,Earth|Barrier and Fortify defender|Lv 12 / HP 295 / P 28 / M 25 / D 24 / MD 22 / Spd 10 / Acc 75 / Eva 5 / Crit 4 / SR 10|Holy +25%; Earth +25%|320 XP|60 Gold|1× Holy Crystal; 1× Stone Core|10%: 1 item from [Holy Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-sacred-treant)|[Loot](12_Enemy_Codex.md#monster-sacred-treant)|
|Blighted Blossom|Mini Boss|Holy,Darkness|Sacred Treant variant with corruption effects|Lv 15 / HP 465 / P 55 / M 50 / D 36 / MD 36 / Spd 13 / Acc 78 / Eva 6 / Crit 4 / SR 5|Holy +25%; Darkness +25%|820 XP|144 Gold|1× Holy Crystal; 1× Magic Crystal|18%: 1 item from [Holy Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-T2-06`,drops `Sunroot Seed`;during `R-HTG-B01`,spawns as Bounty and drops `Blighted Petal`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-blighted-blossom)|[Loot](12_Enemy_Codex.md#monster-blighted-blossom)|
## Overgrown Trail — Earth Region (Stage 3)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Moss Spider|Normal|Earth|Poison and Rooted controller|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Earth +25%|700 XP|130 Gold|1× Spider Silk; 1× Venom Sac|10%: 1 item from [Earth Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Thorn Sap Sample` during `R-EOT-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-moss-spider)|[Loot](12_Enemy_Codex.md#monster-moss-spider)|
|Thorn Beast|Normal|Earth|Defensive physical attacker|Lv 25 / HP 565 / P 52 / M 44 / D 41 / MD 35 / Spd 12 / Acc 79 / Eva 7 / Crit 7 / SR 12|Earth +25%|700 XP|130 Gold|1× Forest Herb; 1× Beast Claw; 1× Crystal Shard|10%: 1 item from [Earth Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Thorn Sap Sample` during `R-EOT-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-thorn-beast)|[Loot](12_Enemy_Codex.md#monster-thorn-beast)|
|Fungus|Normal|Earth,Darkness|Poison and Magic controller|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Earth +25%; Darkness +25%|700 XP|130 Gold|1× Mana Mushroom; 1× Redcap; 1× Cursed Twig|10%: 1 item from [Earth Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Thorn Sap Sample` during `R-EOT-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-fungus)|[Loot](12_Enemy_Codex.md#monster-fungus)|
|Thorn Matriarch|Mini Boss|Earth|Thorn Beast variant with Stun|Lv 29 / HP 770 / P 86 / M 79 / D 55 / MD 55 / Spd 15 / Acc 82 / Eva 8 / Crit 5 / SR 7|Earth +25%|1,750 XP|312 Gold|1× Spider Silk; 1× Stone Core|18%: 1 item from [Earth Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `S-T3-01`;drops `Thornheart Knot`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-thorn-matriarch)|[Loot](12_Enemy_Codex.md#monster-thorn-matriarch)|
|Webmother Nyss|Mini Boss|Earth,Darkness|Moss Spider variant with Poison|Lv 29 / HP 770 / P 86 / M 79 / D 55 / MD 55 / Spd 15 / Acc 82 / Eva 8 / Crit 5 / SR 7|Earth +25%; Darkness +25%|1,750 XP|312 Gold|1× Spider Silk; 1× Venom Sac|18%: 1 item from [Earth Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-EOT-B01`;drops `Webmother Gland`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-webmother-nyss)|[Loot](12_Enemy_Codex.md#monster-webmother-nyss)|
## Bandit Camp — Air Region (Stage 3)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Bandit Scout|Normal|Air|Fast physical attacker|Lv 25 / HP 410 / P 55 / M 44 / D 32 / MD 30 / Spd 17 / Acc 88 / Eva 13 / Crit 10 / SR 7|Air +25%|700 XP|130 Gold|1× Iron Ore; 1× Tattered Cloth|10%: 1 item from [Air Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Bandit Supply Seal` during `R-ABC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-bandit-scout)|[Loot](12_Enemy_Codex.md#monster-bandit-scout)|
|Sand Raider|Normal|Air|Berserk physical attacker|Lv 25 / HP 465 / P 55 / M 44 / D 32 / MD 30 / Spd 14 / Acc 81 / Eva 8 / Crit 7 / SR 7|Air +25%|700 XP|130 Gold|1× Iron Ore; 1× Beast Claw|10%: 1 item from [Air Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Bandit Supply Seal` during `R-ABC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-sand-raider)|[Loot](12_Enemy_Codex.md#monster-sand-raider)|
|Bandit Archer|Normal|Air|Pinning and Piercing ranged attacker|Lv 25 / HP 370 / P 48 / M 44 / D 30 / MD 30 / Spd 18 / Acc 88 / Eva 13 / Crit 8 / SR 7|Air +25%|700 XP|130 Gold|1× Harpy Feather; 1× Iron Ore|10%: 1 item from [Air Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Bandit Supply Seal` during `R-ABC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-bandit-archer)|[Loot](12_Enemy_Codex.md#monster-bandit-archer)|
|Bandit Alchemist|Elite|Fire,Air|Poison,Blind,and Fire caster|Lv 27 / HP 630 / P 49 / M 82 / D 46 / MD 50 / Spd 16 / Acc 82 / Eva 8 / Crit 5 / SR 10|Fire +25%; Air +25%|1,050 XP|202 Gold|1× Cactus Sap; 1× Magic Crystal; 1× Bomb Powder|18%: 1 item from [Air Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-bandit-alchemist)|[Loot](12_Enemy_Codex.md#monster-bandit-alchemist)|
|Dune Captain Kharif|Mini Boss|Air|Sand Raider leader with Armor Break|Lv 29 / HP 850 / P 100 / M 79 / D 60 / MD 55 / Spd 15 / Acc 82 / Eva 8 / Crit 7 / SR 7|Air +25%|1,750 XP|312 Gold|1× Iron Ore; 1× Air Crystal|18%: 1 item from [Air Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-ABC-B01`;drops `Captain's Badge`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dune-captain-kharif)|[Loot](12_Enemy_Codex.md#monster-dune-captain-kharif)|
## Echo Mine — Water Region (Stage 3)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Crystal Beetle|Normal|Earth,Water|High Magical Defense enemy|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Earth +25%; Water +25%|700 XP|130 Gold|1× Crystal Shard; 1× Iron Ore|10%: 1 item from [Water Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Mine Claim Stamp` during `R-WEM-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-crystal-beetle)|[Loot](12_Enemy_Codex.md#monster-crystal-beetle)|
|Mine Wraith|Normal|Darkness|Fear and Soul Rend caster|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Darkness +25%|700 XP|130 Gold|1× Dark Crystal; 1× Crystal Shard|10%: 1 item from [Water Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Mine Claim Stamp` during `R-WEM-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-mine-wraith)|[Loot](12_Enemy_Codex.md#monster-mine-wraith)|
|Stone Golem|Normal|Earth|High Defense Stun attacker|Lv 25 / HP 515 / P 45 / M 44 / D 37 / MD 35 / Spd 13 / Acc 79 / Eva 7 / Crit 5 / SR 12|Earth +25%|700 XP|130 Gold|1× Stone Core; 1× Iron Ore|10%: 1 item from [Water Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Mine Claim Stamp` during `R-WEM-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-stone-golem)|[Loot](12_Enemy_Codex.md#monster-stone-golem)|
|Quartzback Golem|Mini Boss|Earth,Water|Stone Golem variant with Barrier|Lv 29 / HP 940 / P 82 / M 79 / D 68 / MD 62 / Spd 13 / Acc 80 / Eva 7 / Crit 5 / SR 12|Earth +25%; Water +25%|1,750 XP|312 Gold|1× Stone Core; 1× Crystal Shard|18%: 1 item from [Water Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-WEM-B01`;drops `Quartzback Core`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-quartzback-golem)|[Loot](12_Enemy_Codex.md#monster-quartzback-golem)|
## Lava Fissures — Fire Region (Stage 3)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Flame Elemental|Normal|Fire|Fire Bolt and Flame Wave caster|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Fire +25%|700 XP|130 Gold|1× Molten Core; 1× Ember Core; 1× Fire Essence|10%: 1 item from [Fire Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Fissure Heat Sample` during `R-FLF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-flame-elemental)|[Loot](12_Enemy_Codex.md#monster-flame-elemental)|
|Cinder Witch|Normal|Fire,Darkness|Confusion and Fire caster|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Fire +25%; Darkness +25%|700 XP|130 Gold|1× Molten Core; 1× Dark Crystal|10%: 1 item from [Fire Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Fissure Heat Sample` during `R-FLF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-cinder-witch)|[Loot](12_Enemy_Codex.md#monster-cinder-witch)|
|Fire Drake|Normal|Fire,Air|Burn and Winded attacker|Lv 25 / HP 370 / P 48 / M 44 / D 30 / MD 30 / Spd 18 / Acc 88 / Eva 13 / Crit 8 / SR 7|Fire +25%; Air +25%|700 XP|130 Gold|1× Molten Core; 1× Ember Core; 1× Fire Essence|10%: 1 item from [Fire Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-fire-drake)|[Loot](12_Enemy_Codex.md#monster-fire-drake)|
|Embermaw Lizard|Mini Boss|Fire|Ash Lizard variant with Charge|Lv 29 / HP 850 / P 100 / M 79 / D 60 / MD 55 / Spd 15 / Acc 82 / Eva 8 / Crit 7 / SR 7|Fire +25%|1,750 XP|312 Gold|1× Molten Core; 1× Beast Claw|18%: 1 item from [Fire Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-FLF-B01`;drops `Embermaw Fang`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-embermaw-lizard)|[Loot](12_Enemy_Codex.md#monster-embermaw-lizard)|
## Forgotten Crypt — Darkness Region (Stage 3)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Grave Wraith|Normal|Darkness|Dark Bolt and Fear caster|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Darkness +25%|700 XP|130 Gold|1× Cursed Twig; 1× Dark Crystal|10%: 1 item from [Darkness Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Crypt Seal Fragment` during `R-DFC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-grave-wraith)|[Loot](12_Enemy_Codex.md#monster-grave-wraith)|
|Plague Mummy|Normal|Darkness|Poison and Curse attacker|Lv 25 / HP 420 / P 48 / M 44 / D 30 / MD 30 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 7|Darkness +25%|700 XP|130 Gold|1× Venom Sac; 1× Cursed Twig|10%: 1 item from [Darkness Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Crypt Seal Fragment` during `R-DFC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-plague-mummy)|[Loot](12_Enemy_Codex.md#monster-plague-mummy)|
|Night Hag|Normal|Darkness|Silence,Confusion,and Life Drain caster|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Darkness +25%|700 XP|130 Gold|1× Dark Crystal; 1× Mana Mushroom|10%: 1 item from [Darkness Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-night-hag)|[Loot](12_Enemy_Codex.md#monster-night-hag)|
|Gravebound Knight Arct|Mini Boss|Darkness|Dread Knight variant with Stun|Lv 29 / HP 850 / P 100 / M 79 / D 60 / MD 55 / Spd 15 / Acc 82 / Eva 8 / Crit 7 / SR 7|Darkness +25%|1,750 XP|312 Gold|1× Dark Crystal; 1× Crystal Shard|18%: 1 item from [Darkness Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-DFC-B01`;drops `Gravebound Crest`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-gravebound-knight-arct)|[Loot](12_Enemy_Codex.md#monster-gravebound-knight-arct)|
## Sanctum Halls — Holy Region (Stage 3)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Stone Guardian|Normal|Earth,Holy|Barrier and Stun construct|Lv 25 / HP 515 / P 45 / M 44 / D 37 / MD 35 / Spd 13 / Acc 79 / Eva 7 / Crit 5 / SR 12|Earth +25%; Holy +25%|700 XP|130 Gold|1× Ancient Coin; 1× Crystal Shard|10%: 1 item from [Holy Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Sanctum Archive Seal` during `R-HSH-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-stone-guardian)|[Loot](12_Enemy_Codex.md#monster-stone-guardian)|
|Sun Priest|Normal|Holy|Cleanse,Heal,and Holy caster|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Holy +25%|700 XP|130 Gold|1× Holy Crystal; 1× Magic Crystal|10%: 1 item from [Holy Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Sanctum Archive Seal` during `R-HSH-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-sun-priest)|[Loot](12_Enemy_Codex.md#monster-sun-priest)|
|Inquisitor|Normal|Holy,Darkness|Silence and Judgment caster|Lv 25 / HP 420 / P 32 / M 55 / D 30 / MD 34 / Spd 15 / Acc 81 / Eva 8 / Crit 5 / SR 10|Holy +25%; Darkness +25%|700 XP|130 Gold|1× Ancient Coin; 1× Holy Crystal|10%: 1 item from [Holy Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-inquisitor)|[Loot](12_Enemy_Codex.md#monster-inquisitor)|
|Veiled Inquisitor Sorn|Mini Boss|Holy,Darkness|Inquisitor variant with stronger Silence|Lv 29 / HP 770 / P 86 / M 79 / D 55 / MD 55 / Spd 15 / Acc 82 / Eva 8 / Crit 5 / SR 7|Holy +25%; Darkness +25%|1,750 XP|312 Gold|1× Ancient Coin; 1× Holy Crystal|18%: 1 item from [Holy Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-HSH-B01`;drops `Veiled Seal`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-veiled-inquisitor-sorn)|[Loot](12_Enemy_Codex.md#monster-veiled-inquisitor-sorn)|
## Deep Woods — Earth Region (Stage 4)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Goblin Mage|Elite|Earth|Earth magic and Rooted controller|Lv 43 / HP 970 / P 72 / M 125 / D 65 / MD 73 / Spd 19 / Acc 86 / Eva 10 / Crit 6 / SR 12|Earth +25%|2,100 XP|403 Gold|1× Magic Crystal; 1× Mana Mushroom|18%: 1 item from [Earth Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Grove Memory Shard` during `R-EDW-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-goblin-mage)|[Loot](12_Enemy_Codex.md#monster-goblin-mage)|
|Treant|Elite|Earth|Fortify and Regeneration defender|Lv 43 / HP 1180 / P 100 / M 97 / D 81 / MD 74 / Spd 14 / Acc 84 / Eva 9 / Crit 6 / SR 14|Earth +25%|2,100 XP|403 Gold|1× Forest Herb; 1× Stone Core; 1× Crystal Shard|18%: 1 item from [Earth Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Grove Memory Shard` during `R-EDW-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-treant)|[Loot](12_Enemy_Codex.md#monster-treant)|
|Hollowroot Treant|Mini Boss|Earth,Darkness|Treant variant with stronger Barrier|Lv 45 / HP 1445 / P 123 / M 119 / D 99 / MD 90 / Spd 14 / Acc 84 / Eva 9 / Crit 6 / SR 14|Earth +25%; Darkness +25%|3,500 XP|624 Gold|1× Stone Core; 1× Magic Crystal|18%: 1 item from [Earth Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-EDW-B01`;drops `Hollowroot Bark`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-hollowroot-treant)|[Loot](12_Enemy_Codex.md#monster-hollowroot-treant)|
|Forest Witch|Elite|Earth,Darkness|Poison, Curse, and support caster|Lv 43 / HP 970 / P 72 / M 125 / D 65 / MD 73 / Spd 19 / Acc 86 / Eva 10 / Crit 6 / SR 12|Earth +25%; Darkness +25%|2,100 XP|403 Gold|1× Redcap; 1× Mana Mushroom; 1× Cursed Twig; 1× Magic Crystal|18%: 1 item from [Earth Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|No conditional Quest Item. Added as a direct source for legacy potion ingredients.|Added|[Pattern](13_Enemy_AI_Patterns.md#pattern-forest-witch)|[Loot](12_Enemy_Codex.md#monster-forest-witch)|
## Ancient Ruins — Air Region (Stage 4)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Sand Wraith|Elite|Darkness,Air|Fear and Blind magic attacker|Lv 43 / HP 970 / P 72 / M 125 / D 65 / MD 73 / Spd 19 / Acc 86 / Eva 10 / Crit 6 / SR 12|Darkness +25%; Air +25%|2,100 XP|403 Gold|1× Desert Spirit Dust; 1× Dark Crystal|18%: 1 item from [Air Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Observatory Gear Segment` during `R-AAR-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-sand-wraith)|[Loot](12_Enemy_Codex.md#monster-sand-wraith)|
|Desert Shaman|Elite|Air,Holy|Barrier,Heal,and Gale caster|Lv 43 / HP 1180 / P 68 / M 125 / D 81 / MD 82 / Spd 15 / Acc 84 / Eva 9 / Crit 6 / SR 17|Air +25%; Holy +25%|2,100 XP|403 Gold|1× Air Crystal; 1× Magic Crystal; 1× Sun Charm|18%: 1 item from [Air Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Observatory Gear Segment` during `R-AAR-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-desert-shaman)|[Loot](12_Enemy_Codex.md#monster-desert-shaman)|
|Mummy|Elite|Darkness|Poison and Curse attacker|Lv 43 / HP 970 / P 106 / M 97 / D 65 / MD 65 / Spd 18 / Acc 86 / Eva 10 / Crit 6 / SR 9|Darkness +25%|2,100 XP|403 Gold|1× Ancient Coin; 1× Cursed Twig|18%: 1 item from [Air Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Observatory Gear Segment` during `R-AAR-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-mummy)|[Loot](12_Enemy_Codex.md#monster-mummy)|
|Ashen Mummy Scribe|Mini Boss|Darkness,Air|Mummy variant with Dust Veil|Lv 45 / HP 1180 / P 129 / M 119 / D 80 / MD 80 / Spd 18 / Acc 86 / Eva 10 / Crit 6 / SR 9|Darkness +25%; Air +25%|3,500 XP|624 Gold|1× Ancient Coin; 1× Magic Crystal|18%: 1 item from [Air Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-AAR-B01`;drops `Scribe's Tablet`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ashen-mummy-scribe)|[Loot](12_Enemy_Codex.md#monster-ashen-mummy-scribe)|
|Tomb Guardian|Normal|Earth,Darkness|Defensive crypt construct|Lv 40 / HP 810 / P 70 / M 67 / D 55 / MD 51 / Spd 14 / Acc 83 / Eva 9 / Crit 6 / SR 13|Earth +25%; Darkness +25%|1,400 XP|260 Gold|1× Ancient Coin; 1× Stone Core|10%: 1 item from [Air Tier 4 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Observatory Gear Segment` during `R-AAR-C01` only.|Added|[Pattern](13_Enemy_AI_Patterns.md#pattern-tomb-guardian)|[Loot](12_Enemy_Codex.md#monster-tomb-guardian)|
## Ice Caves — Water Region (Stage 4)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Frost Spider|Normal|Water,Earth|Rooted,Freeze,and Poison attacker|Lv 40 / HP 660 / P 72 / M 67 / D 45 / MD 45 / Spd 18 / Acc 85 / Eva 9 / Crit 6 / SR 9|Water +25%; Earth +25%|1,400 XP|260 Gold|1× Spider Silk; 1× Venom Sac; 1× Frost Crystal|10%: 1 item from [Water Tier 4 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Ice Cave Survey Chip` during `R-WIC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-frost-spider)|[Loot](12_Enemy_Codex.md#monster-frost-spider)|
|Frost Mage|Normal|Water|Freeze and Barrier caster|Lv 40 / HP 810 / P 46 / M 86 / D 55 / MD 57 / Spd 14 / Acc 83 / Eva 9 / Crit 6 / SR 17|Water +25%|1,400 XP|260 Gold|1× Frost Crystal; 1× Magic Crystal|10%: 1 item from [Water Tier 4 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Ice Cave Survey Chip` during `R-WIC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-frost-mage)|[Loot](12_Enemy_Codex.md#monster-frost-mage)|
|Ice Elemental|Elite|Water|Wet and Freeze magic attacker|Lv 43 / HP 970 / P 72 / M 125 / D 65 / MD 73 / Spd 19 / Acc 86 / Eva 10 / Crit 6 / SR 12|Water +25%|2,100 XP|403 Gold|1× Ice Moss; 1× Frost Crystal|18%: 1 item from [Water Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ice-elemental)|[Loot](12_Enemy_Codex.md#monster-ice-elemental)|
|Icebound Scribe|Mini Boss|Water|Frost Mage variant with Frozen Prison|Lv 45 / HP 1180 / P 88 / M 152 / D 80 / MD 89 / Spd 19 / Acc 86 / Eva 10 / Crit 6 / SR 12|Water +25%|3,500 XP|624 Gold|1× Frost Crystal; 1× Magic Crystal|18%: 1 item from [Water Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `S-T4-03`;drops `Frozen Star Chart`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-icebound-scribe)|[Loot](12_Enemy_Codex.md#monster-icebound-scribe)|
|Icefang Matriarch|Mini Boss|Water,Earth|Frost Spider variant with strong Poison|Lv 45 / HP 1180 / P 129 / M 119 / D 80 / MD 80 / Spd 18 / Acc 86 / Eva 10 / Crit 6 / SR 9|Water +25%; Earth +25%|3,500 XP|624 Gold|1× Spider Silk; 1× Frost Crystal|18%: 1 item from [Water Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-WIC-B01`;drops `Icefang Fang`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-icefang-matriarch)|[Loot](12_Enemy_Codex.md#monster-icefang-matriarch)|
|Frost Wyrm|Normal|Water,Air|Freeze and Winded caster|Lv 40 / HP 580 / P 49 / M 86 / D 45 / MD 50 / Spd 21 / Acc 92 / Eva 15 / Crit 9 / SR 11|Water +25%; Air +25%|1,400 XP|260 Gold|1× Frost Crystal; 1× Ice Moss|10%: 1 item from [Water Tier 4 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Ice Cave Survey Chip` during `R-WIC-C01` only.|Added|[Pattern](13_Enemy_AI_Patterns.md#pattern-frost-wyrm)|[Loot](12_Enemy_Codex.md#monster-frost-wyrm)|
## Magma Forge — Fire Region (Stage 4)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Molten Golem|Elite|Fire,Earth|High Defense Fire construct|Lv 43 / HP 1180 / P 100 / M 97 / D 81 / MD 74 / Spd 14 / Acc 84 / Eva 9 / Crit 6 / SR 14|Fire +25%; Earth +25%|2,100 XP|403 Gold|1× Molten Core; 1× Obsidian Fragment|18%: 1 item from [Fire Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Forge Calibration Plate` during `R-FMF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-molten-golem)|[Loot](12_Enemy_Codex.md#monster-molten-golem)|
|Ember Wyrm|Elite|Fire|Charge and Flame Wave attacker|Lv 43 / HP 1065 / P 123 / M 97 / D 70 / MD 65 / Spd 17 / Acc 86 / Eva 10 / Crit 8 / SR 9|Fire +25%|2,100 XP|403 Gold|1× Molten Core; 1× Ember Core|18%: 1 item from [Fire Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Forge Calibration Plate` during `R-FMF-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ember-wyrm)|[Loot](12_Enemy_Codex.md#monster-ember-wyrm)|
|Forged Flame Sentinel|Mini Boss|Fire,Earth|Molten Golem variant with Flame Wave|Lv 45 / HP 1445 / P 123 / M 119 / D 99 / MD 90 / Spd 14 / Acc 84 / Eva 9 / Crit 6 / SR 14|Fire +25%; Earth +25%|3,500 XP|624 Gold|1× Molten Core; 1× Obsidian Fragment|18%: 1 item from [Fire Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-T4-04`,drops `Forge Heart Key`;during `R-FMF-B01`,spawns as Bounty and drops `Sentinel Core`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-forged-flame-sentinel)|[Loot](12_Enemy_Codex.md#monster-forged-flame-sentinel)|
## Void Rift — Darkness Region (Stage 4)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Void Golem|Elite|Darkness,Earth|High Defense void construct|Lv 43 / HP 1180 / P 100 / M 97 / D 81 / MD 74 / Spd 14 / Acc 84 / Eva 9 / Crit 6 / SR 14|Darkness +25%; Earth +25%|2,100 XP|403 Gold|1× Dark Crystal; 1× Crystal Shard|18%: 1 item from [Darkness Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Rift Stabilizer Fragment` during `R-DVR-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-void-golem)|[Loot](12_Enemy_Codex.md#monster-void-golem)|
|Shadow Drake|Elite|Darkness,Air|Shadow Mark,Fear,and Gale attacker|Lv 43 / HP 970 / P 106 / M 97 / D 65 / MD 65 / Spd 18 / Acc 86 / Eva 10 / Crit 6 / SR 9|Darkness +25%; Air +25%|2,100 XP|403 Gold|1× Dark Crystal; 1× Shadow Scale|18%: 1 item from [Darkness Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Rift Stabilizer Fragment` during `R-DVR-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-shadow-drake)|[Loot](12_Enemy_Codex.md#monster-shadow-drake)|
|Dread Knight|Elite|Darkness|Armor Break and Stun fighter|Lv 43 / HP 1065 / P 123 / M 97 / D 70 / MD 65 / Spd 17 / Acc 86 / Eva 10 / Crit 8 / SR 9|Darkness +25%|2,100 XP|403 Gold|1× Dark Crystal; 1× Iron Ore|18%: 1 item from [Darkness Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dread-knight)|[Loot](12_Enemy_Codex.md#monster-dread-knight)|
|Riftbound Echo|Mini Boss|Darkness|Void Golem variant with Soul Rend|Lv 45 / HP 1445 / P 123 / M 119 / D 99 / MD 90 / Spd 14 / Acc 84 / Eva 9 / Crit 6 / SR 14|Darkness +25%|3,500 XP|624 Gold|1× Dark Crystal; 1× Magic Crystal|18%: 1 item from [Darkness Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-T4-05`,drops `Void Compass`;during `R-DVR-B01`,spawns as Bounty and drops `Rift Echo Shard`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-riftbound-echo)|[Loot](12_Enemy_Codex.md#monster-riftbound-echo)|
## Dawn Basilica — Holy Region (Stage 4)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Dawn Seraph|Elite|Holy,Air|Haste,Barrier,Gale,and Holy caster|Lv 43 / HP 1040 / P 68 / M 125 / D 81 / MD 82 / Spd 19 / Acc 91 / Eva 14 / Crit 9 / SR 17|Holy +25%; Air +25%|2,100 XP|403 Gold|1× Holy Crystal; 1× Harpy Feather|18%: 1 item from [Holy Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Basilica Ward Fragment` during `R-HDB-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dawn-seraph)|[Loot](12_Enemy_Codex.md#monster-dawn-seraph)|
|Warden|Elite|Holy,Earth|Heavy defender with Fortify|Lv 43 / HP 1300 / P 116 / M 97 / D 86 / MD 74 / Spd 14 / Acc 84 / Eva 9 / Crit 8 / SR 14|Holy +25%; Earth +25%|2,100 XP|403 Gold|1× Holy Crystal; 1× Stone Core|18%: 1 item from [Holy Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Basilica Ward Fragment` during `R-HDB-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-warden)|[Loot](12_Enemy_Codex.md#monster-warden)|
|Fallen Seraph Amon|Mini Boss|Holy,Darkness|Dawn Seraph variant with Magic Vulnerability|Lv 45 / HP 1180 / P 88 / M 152 / D 80 / MD 89 / Spd 19 / Acc 86 / Eva 10 / Crit 6 / SR 12|Holy +25%; Darkness +25%|3,500 XP|624 Gold|1× Holy Crystal; 1× Dark Crystal|18%: 1 item from [Holy Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-T4-06`,drops `Oath Feather [Story]`;during `R-HDB-B01`,spawns as Bounty and drops `Oath Feather [Bounty]`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-fallen-seraph-amon)|[Loot](12_Enemy_Codex.md#monster-fallen-seraph-amon)|
## Frozen Peak — Water Region (Stage 5)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Mountain Beast|Normal|Earth,Water|Heavy physical attacker|Lv 55 / HP 1080 / P 119 / M 94 / D 66 / MD 62 / Spd 18 / Acc 89 / Eva 11 / Crit 9 / SR 10|Earth +25%; Water +25%|2,600 XP|520 Gold|1× Mountain Beast Claw; 1× Beast Claw|10%: 1 item from [Water Tier 5 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Peak Prayer Bead` during `R-WFP-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-mountain-beast)|[Loot](12_Enemy_Codex.md#monster-mountain-beast)|
|Stormclaw Harpy|Mini Boss|Air,Water|Harpy variant with Winded and Haste|Lv 59 / HP 1520 / P 180 / M 167 / D 108 / MD 108 / Spd 24 / Acc 97 / Eva 16 / Crit 11 / SR 10|Air +25%; Water +25%|6,500 XP|1,248 Gold|1× Harpy Feather; 1× Frost Crystal|18%: 1 item from [Water Tier 5 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-WFP-B01`;drops `Stormclaw Plume`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-stormclaw-harpy)|[Loot](12_Enemy_Codex.md#monster-stormclaw-harpy)|
|Avalanche Elemental|Elite|Water,Air,Earth|Area-control elemental caster|Lv 57 / HP 1410 / P 101 / M 175 / D 88 / MD 99 / Spd 21 / Acc 90 / Eva 12 / Crit 8 / SR 14|Water +25%; Air +25%; Earth +25%|3,900 XP|806 Gold|1× Stone Core; 1× Air Crystal; 1× Frost Crystal|18%: 1 item from [Water Tier 5 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Peak Prayer Bead` during `R-WFP-C01` only.|Added|[Pattern](13_Enemy_AI_Patterns.md#pattern-avalanche-elemental)|[Loot](12_Enemy_Codex.md#monster-avalanche-elemental)|
|Peak Guardian|Elite|Holy,Earth|Fortified protector|Lv 57 / HP 1410 / P 147 / M 137 / D 88 / MD 88 / Spd 21 / Acc 90 / Eva 12 / Crit 8 / SR 10|Holy +25%; Earth +25%|3,900 XP|806 Gold|1× Sun Charm; 1× Holy Crystal; 1× Stone Core|18%: 1 item from [Holy Tier 5 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Peak Prayer Bead` during `R-WFP-C01` only.|Added|[Pattern](13_Enemy_AI_Patterns.md#pattern-peak-guardian)|[Loot](12_Enemy_Codex.md#monster-peak-guardian)|
## King's Clearing — Earth Region (Stage 6)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Goblin King|Boss|Earth|Summoning physical and Earth boss|Lv 65 / HP 4335 / P 376 / M 351 / D 226 / MD 226 / Spd 24 / Acc 95 / Eva 13 / Crit 8 / SR 17|Earth +25%|17,000 XP|3,375 Gold|1× Crystal Shard; 1× Magic Crystal|25%: 1 item from [Earth Tier 6 Elite Pool](05_Equipment_and_Drop_Pools.md)|Drops `Earth Sigil` during `S-T6-01`;drops `King's Crown Shard` only during `R-EKC-B01`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-goblin-king)|[Loot](12_Enemy_Codex.md#monster-goblin-king)|
## Ruin Guardian Chamber — Air Region (Stage 6)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Ruin Guardian|Boss|Air,Earth,Holy|Barrier and Stun construct boss|Lv 65 / HP 5290 / P 358 / M 351 / D 280 / MD 257 / Spd 20 / Acc 93 / Eva 13 / Crit 8 / SR 23|Air +25%; Earth +25%; Holy +25%|17,000 XP|3,375 Gold|1× Air Crystal; 1× Crystal Shard; 1× Sun Charm|25%: 1 item from [Air Tier 6 Elite Pool](05_Equipment_and_Drop_Pools.md)|Drops `Air Sigil` during `S-T6-02`;drops `Guardian Core Plate` only during `R-ARGC-B01`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ruin-guardian)|[Loot](12_Enemy_Codex.md#monster-ruin-guardian)|
## Summit Shrine — Water Region (Stage 6)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Frost Titan|Boss|Water,Earth|Freeze,Slow,and Stun boss|Lv 65 / HP 4335 / P 376 / M 351 / D 226 / MD 226 / Spd 24 / Acc 95 / Eva 13 / Crit 8 / SR 17|Water +25%; Earth +25%|17,000 XP|3,375 Gold|1× Frost Crystal; 1× Magic Crystal|25%: 1 item from [Water Tier 6 Elite Pool](05_Equipment_and_Drop_Pools.md)|Drops `Water Sigil` during `S-T6-03`;drops `Titan Glacier Heart` only during `R-WSS-B01`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-frost-titan)|[Loot](12_Enemy_Codex.md#monster-frost-titan)|
## Inferno Core — Fire Region (Stage 6)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Inferno Lord|Boss|Fire,Darkness|Summoning Fire boss with Infernal Nova|Lv 65 / HP 4335 / P 376 / M 351 / D 226 / MD 226 / Spd 24 / Acc 95 / Eva 13 / Crit 8 / SR 17|Fire +25%; Darkness +25%|17,000 XP|3,375 Gold|1× Molten Core; 1× Obsidian Fragment|25%: 1 item from [Fire Tier 6 Elite Pool](05_Equipment_and_Drop_Pools.md)|Drops `Fire Sigil` during `S-T6-04`;drops `Inferno Ember` only during `R-FIC-B01`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-inferno-lord)|[Loot](12_Enemy_Codex.md#monster-inferno-lord)|
## Dread Throne — Darkness Region (Stage 6)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Shadow Lord|Boss|Darkness|Summoning Darkness boss with Voidstorm|Lv 65 / HP 4335 / P 376 / M 351 / D 226 / MD 226 / Spd 24 / Acc 95 / Eva 13 / Crit 8 / SR 17|Darkness +25%|17,000 XP|3,375 Gold|1× Dark Crystal; 1× Dragon Rune|25%: 1 item from [Darkness Tier 6 Elite Pool](05_Equipment_and_Drop_Pools.md)|Drops `Darkness Sigil` during `S-T6-05`;drops `Dread Veil Fragment` only during `R-DDT-B01`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-shadow-lord)|[Loot](12_Enemy_Codex.md#monster-shadow-lord)|
## Oracle Chamber — Holy Region (Stage 6)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Oracle|Boss|Holy|Barrier,Cleanse,Solar Verdict,and Judgment boss|Lv 65 / HP 5290 / P 358 / M 351 / D 280 / MD 257 / Spd 20 / Acc 93 / Eva 13 / Crit 8 / SR 23|Holy +25%|17,000 XP|3,375 Gold|1× Holy Crystal; 1× Dragon Rune|25%: 1 item from [Holy Tier 6 Elite Pool](05_Equipment_and_Drop_Pools.md)|Drops `Holy Sigil` during `S-T6-06`;drops `Oracle's Trial Seal` only during `R-HOC-B01`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-oracle)|[Loot](12_Enemy_Codex.md#monster-oracle)|
## Dragon Valley — Dragon King's Dominion (Stage 7)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Dragon Servant|Normal|Darkness,Fire|Darkness caster with Burn and Berserk|Lv 70 / HP 1980 / P 136 / M 206 / D 110 / MD 113 / Spd 24 / Acc 97 / Eva 15 / Crit 11 / SR 17|Darkness +25%; Fire +25%|5,000 XP|1,050 Gold|1× Dragon Rune; 1× Dark Crystal|10%: 1 item from [Dragon Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Dragonwatch Route Mark` during `R-DRDV-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dragon-servant)|[Loot](12_Enemy_Codex.md#monster-dragon-servant)|
|Dragon Whelp|Normal|Fire|Burn and Quick Attack dragon|Lv 70 / HP 1800 / P 172 / M 160 / D 101 / MD 101 / Spd 24 / Acc 97 / Eva 15 / Crit 9 / SR 14|Fire +25%|5,000 XP|1,050 Gold|1× Dragon Claw; 1× Dragon Rune|10%: 1 item from [Dragon Tier 1 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Dragonwatch Route Mark` during `R-DRDV-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dragon-whelp)|[Loot](12_Enemy_Codex.md#monster-dragon-whelp)|
|Redscale Whelp|Mini Boss|Fire|Dragon Whelp variant with stronger Burn|Lv 75 / HP 3110 / P 296 / M 278 / D 175 / MD 175 / Spd 25 / Acc 98 / Eva 15 / Crit 10 / SR 14|Fire +25%|12,500 XP|2,520 Gold|1× Dragon Claw; 1× Dragon Rune|18%: 1 item from [Dragon Tier 1 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-DRDV-B01`;drops `Redscale Horn`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-redscale-whelp)|[Loot](12_Enemy_Codex.md#monster-redscale-whelp)|
## Dragon Cave — Dragon King's Dominion (Stage 8)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Wyvern|Normal|Air,Fire|Gale,Bleeding,Burn,and Haste attacker|Lv 80 / HP 2010 / P 207 / M 194 / D 124 / MD 124 / Spd 32 / Acc 108 / Eva 21 / Crit 13 / SR 15|Air +25%; Fire +25%|7,200 XP|1,500 Gold|1× Dragon Claw; 1× Harpy Feather|10%: 1 item from [Dragon Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Cave Binding Fragment` during `R-DRDC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-wyvern)|[Loot](12_Enemy_Codex.md#monster-wyvern)|
|Dragon Archer|Normal|Air|Pinning and Piercing ranged attacker|Lv 80 / HP 2010 / P 207 / M 194 / D 124 / MD 124 / Spd 32 / Acc 108 / Eva 21 / Crit 13 / SR 15|Air +25%|7,200 XP|1,500 Gold|1× Dragon Rune; 1× Harpy Feather|10%: 1 item from [Dragon Tier 2 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Cave Binding Fragment` during `R-DRDC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dragon-archer)|[Loot](12_Enemy_Codex.md#monster-dragon-archer)|
|Bonewing Remnant|Mini Boss|Darkness,Air|Bone Dragon variant with Winded|Lv 85 / HP 3465 / P 356 / M 332 / D 212 / MD 212 / Spd 34 / Acc 108 / Eva 21 / Crit 13 / SR 15|Darkness +25%; Air +25%|18,000 XP|3,600 Gold|1× Dragon Bone; 1× Dark Crystal|18%: 1 item from [Dragon Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|Spawns only during `R-DRDC-B01`;drops `Bonewing Scale`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-bonewing-remnant)|[Loot](12_Enemy_Codex.md#monster-bonewing-remnant)|
## Dragon Cave / Ancient Nest — Dragon King's Dominion (Stage 8)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Bone Dragon|Elite|Darkness|Shadow Mark,Fear,Barrier,and Dark Bolt enemy|Lv 83 / HP 3925 / P 277 / M 273 / D 214 / MD 198 / Spd 24 / Acc 99 / Eva 15 / Crit 10 / SR 21|Darkness +25%|10,800 XP|2,325 Gold|1× Dragon Bone; 1× Dark Crystal|18%: 1 item from [Dragon Tier 2 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Nest Survey Fragment` during `R-DRAN-C01` only when encountered in Ancient Nest.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-bone-dragon)|[Loot](12_Enemy_Codex.md#monster-bone-dragon)|
## Obsidian Citadel — Dragon King's Dominion (Stage 9)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Dragon Knight|Normal|Fire,Darkness|Armor Break,Fortify,Stun,and Heavy Attack fighter|Lv 88 / HP 3790 / P 269 / M 228 / D 196 / MD 167 / Spd 22 / Acc 102 / Eva 17 / Crit 13 / SR 22|Fire +25%; Darkness +25%|10,000 XP|2,100 Gold|1× Obsidian Fragment; 1× Dragon Rune|10%: 1 item from [Dragon Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Citadel Armory Tag` during `R-DROC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dragon-knight)|[Loot](12_Enemy_Codex.md#monster-dragon-knight)|
|Dragon Priest|Normal|Holy,Fire|Cleanse,Regeneration,Heal,and Holy caster|Lv 88 / HP 2825 / P 166 / M 293 / D 147 / MD 165 / Spd 29 / Acc 104 / Eva 18 / Crit 11 / SR 20|Holy +25%; Fire +25%|10,000 XP|2,100 Gold|1× Holy Crystal; 1× Dragon Rune; 1× Dragon Relic|10%: 1 item from [Dragon Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Citadel Armory Tag` during `R-DROC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dragon-priest)|[Loot](12_Enemy_Codex.md#monster-dragon-priest)|
|Dragon Warlock|Normal|Darkness,Fire|Silence,Focus,Soul Rend,and Dark Bolt caster|Lv 88 / HP 2825 / P 166 / M 293 / D 147 / MD 165 / Spd 29 / Acc 104 / Eva 18 / Crit 11 / SR 20|Darkness +25%; Fire +25%|10,000 XP|2,100 Gold|1× Dark Crystal; 1× Dragon Rune|10%: 1 item from [Dragon Tier 3 Normal Pool](05_Equipment_and_Drop_Pools.md)|`Citadel Armory Tag` during `R-DROC-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dragon-warlock)|[Loot](12_Enemy_Codex.md#monster-dragon-warlock)|
|Obsidian Guardian|Elite|Fire,Earth|High Defense construct|Lv 91 / HP 4840 / P 326 / M 322 / D 255 / MD 235 / Spd 24 / Acc 103 / Eva 17 / Crit 11 / SR 22|Fire +25%; Earth +25%|15,000 XP|3,255 Gold|1× Obsidian Core; 1× Obsidian Fragment|18%: 1 item from [Dragon Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|None.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-obsidian-guardian)|[Loot](12_Enemy_Codex.md#monster-obsidian-guardian)|
|Obsidian Warden Korr|Mini Boss|Fire,Earth|Obsidian Guardian variant with Barrier and Stun|Lv 93 / HP 5915 / P 398 / M 394 / D 312 / MD 288 / Spd 24 / Acc 103 / Eva 17 / Crit 11 / SR 22|Fire +25%; Earth +25%|25,000 XP|5,040 Gold|1× Obsidian Core; 1× Ancient Dragon Fang|18%: 1 item from [Dragon Tier 3 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-DRAGON-03`,drops `Citadel Gate Sigil`;during `R-DROC-B01`,spawns as Bounty and drops `Warden Command Sigil`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-obsidian-warden-korr)|[Loot](12_Enemy_Codex.md#monster-obsidian-warden-korr)|
## Ancient Nest — Dragon King's Dominion (Stage 10)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Dragon Knight Captain|Elite|Fire,Darkness|Rally,Armor Break,Stun,and Fortify leader|Lv 96 / HP 5840 / P 380 / M 374 / D 300 / MD 276 / Spd 25 / Acc 106 / Eva 19 / Crit 12 / SR 23|Fire +25%; Darkness +25%|20,500 XP|4,340 Gold|1× Dragon Rune; 1× Obsidian Fragment; 1× Dragon Relic|18%: 1 item from [Dragon Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|`Nest Survey Fragment` during `R-DRAN-C01` only.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dragon-knight-captain)|[Loot](12_Enemy_Codex.md#monster-dragon-knight-captain)|
|Ancient Dragon|Boss|Fire,Air,Darkness|Dragonfire Breath,Storm Wing,Eclipse,and Scale Harden boss|Lv 98 / HP 12560 / P 889 / M 835 / D 538 / MD 538 / Spd 31 / Acc 109 / Eva 20 / Crit 12 / SR 24|Fire +25%; Air +25%; Darkness +25%|54,000 XP|12,600 Gold|1× Ancient Dragon Scale; 1× Ancient Dragon Fang; 1× Dragon Rune; 1× Mythic Ember|25%: 1 item from [Dragon Tier 4 Elite Pool](05_Equipment_and_Drop_Pools.md)|During `S-DRAGON-04`,drops `Ancient Memory Scale`;during `R-DRAN-B01`,drops `Ancient Dragon Memory Scale`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-ancient-dragon)|[Loot](12_Enemy_Codex.md#monster-ancient-dragon)|
## Dragon King's Lair — Dragon King's Dominion (Stage 11)

|Enemy|Implementation Rank|Elements|Combat role|Base Stats|Element resistance|XP|Gold|Guaranteed materials|Equipment roll|Conditional Quest/Proof drop|Origin|AI Pattern|Full Crafting Loot|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Dragon King|Final Boss|Fire,Air,Darkness|Final multi-element boss|Lv 100 / HP 21500 / P 1080 / M 1015 / D 620 / MD 620 / Spd 34 / Acc 112 / Eva 22 / Crit 15 / SR 30|Fire +25%; Air +25%; Darkness +25%|0 XP|0 Gold|None|None|Spawns only for `S-DRAGON-05`;drops only `Dragon King's Seal`.|Existing|[Pattern](13_Enemy_AI_Patterns.md#pattern-dragon-king)|[Loot](12_Enemy_Codex.md#monster-dragon-king)|

## Added active enemy entries

|Enemy|Why added|System integration|
|---|---|---|
|Goblin Bomber|`Bomb Powder` recipe source was named but no active enemy existed.|Loot, AI, Goblin Forest encounter, and `R-EGF-K05`.|
|Sand Wolf|Legacy ingredient source needed a current roster enemy.|Loot, AI, Scorching Dunes encounter, and `R-ASD-K03`.|
|Forest Witch|Legacy Redcap/Mana/Cursed ingredient source needed an active current enemy.|Loot, AI, Deep Woods encounter, and `R-EDW-K04`.|
|Frost Wyrm|Legacy Frost Crystal source needed current roster coverage.|Loot, AI, Ice Caves encounter, and `R-WIC-K04`.|
|Tomb Guardian|Legacy Ancient Coin source needed current roster coverage.|Loot, AI, Ancient Ruins encounter, and `R-AAR-K04`.|
|Avalanche Elemental|Legacy Stone Core/Air Crystal source needed current roster coverage.|Loot, AI, Frozen Peak encounter, and `R-WFP-K03`.|
|Peak Guardian|Legacy Sun Charm source needed current roster coverage.|Loot, AI, Frozen Peak encounter, and `R-WFP-K04`.|

## Dual-area entities

|Enemy|Rule|
|---|---|
|Ashfang Hound|Uses Stage 2 baseline for its Story fight in Ember Fields; its Tier 1 bounty spawn in Ashen Border applies the area encounter scaling modifier.|
|Bone Dragon|Uses Dragon Cave Stage 8 baseline; when encountered in Ancient Nest, apply the Ancient Nest encounter scaling modifier before combat.|

The original descriptive loot tables are preserved in [Source_Enemy_Loot_Tables_Updated.md](Source_Enemy_Loot_Tables_Updated.md).

## Balance 2.0 Codex additions

- Every enemy row now has an `AI Pattern` link to a stable, individual anchor in [Individual Enemy Pattern Links](13_Enemy_AI_Patterns.md).
- Every enemy row now has a `Full Crafting Loot` link. That page combines exact guaranteed materials with any independent supplemental crafting rolls and proves direct Monster Loot coverage for every craft input.
- Levels, stats, XP, and Gold have been rebased to the Level 1–100 progression model. See [Progression, XP, and Level Balance](02_Attributes_and_Combat.md).

## Revised XP and Gold reward bands

|Area stage|Normal XP|Elite XP|Mini Boss XP|Boss XP|Normal Gold|
|---:|---:|---:|---:|---:|---:|
|1|140|220|360|600|28|
|2|320|500|820|1,300|60|
|3|700|1,050|1,750|2,800|130|
|4|1,400|2,100|3,500|5,600|260|
|5|2,600|3,900|6,500|10,500|520|
|6|4,200|6,300|10,500|17,000|750|
|7|5,000|7,500|12,500|20,000|1,050|
|8|7,200|10,800|18,000|28,800|1,500|
|9|10,000|15,000|25,000|40,000|2,100|
|10|13,500|20,500|34,000|54,000|2,800|
|11|0|0|0|0|0|

Elite Gold is 1.55× Normal Gold, Mini Boss Gold is 2.4×, and Boss Gold is 4.5×, rounded to the nearest whole Gold. This enables the slower Level 1–100 curve while retaining a clear farm/reward relationship. Dragon King grants no direct XP or Gold by design.

## Supplemental crafting loot profiles

Each Codex enemy row links here. `Guaranteed` duplicates the exact Codex material award. `Supplemental` is an independent extra roll added by this revision. The absence of a supplemental row means that the existing guaranteed materials are the complete crafting profile for that monster.

## Forest Entrance — Earth Region (Stage 1)

<a id="monster-forest-rat"></a>
### Forest Rat

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Forest Herb|1|100%|
|Guaranteed|Iron Scrap|1|100%|

<a id="monster-wild-boar"></a>
### Wild Boar

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Beast Claw|1|100%|
|Guaranteed|Forest Herb|1|100%|

<a id="monster-barkhide-boar"></a>
### Barkhide Boar

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Beast Claw|1|100%|
|Guaranteed|Iron Scrap|1|100%|
|Supplemental|Enchantment Dust|1|35%|

## Desert Border — Air Region (Stage 1)

<a id="monster-desert-rat"></a>
### Desert Rat

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Cactus Sap|1|100%|

<a id="monster-sand-beetle"></a>
### Sand Beetle

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Iron Ore|1|100%|
|Guaranteed|Beetle Shell|1|100%|

<a id="monster-dustrunner-scarab"></a>
### Dustrunner Scarab

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Iron Ore|1|100%|
|Guaranteed|Air Crystal|1|100%|
|Supplemental|Enchantment Dust|1|35%|

## Mountain Foothills — Water Region (Stage 1)

<a id="monster-snow-wolf"></a>
### Snow Wolf

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ice Moss|1|100%|
|Guaranteed|Beast Claw|1|100%|

<a id="monster-ice-bat"></a>
### Ice Bat

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Frost Crystal|1|100%|
|Guaranteed|Ice Moss|1|100%|

<a id="monster-whitefang-alpha"></a>
### Whitefang Alpha

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ice Moss|1|100%|
|Guaranteed|Beast Claw|1|100%|
|Supplemental|Enchantment Dust|1|35%|

## Ashen Border — Fire Region (Stage 1)

<a id="monster-ash-lizard"></a>
### Ash Lizard

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ember Core|1|100%|
|Guaranteed|Beast Claw|1|100%|

<a id="monster-ember-hound"></a>
### Ember Hound

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ember Core|1|100%|
|Guaranteed|Beast Claw|1|100%|

## Gloomwood — Darkness Region (Stage 1)

<a id="monster-shade"></a>
### Shade

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Cursed Twig|1|100%|
|Guaranteed|Mana Mushroom|1|100%|

<a id="monster-bone-hound"></a>
### Bone Hound

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Beast Claw|1|100%|
|Guaranteed|Cursed Twig|1|100%|

<a id="monster-lantern-shade"></a>
### Lantern Shade

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Cursed Twig|1|100%|
|Guaranteed|Dark Crystal|1|100%|
|Supplemental|Enchantment Dust|1|35%|

## Sunlit Road — Holy Region (Stage 1)

<a id="monster-sun-acolyte"></a>
### Sun Acolyte

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Forest Herb|1|100%|

<a id="monster-temple-squire"></a>
### Temple Squire

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Iron Ore|1|100%|

<a id="monster-sunwing-hawk"></a>
### Sunwing Hawk

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Harpy Feather|1|100%|
|Supplemental|Enchantment Dust|1|35%|

## Goblin Forest — Earth Region (Stage 2)

<a id="monster-goblin-scout"></a>
### Goblin Scout

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Forest Herb|1|100%|
|Guaranteed|Iron Scrap|1|100%|
|Supplemental|Empty Bottle|1|20%|

<a id="monster-goblin-dagger"></a>
### Goblin Dagger

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Beast Claw|1|100%|
|Guaranteed|Iron Scrap|1|100%|

<a id="monster-goblin-archer"></a>
### Goblin Archer

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Harpy Feather|1|100%|
|Guaranteed|Iron Scrap|1|100%|

<a id="monster-goblin-shaman"></a>
### Goblin Shaman

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Iron Ore|1|100%|
|Guaranteed|Mana Mushroom|1|100%|
|Guaranteed|Magic Crystal|1|100%|
|Supplemental|Redcap|1|30%|

<a id="monster-totem-bound-goblin"></a>
### Totem-Bound Goblin

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Iron Ore|1|100%|
|Guaranteed|Magic Crystal|1|100%|

<a id="monster-boneknife-skulk"></a>
### Boneknife Skulk

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Iron Ore|1|100%|
|Guaranteed|Beast Claw|1|100%|
|Supplemental|Enchantment Fragment|1|35%|

<a id="monster-goblin-bomber"></a>
### Goblin Bomber

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Bomb Powder|1|100%|
|Guaranteed|Iron Scrap|1|100%|
|Supplemental|Empty Oil Flask|1|50%|

## Scorching Dunes — Air Region (Stage 2)

<a id="monster-sand-scorpion"></a>
### Sand Scorpion

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Venom Sac|1|100%|
|Guaranteed|Scorpion Tail|1|100%|

<a id="monster-vulture"></a>
### Vulture

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Harpy Feather|1|100%|
|Guaranteed|Air Crystal|1|100%|

<a id="monster-glasswing-vulture"></a>
### Glasswing Vulture

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Harpy Feather|1|100%|
|Guaranteed|Air Crystal|1|100%|
|Supplemental|Enchantment Fragment|1|35%|

<a id="monster-sand-wolf"></a>
### Sand Wolf

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Beast Claw|1|100%|
|Guaranteed|Cactus Sap|1|100%|

## Mountain Pass — Water Region (Stage 2)

<a id="monster-rock-crawler"></a>
### Rock Crawler

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Iron Ore|1|100%|
|Guaranteed|Stone Core|1|100%|

<a id="monster-harpy"></a>
### Harpy

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Harpy Feather|1|100%|
|Guaranteed|Air Crystal|1|100%|

<a id="monster-echo-stalker"></a>
### Echo Stalker

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Crystal Shard|1|100%|
|Guaranteed|Dark Crystal|1|100%|
|Supplemental|Enchantment Fragment|1|35%|

## Ashen Border / Ember Fields — Fire Region (Stage 2)

<a id="monster-ashfang-hound"></a>
### Ashfang Hound

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ember Core|1|100%|
|Guaranteed|Beast Claw|1|100%|
|Supplemental|Enchantment Dust|1|35%|

## Ember Fields — Fire Region (Stage 2)

<a id="monster-lava-slime"></a>
### Lava Slime

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Obsidian Fragment|1|100%|
|Guaranteed|Ember Core|1|100%|
|Guaranteed|Fire Essence|1|100%|

<a id="monster-magma-beetle"></a>
### Magma Beetle

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Obsidian Fragment|1|100%|
|Guaranteed|Iron Ore|1|100%|
|Supplemental|Beetle Shell|1|40%|

<a id="monster-ash-cultist"></a>
### Ash Cultist

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ember Core|1|100%|
|Guaranteed|Cursed Twig|1|100%|
|Supplemental|Tattered Cloth|1|35%|

<a id="monster-magmaheart-slime"></a>
### Magmaheart Slime

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Obsidian Fragment|1|100%|
|Guaranteed|Ember Core|1|100%|
|Supplemental|Enchantment Fragment|1|35%|

## Shadow Marsh — Darkness Region (Stage 2)

<a id="monster-shadow-spider"></a>
### Shadow Spider

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Venom Sac|1|100%|
|Guaranteed|Spider Silk|1|100%|

<a id="monster-dark-wolf"></a>
### Dark Wolf

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Beast Claw|1|100%|
|Guaranteed|Dark Crystal|1|100%|

<a id="monster-bogshade-huntress"></a>
### Bogshade Huntress

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Venom Sac|1|100%|
|Guaranteed|Dark Crystal|1|100%|
|Supplemental|Enchantment Fragment|1|35%|

## Temple Gardens — Holy Region (Stage 2)

<a id="monster-radiant-hawk"></a>
### Radiant Hawk

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Harpy Feather|1|100%|
|Guaranteed|Holy Crystal|1|100%|

<a id="monster-light-sprite"></a>
### Light Sprite

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Mana Mushroom|1|100%|

<a id="monster-sacred-treant"></a>
### Sacred Treant

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Stone Core|1|100%|

<a id="monster-blighted-blossom"></a>
### Blighted Blossom

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Magic Crystal|1|100%|
|Supplemental|Enchantment Fragment|1|35%|

## Overgrown Trail — Earth Region (Stage 3)

<a id="monster-moss-spider"></a>
### Moss Spider

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Spider Silk|1|100%|
|Guaranteed|Venom Sac|1|100%|

<a id="monster-thorn-beast"></a>
### Thorn Beast

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Forest Herb|1|100%|
|Guaranteed|Beast Claw|1|100%|
|Guaranteed|Crystal Shard|1|100%|

<a id="monster-fungus"></a>
### Fungus

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Mana Mushroom|1|100%|
|Guaranteed|Redcap|1|100%|
|Guaranteed|Cursed Twig|1|100%|

<a id="monster-thorn-matriarch"></a>
### Thorn Matriarch

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Spider Silk|1|100%|
|Guaranteed|Stone Core|1|100%|

<a id="monster-webmother-nyss"></a>
### Webmother Nyss

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Spider Silk|1|100%|
|Guaranteed|Venom Sac|1|100%|
|Supplemental|Enchantment Crystal|1|35%|

## Bandit Camp — Air Region (Stage 3)

<a id="monster-bandit-scout"></a>
### Bandit Scout

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Iron Ore|1|100%|
|Guaranteed|Tattered Cloth|1|100%|
|Supplemental|Iron Scrap|1|30%|
|Supplemental|Empty Bottle|1|25%|

<a id="monster-sand-raider"></a>
### Sand Raider

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Iron Ore|1|100%|
|Guaranteed|Beast Claw|1|100%|
|Supplemental|Tattered Cloth|1|55%|

<a id="monster-bandit-archer"></a>
### Bandit Archer

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Harpy Feather|1|100%|
|Guaranteed|Iron Ore|1|100%|

<a id="monster-bandit-alchemist"></a>
### Bandit Alchemist

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Cactus Sap|1|100%|
|Guaranteed|Magic Crystal|1|100%|
|Guaranteed|Bomb Powder|1|100%|
|Supplemental|Empty Oil Flask|1|40%|

<a id="monster-dune-captain-kharif"></a>
### Dune Captain Kharif

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Iron Ore|1|100%|
|Guaranteed|Air Crystal|1|100%|
|Supplemental|Enchantment Crystal|1|35%|

## Echo Mine — Water Region (Stage 3)

<a id="monster-crystal-beetle"></a>
### Crystal Beetle

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Crystal Shard|1|100%|
|Guaranteed|Iron Ore|1|100%|
|Supplemental|Beetle Shell|1|40%|

<a id="monster-mine-wraith"></a>
### Mine Wraith

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dark Crystal|1|100%|
|Guaranteed|Crystal Shard|1|100%|

<a id="monster-stone-golem"></a>
### Stone Golem

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Stone Core|1|100%|
|Guaranteed|Iron Ore|1|100%|
|Supplemental|Crystal Shard|1|35%|

<a id="monster-quartzback-golem"></a>
### Quartzback Golem

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Stone Core|1|100%|
|Guaranteed|Crystal Shard|1|100%|
|Supplemental|Enchantment Crystal|1|35%|

## Lava Fissures — Fire Region (Stage 3)

<a id="monster-flame-elemental"></a>
### Flame Elemental

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Molten Core|1|100%|
|Guaranteed|Ember Core|1|100%|
|Guaranteed|Fire Essence|1|100%|

<a id="monster-cinder-witch"></a>
### Cinder Witch

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Molten Core|1|100%|
|Guaranteed|Dark Crystal|1|100%|
|Supplemental|Fire Essence|1|45%|
|Supplemental|Empty Oil Flask|1|35%|

<a id="monster-fire-drake"></a>
### Fire Drake

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Molten Core|1|100%|
|Guaranteed|Ember Core|1|100%|
|Guaranteed|Fire Essence|1|100%|

<a id="monster-embermaw-lizard"></a>
### Embermaw Lizard

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Molten Core|1|100%|
|Guaranteed|Beast Claw|1|100%|
|Supplemental|Enchantment Crystal|1|35%|

## Forgotten Crypt — Darkness Region (Stage 3)

<a id="monster-grave-wraith"></a>
### Grave Wraith

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Cursed Twig|1|100%|
|Guaranteed|Dark Crystal|1|100%|

<a id="monster-plague-mummy"></a>
### Plague Mummy

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Venom Sac|1|100%|
|Guaranteed|Cursed Twig|1|100%|

<a id="monster-night-hag"></a>
### Night Hag

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dark Crystal|1|100%|
|Guaranteed|Mana Mushroom|1|100%|
|Supplemental|Cursed Twig|1|45%|

<a id="monster-gravebound-knight-arct"></a>
### Gravebound Knight Arct

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dark Crystal|1|100%|
|Guaranteed|Crystal Shard|1|100%|
|Supplemental|Enchantment Crystal|1|35%|

## Sanctum Halls — Holy Region (Stage 3)

<a id="monster-stone-guardian"></a>
### Stone Guardian

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ancient Coin|1|100%|
|Guaranteed|Crystal Shard|1|100%|

<a id="monster-sun-priest"></a>
### Sun Priest

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Magic Crystal|1|100%|

<a id="monster-inquisitor"></a>
### Inquisitor

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ancient Coin|1|100%|
|Guaranteed|Holy Crystal|1|100%|

<a id="monster-veiled-inquisitor-sorn"></a>
### Veiled Inquisitor Sorn

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ancient Coin|1|100%|
|Guaranteed|Holy Crystal|1|100%|
|Supplemental|Enchantment Crystal|1|35%|

## Deep Woods — Earth Region (Stage 4)

<a id="monster-goblin-mage"></a>
### Goblin Mage

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Magic Crystal|1|100%|
|Guaranteed|Mana Mushroom|1|100%|

<a id="monster-treant"></a>
### Treant

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Forest Herb|1|100%|
|Guaranteed|Stone Core|1|100%|
|Guaranteed|Crystal Shard|1|100%|

<a id="monster-hollowroot-treant"></a>
### Hollowroot Treant

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Stone Core|1|100%|
|Guaranteed|Magic Crystal|1|100%|
|Supplemental|Enchantment Crystal|1|40%|

<a id="monster-forest-witch"></a>
### Forest Witch

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Redcap|1|100%|
|Guaranteed|Mana Mushroom|1|100%|
|Guaranteed|Cursed Twig|1|100%|
|Guaranteed|Magic Crystal|1|100%|

## Ancient Ruins — Air Region (Stage 4)

<a id="monster-sand-wraith"></a>
### Sand Wraith

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Desert Spirit Dust|1|100%|
|Guaranteed|Dark Crystal|1|100%|

<a id="monster-desert-shaman"></a>
### Desert Shaman

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Air Crystal|1|100%|
|Guaranteed|Magic Crystal|1|100%|
|Guaranteed|Sun Charm|1|100%|

<a id="monster-mummy"></a>
### Mummy

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ancient Coin|1|100%|
|Guaranteed|Cursed Twig|1|100%|
|Supplemental|Desert Spirit Dust|1|30%|

<a id="monster-ashen-mummy-scribe"></a>
### Ashen Mummy Scribe

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ancient Coin|1|100%|
|Guaranteed|Magic Crystal|1|100%|
|Supplemental|Desert Spirit Dust|1|60%|

<a id="monster-tomb-guardian"></a>
### Tomb Guardian

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ancient Coin|1|100%|
|Guaranteed|Stone Core|1|100%|

## Ice Caves — Water Region (Stage 4)

<a id="monster-frost-spider"></a>
### Frost Spider

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Spider Silk|1|100%|
|Guaranteed|Venom Sac|1|100%|
|Guaranteed|Frost Crystal|1|100%|
|Supplemental|Ice Moss|1|30%|

<a id="monster-frost-mage"></a>
### Frost Mage

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Frost Crystal|1|100%|
|Guaranteed|Magic Crystal|1|100%|

<a id="monster-ice-elemental"></a>
### Ice Elemental

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ice Moss|1|100%|
|Guaranteed|Frost Crystal|1|100%|

<a id="monster-icebound-scribe"></a>
### Icebound Scribe

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Frost Crystal|1|100%|
|Guaranteed|Magic Crystal|1|100%|

<a id="monster-icefang-matriarch"></a>
### Icefang Matriarch

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Spider Silk|1|100%|
|Guaranteed|Frost Crystal|1|100%|
|Supplemental|Enchantment Crystal|1|40%|

<a id="monster-frost-wyrm"></a>
### Frost Wyrm

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Frost Crystal|1|100%|
|Guaranteed|Ice Moss|1|100%|

## Magma Forge — Fire Region (Stage 4)

<a id="monster-molten-golem"></a>
### Molten Golem

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Molten Core|1|100%|
|Guaranteed|Obsidian Fragment|1|100%|

<a id="monster-ember-wyrm"></a>
### Ember Wyrm

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Molten Core|1|100%|
|Guaranteed|Ember Core|1|100%|

<a id="monster-forged-flame-sentinel"></a>
### Forged Flame Sentinel

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Molten Core|1|100%|
|Guaranteed|Obsidian Fragment|1|100%|

## Void Rift — Darkness Region (Stage 4)

<a id="monster-void-golem"></a>
### Void Golem

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dark Crystal|1|100%|
|Guaranteed|Crystal Shard|1|100%|

<a id="monster-shadow-drake"></a>
### Shadow Drake

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dark Crystal|1|100%|
|Guaranteed|Shadow Scale|1|100%|

<a id="monster-dread-knight"></a>
### Dread Knight

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dark Crystal|1|100%|
|Guaranteed|Iron Ore|1|100%|

<a id="monster-riftbound-echo"></a>
### Riftbound Echo

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dark Crystal|1|100%|
|Guaranteed|Magic Crystal|1|100%|

## Dawn Basilica — Holy Region (Stage 4)

<a id="monster-dawn-seraph"></a>
### Dawn Seraph

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Harpy Feather|1|100%|

<a id="monster-warden"></a>
### Warden

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Stone Core|1|100%|

<a id="monster-fallen-seraph-amon"></a>
### Fallen Seraph Amon

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Dark Crystal|1|100%|

## Frozen Peak — Water Region (Stage 5)

<a id="monster-mountain-beast"></a>
### Mountain Beast

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Mountain Beast Claw|1|100%|
|Guaranteed|Beast Claw|1|100%|
|Supplemental|Stone Core|1|45%|

<a id="monster-stormclaw-harpy"></a>
### Stormclaw Harpy

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Harpy Feather|1|100%|
|Guaranteed|Frost Crystal|1|100%|
|Supplemental|Air Crystal|1|65%|

<a id="monster-avalanche-elemental"></a>
### Avalanche Elemental

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Stone Core|1|100%|
|Guaranteed|Air Crystal|1|100%|
|Guaranteed|Frost Crystal|1|100%|

<a id="monster-peak-guardian"></a>
### Peak Guardian

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Sun Charm|1|100%|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Stone Core|1|100%|

## King's Clearing — Earth Region (Stage 6)

<a id="monster-goblin-king"></a>
### Goblin King

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Crystal Shard|1|100%|
|Guaranteed|Magic Crystal|1|100%|

## Ruin Guardian Chamber — Air Region (Stage 6)

<a id="monster-ruin-guardian"></a>
### Ruin Guardian

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Air Crystal|1|100%|
|Guaranteed|Crystal Shard|1|100%|
|Guaranteed|Sun Charm|1|100%|

## Summit Shrine — Water Region (Stage 6)

<a id="monster-frost-titan"></a>
### Frost Titan

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Frost Crystal|1|100%|
|Guaranteed|Magic Crystal|1|100%|

## Inferno Core — Fire Region (Stage 6)

<a id="monster-inferno-lord"></a>
### Inferno Lord

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Molten Core|1|100%|
|Guaranteed|Obsidian Fragment|1|100%|

## Dread Throne — Darkness Region (Stage 6)

<a id="monster-shadow-lord"></a>
### Shadow Lord

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dark Crystal|1|100%|
|Guaranteed|Dragon Rune|1|100%|

## Oracle Chamber — Holy Region (Stage 6)

<a id="monster-oracle"></a>
### Oracle

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Dragon Rune|1|100%|

## Dragon Valley — Dragon King's Dominion (Stage 7)

<a id="monster-dragon-servant"></a>
### Dragon Servant

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dragon Rune|1|100%|
|Guaranteed|Dark Crystal|1|100%|
|Supplemental|Empty Bottle|1|20%|

<a id="monster-dragon-whelp"></a>
### Dragon Whelp

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dragon Claw|1|100%|
|Guaranteed|Dragon Rune|1|100%|

<a id="monster-redscale-whelp"></a>
### Redscale Whelp

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dragon Claw|1|100%|
|Guaranteed|Dragon Rune|1|100%|

## Dragon Cave — Dragon King's Dominion (Stage 8)

<a id="monster-wyvern"></a>
### Wyvern

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dragon Claw|1|100%|
|Guaranteed|Harpy Feather|1|100%|

<a id="monster-dragon-archer"></a>
### Dragon Archer

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dragon Rune|1|100%|
|Guaranteed|Harpy Feather|1|100%|

<a id="monster-bonewing-remnant"></a>
### Bonewing Remnant

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dragon Bone|1|100%|
|Guaranteed|Dark Crystal|1|100%|
|Supplemental|Shadow Scale|1|60%|

## Dragon Cave / Ancient Nest — Dragon King's Dominion (Stage 8)

<a id="monster-bone-dragon"></a>
### Bone Dragon

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dragon Bone|1|100%|
|Guaranteed|Dark Crystal|1|100%|
|Supplemental|Shadow Scale|1|45%|

## Obsidian Citadel — Dragon King's Dominion (Stage 9)

<a id="monster-dragon-knight"></a>
### Dragon Knight

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Obsidian Fragment|1|100%|
|Guaranteed|Dragon Rune|1|100%|

<a id="monster-dragon-priest"></a>
### Dragon Priest

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Holy Crystal|1|100%|
|Guaranteed|Dragon Rune|1|100%|
|Guaranteed|Dragon Relic|1|100%|

<a id="monster-dragon-warlock"></a>
### Dragon Warlock

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dark Crystal|1|100%|
|Guaranteed|Dragon Rune|1|100%|

<a id="monster-obsidian-guardian"></a>
### Obsidian Guardian

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Obsidian Core|1|100%|
|Guaranteed|Obsidian Fragment|1|100%|

<a id="monster-obsidian-warden-korr"></a>
### Obsidian Warden Korr

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Obsidian Core|1|100%|
|Guaranteed|Ancient Dragon Fang|1|100%|

## Ancient Nest — Dragon King's Dominion (Stage 10)

<a id="monster-dragon-knight-captain"></a>
### Dragon Knight Captain

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Dragon Rune|1|100%|
|Guaranteed|Obsidian Fragment|1|100%|
|Guaranteed|Dragon Relic|1|100%|

<a id="monster-ancient-dragon"></a>
### Ancient Dragon

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|Guaranteed|Ancient Dragon Scale|1|100%|
|Guaranteed|Ancient Dragon Fang|1|100%|
|Guaranteed|Dragon Rune|1|100%|
|Guaranteed|Mythic Ember|1|100%|

## Dragon King's Lair — Dragon King's Dominion (Stage 11)

<a id="monster-dragon-king"></a>
### Dragon King

|Loot type|Item|Quantity|Chance|
|---|---|---:|---:|
|None|No crafting material|0|0%|

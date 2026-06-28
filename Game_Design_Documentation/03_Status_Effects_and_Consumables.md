# Status Effects, Potions, Oils, Ingredients, and Crafting

## Linked documents

[Combat formulas](02_Attributes_and_Combat.md) · [Player skills](04_Player_and_Skills.md) · [Item prices](06_Item_Price_Catalog.md) · [Market and Alchemy](07_Economy_Market_and_Alchemy.md) · [Enemy Codex](12_Enemy_Codex.md)

## Canonical effect register

|Effect|Type|Exact result|Default duration|Removal|
|---|---|---|---|---|
|Burn|DoT|End of target action: Fire Magic DoT at stored Magic Power × 0.45.|3 own actions|Burn Salve; Purifying Potion|
|Poison|DoT|End of target action: Neutral DoT at stored Magic Power × 0.35; ignores 50% Defense.|3 own actions|Antidote; Purifying Potion|
|Bleeding|DoT|Triggers after target uses a Physical Skill or takes a Physical critical hit: stored PAtk × 0.45.|3 own actions|Bandage; Purifying Potion|
|Curse|DoT|End of target action: Darkness Magic DoT at stored Magic Power × 0.40.|3 own actions|Mind Tonic; Purifying Potion|
|Stun|Control|Cannot choose an action.|1 own action|Awakening; Purifying|
|Sleep|Control|Cannot choose an action; ends early when damaged.|1 own action|Awakening; Purifying|
|Freeze|Control|Cannot choose an action.|1 own action|Awakening; Purifying|
|Confusion|Control|Random valid action/target is selected.|1 own action|Mind Tonic; Purifying|
|Fear|Control|Cannot use offensive skills or attacks.|1 own action|Mind Tonic; Purifying|
|Silence|Control|Cannot use Staff or Elemental Magic Skills.|1 own action|Mind Tonic; Purifying|
|Rooted|Control|Cannot evade; Speed -25%.|2 own actions|Purifying|
|Weakness|Debuff|Physical Attack -20%.|2 own actions|Purifying|
|Magic Break|Debuff|Magic Power -20%.|2 own actions|Purifying|
|Armor Break|Debuff|Defense -20%.|2 own actions|Purifying|
|Magic Vulnerability|Debuff|Magical Defense -20%.|2 own actions|Purifying|
|Blind|Debuff|Accuracy -20.|2 own actions|Mind Tonic; Purifying|
|Slow|Debuff|Speed -25%.|2 own actions|Purifying|
|Crippled|Debuff|Speed -20%; Physical Attack -15%.|2 own actions|Purifying|
|Wet|Setup|Incoming Water Damage +20%; enables named Water/Air Skill bonuses.|2 own actions|Purifying|
|Scorched|Setup|Incoming Fire Damage +20%; Healing Received -25%.|2 own actions|Purifying|
|Cracked|Setup|Incoming Physical Damage +15%; Defense -15%.|2 own actions|Purifying|
|Winded|Setup|Accuracy -15; Evasion -15%.|2 own actions|Purifying|
|Shadow Mark|Setup|Incoming Darkness Damage +20%; Healing Received -20%.|2 own actions|Mind Tonic; Purifying|
|Holy Mark|Setup|Incoming Holy Damage +20%; prevents named Darkness synergies.|2 own actions|Purifying|
|Regeneration|Positive|Restore its listed HP amount at end of own action.|Listed source duration|—|
|Mana Regeneration|Positive|Restore its listed MP amount at end of own action.|Listed source duration|—|
|Barrier|Positive|Absorbs Damage until depleted or duration ends.|Listed source duration|—|
|Haste|Positive|Increases Speed by listed percentage.|Listed source duration|—|
|Focus|Positive|Increases Magic Power and Accuracy by listed amounts.|Listed source duration|—|
|Magic Ward|Positive|Increases Magical Defense by listed percentage.|Listed source duration|—|
|Fortify|Positive|Increases Defense and Magical Defense by listed percentage.|Listed source duration|—|
|Berserk|Positive|Increases Physical Attack; lowers Defense by listed values.|Listed source duration|—|
|Evasion Up|Positive|Increases Evasion by listed percentage points.|Listed source duration|—|
|Lifesteal|Positive|Heals from post-Barrier direct Health Damage only.|Listed source duration|—|
|Elemental Ward|Positive|First elemental hit selects its protected element; gain listed Resistance for remaining duration.|Listed source duration|—|
|Damage Reduction|Positive|Final incoming Damage is reduced by listed percentage; 75% total cap.|Listed source duration|—|

<a id="potion-action-reuse-and-duration-rules"></a>
## Potion action, reuse, and duration rules

|Rule|Canonical implementation|
|---|---|
|Potion action|Using any Potion or medicine consumes the Player's action unless `Alchemist's Pouch` explicitly grants its once-per-battle extra use.|
|Recovery reuse|After Small/Health/Greater/Full Health, Small/Mana/Greater/Full Mana, or Rejuvenation use, the Player receives `Recovery Item Cooldown` for **2 own actions**. Another recovery Potion cannot be used while it remains.|
|Medicine and buffs|Status medicines, buff Potions, resistance Potions, and Oils do not share the recovery cooldown, but still require an action.|
|Temporary effects|A temporary Potion effect is **not** whole-battle. Its exact duration is in the table below and counts down on the Player's own completed actions.|
|Oils|Apply outside combat or as a pre-combat preparation action. An Oil lasts for **3 Player own actions** or until combat ends, whichever happens first.|
|One use limit|The same named consumable cannot be used twice during the same Player action, including through `Alchemist's Pouch`.|
|Smoke Bomb / Recall|Utilities, not Potions. Smoke Bomb cannot escape Mini Boss, Boss, Final Boss, or story-locked encounters; Recall is out of combat only.|

## Exact consumable effects

Normal recovery uses **fixed values**, not Max-HP/Max-MP percentages. This keeps low Potions relevant at the start without making four shop Potions restore a full endgame health bar.

|Item|Acquisition|Exact effect|Duration / limit|
|---|---|---|---|
|Small Health Potion|Market or craft|Restore **45 HP**.|Immediate; Recovery Item Cooldown 2 own actions.|
|Health Potion|Craft only|Restore **120 HP**.|Immediate; Recovery Item Cooldown 2 own actions.|
|Greater Health Potion|Craft only|Restore **300 HP**.|Immediate; Recovery Item Cooldown 2 own actions.|
|Full Health Potion|Endgame craft only|Restore all missing HP; remove Burn.|Immediate; Recovery Item Cooldown 2 own actions.|
|Small Mana Potion|Market or craft|Restore **18 MP**.|Immediate; Recovery Item Cooldown 2 own actions.|
|Mana Potion|Craft only|Restore **55 MP**.|Immediate; Recovery Item Cooldown 2 own actions.|
|Greater Mana Potion|Craft only|Restore **140 MP**.|Immediate; Recovery Item Cooldown 2 own actions.|
|Full Mana Potion|Endgame craft only|Restore all missing MP; remove Silence.|Immediate; Recovery Item Cooldown 2 own actions.|
|Rejuvenation Potion|Craft only|Restore **90 HP** and **45 MP**.|Immediate; Recovery Item Cooldown 2 own actions.|
|Greater Rejuvenation Potion|Endgame craft only|Restore **260 HP** and **130 MP**.|Immediate; Recovery Item Cooldown 2 own actions.|
|Antidote|Craft only|Remove Poison.|Immediate.|
|Bandage|Craft only|Remove Bleeding.|Immediate.|
|Burn Salve|Craft only|Remove Burn; gain +10% Fire Resistance.|2 own actions.|
|Mind Tonic|Craft only|Remove one: Confusion, Fear, Silence, or Blind, in that priority.|Immediate.|
|Awakening Potion|Craft only|Remove one: Stun, Freeze, or Sleep, in that priority.|Immediate.|
|Purifying Potion|Craft only|Remove up to 2 removable negative effects.|Immediate.|
|Greater Purifying Potion|Endgame craft only|Remove all removable negative effects; gain +20% Global Status Resistance.|2 own actions.|
|Strength Potion|Craft only|+20% Physical Attack.|3 own actions.|
|Focus Potion|Craft only|Focus: +20% Magic Power; +15 Accuracy.|3 own actions.|
|Iron Skin Potion|Craft only|+25% Defense.|3 own actions.|
|Warding Potion|Craft only|+25% Magical Defense.|3 own actions.|
|Swiftness Potion|Craft only|Haste: +25% Speed.|3 own actions.|
|Precision Potion|Craft only|+20 Accuracy; +10% Critical Chance.|3 own actions.|
|Evasion Potion|Craft only|Evasion Up: +18% Evasion.|3 own actions.|
|Critical Potion|Craft only|+20% Critical Chance.|3 own actions.|
|Berserker Potion|Craft only|Berserk: +35% Physical Attack; -15% Defense.|3 own actions.|
|Concentration Potion|Craft only|Focus: +25% Magic Power; +20 Accuracy; +20% Global Status Resistance.|3 own actions.|
|Each elemental Resistance Potion|Craft only|+40% matching element Resistance; Darkness/Holy use +45%.|4 own actions.|
|Elemental Ward Potion|Craft only|Elemental Ward: +35% Resistance to the first elemental type received.|4 own actions.|
|Each elemental Oil|Craft only|Direct weapon hits use the Oil element and gain +15% listed setup/status chance.|3 Player own actions.|
|Smoke Bomb|Market utility|75% escape chance from a normal encounter.|Immediate; no boss escape.|
|Recall Potion|Market utility|Return to Town from a safe non-combat location.|Out of combat only.|
|Treasure Sense Potion|Craft only|+25% Gold Find; +15% Item Find.|5 victorious encounters.|
|Invisibility Potion|Craft only|Skip one non-boss encounter selection.|Consumed when skipping.|
|Lucky Potion|Craft only|+10 percentage points to rare supplemental material-roll chance; does not affect guaranteed drops or Equipment caps.|5 victorious encounters.|
|Phoenix Potion|Mythic craft|When HP would reach 0: remain at 1 HP and restore 35% Max HP.|One automatic safeguard per Potion.|
|Last Stand Potion|Mythic craft|Barrier 35% Max HP; Fortify +25%.|3 own actions.|
|Vampiric Potion|Mythic craft|+15% Lifesteal from direct damage.|3 own actions.|
|Experience Potion|Mythic craft|+50% enemy XP.|Next 10 victories.|
|Gold Potion|Mythic craft|+50% enemy Gold.|Next 10 victories.|

## Early countermeasure availability

The main story order makes basic status answers available before or no later than the first reliable enemy that uses that status.

|First pressure|First meaningful source|Counter available before / at source|Counter recipe|
|---|---|---|---|
|Bleeding|Snow Wolf; Goblin Dagger|Before Mountain Foothills via Forest Entrance|Bandage: 1 Beast Claw + 1 Forest Herb.|
|Burn|Ash Lizard|Before Ashen Border via Desert + Mountain routes|Burn Salve: 1 Cactus Sap + 1 Ice Moss + 1 Empty Bottle.|
|Blind|Ice Bat; Vulture|Before Mountain Foothills via Forest/Desert routes|Mind Tonic: 1 Mana Mushroom + 1 Cactus Sap + 1 Empty Bottle.|
|Freeze|Ice Bat|At Mountain Foothills from its normal guaranteed materials|Awakening: 1 Ice Moss + 1 Mana Mushroom + 1 Empty Bottle.|
|Fear / Curse|Bone Hound / Shade|At Gloomwood from Forest/Desert materials|Mind Tonic for Fear; later Purifying for multi-cleanse.|
|Poison|Sand Scorpion|Before it through Forest/Desert materials|Antidote: 1 Forest Herb + 1 Cactus Sap + 1 Empty Bottle.|
|Rooted / Slow|Moss Spider / later enemies|Before Tier 3 through Sunlit Road materials|Purifying: 1 Holy Crystal + 1 Cactus Sap + 1 Empty Bottle.|
|Stun|Temple Squire|At Sunlit Road; its action-denial answer is already craftable from Mountain materials|Awakening recipe above.|

<a id="craft-input-source-matrix"></a>
## Craft-input source matrix

Every crafting input has at least one direct Monster Loot source. Entries listed as supplemental are extra independent rolls; all ordinary materials in an Enemy Codex `Guaranteed materials` cell are 100% drops.

|Craft input|Earliest availability|Direct monster source(s)|Primary uses|
|---|---|---|---|
|Forest Herb|Forest Entrance|Forest Rat; Wild Boar; Sun Acolyte; Goblin Scout; Thorn Beast; Treant|Small Health; Health; basic medicines|
|Mana Mushroom|Gloomwood|Shade; Goblin Shaman; Light Sprite; Fungus; Night Hag; Goblin Mage; Forest Witch|Small Mana; Mind Tonic; Focus|
|Redcap|Overgrown Trail|Fungus; Forest Witch|Health; Greater Health; Rejuvenation|
|Spider Silk|Overgrown Trail|Shadow Spider; Moss Spider; Thorn Matriarch; Webmother Nyss; Frost Spider; Icefang Matriarch|Evasion; Invisibility; oils|
|Beast Claw|Forest Entrance|Wild Boar; Barkhide Boar; Snow Wolf; Whitefang Alpha; Ash Lizard; Ember Hound; additional sources in Enemy Codex|Bandage; Strength; Critical|
|Cactus Sap|Desert Border|Desert Rat; Sand Wolf; Bandit Alchemist|Antidote; Burn Salve; Health|
|Venom Sac|Scorching Dunes|Sand Scorpion; Shadow Spider; Bogshade Huntress; Moss Spider; Webmother Nyss; Plague Mummy; Frost Spider|advanced Antidote; Poison recipes|
|Harpy Feather|Goblin Forest|Sunwing Hawk; Goblin Archer; Vulture; Glasswing Vulture; Harpy; Radiant Hawk; Bandit Archer; Dawn Seraph; Stormclaw Harpy; Wyvern; Dragon Archer|Swiftness; Precision; Gale Oil|
|Desert Spirit Dust|Ancient Ruins|Sand Wraith|Greater Purifying; Mind recipes|
|Air Crystal|Scorching Dunes|Dustrunner Scarab; Vulture; Glasswing Vulture; Harpy; Dune Captain Kharif; Desert Shaman; Avalanche Elemental; Ruin Guardian|Air Resistance; Gale Oil|
|Ice Moss|Mountain Foothills|Snow Wolf; Ice Bat; Whitefang Alpha; Ice Elemental; Frost Wyrm|Awakening; Water Resistance|
|Frost Crystal|Mountain Foothills|Ice Bat; Frost Spider; Frost Mage; Ice Elemental; Icebound Scribe; Icefang Matriarch; Frost Wyrm; Stormclaw Harpy; Avalanche Elemental; Frost Titan|Greater Mana; Frost Oil|
|Cursed Twig|Gloomwood|Shade; Bone Hound; Lantern Shade; Ash Cultist; Fungus; Grave Wraith; Plague Mummy; Forest Witch; Mummy|Darkness / endgame mind recipes|
|Ancient Coin|Sanctum Halls|Stone Guardian; Inquisitor; Veiled Inquisitor Sorn; Mummy; Ashen Mummy Scribe; Tomb Guardian|Precision; Critical; Treasure Sense|
|Holy Crystal|Sunlit Road|Sun Acolyte; Temple Squire; Sunwing Hawk; Radiant Hawk; Light Sprite; Sacred Treant; additional sources in Enemy Codex|Purifying; Holy Resistance|
|Iron Scrap|Forest Entrance|Forest Rat; Barkhide Boar; Goblin Scout; Goblin Dagger; Goblin Archer; Goblin Bomber|Blacksmith +0→+2|
|Iron Ore|Desert Border|Sand Beetle; Dustrunner Scarab; Temple Squire; Goblin Shaman; Totem-Bound Goblin; Boneknife Skulk; additional sources in Enemy Codex|Blacksmith +1→+2|
|Crystal Shard|Mountain Pass|Echo Stalker; Thorn Beast; Crystal Beetle; Mine Wraith; Quartzback Golem; Gravebound Knight Arct; Stone Guardian; Treant; Void Golem; Goblin King; Ruin Guardian|Blacksmith +2→+3|
|Magic Crystal|Goblin Forest|Goblin Shaman; Totem-Bound Goblin; Blighted Blossom; Bandit Alchemist; Sun Priest; Goblin Mage; additional sources in Enemy Codex|Blacksmith +2→+3; Mana recipes|
|Obsidian Fragment|Ember Fields|Lava Slime; Magma Beetle; Magmaheart Slime; Molten Golem; Forged Flame Sentinel; Inferno Lord; Dragon Knight; Obsidian Guardian; Dragon Knight Captain|Blacksmith +3→+4|
|Molten Core|Lava Fissures|Flame Elemental; Cinder Witch; Fire Drake; Embermaw Lizard; Molten Golem; Ember Wyrm; Forged Flame Sentinel; Inferno Lord|Blacksmith +3→+4|
|Obsidian Core|Obsidian Citadel|Obsidian Guardian; Obsidian Warden Korr|Blacksmith +4→+5; Last Stand|
|Enchantment Dust|Unique Bounties Tier 1|Contract / quest reward; see Enemy Codex|Enchanter Common→Uncommon|
|Enchantment Fragment|Unique Bounties Tier 2|Contract / quest reward; see Enemy Codex|Enchanter Uncommon→Rare|
|Enchantment Crystal|Unique Bounties Tier 3|Contract / quest reward; see Enemy Codex|Enchanter Rare→Epic; rerolls|
|Dragon Rune|Dragon Valley|Shadow Lord; Oracle; Dragon Servant; Dragon Whelp; Redscale Whelp; Dragon Archer; Dragon Knight; Dragon Priest; Dragon Warlock; Dragon Knight Captain; Ancient Dragon|Legendary/Mythic enchanting|
|Ancient Dragon Scale|Ancient Nest|Ancient Dragon|late upgrades; Full recovery|
|Ancient Dragon Fang|Ancient Nest|Obsidian Warden Korr; Ancient Dragon|late upgrades; Mythic|
|Mythic Ember|Ancient Nest|Ancient Dragon|Mythic enchanting/potions|
|Beetle Shell|Desert Border|Sand Beetle|defense utility|
|Scorpion Tail|Scorching Dunes|Sand Scorpion|advanced antidote|
|Stone Core|Mountain Pass|Rock Crawler; Sacred Treant; Thorn Matriarch; Stone Golem; Quartzback Golem; Treant; Hollowroot Treant; Tomb Guardian; Warden; Avalanche Elemental; Peak Guardian|Iron Skin; Earth Resistance|
|Dark Crystal|Mountain Pass|Lantern Shade; Echo Stalker; Dark Wolf; Bogshade Huntress; Mine Wraith; Cinder Witch; additional sources in Enemy Codex|Concentration; Shadow Oil|
|Ember Core|Ashen Border|Ash Lizard; Ember Hound; Ashfang Hound; Lava Slime; Ash Cultist; Magmaheart Slime; Flame Elemental; Fire Drake; Ember Wyrm|Berserker; Fire utility|
|Mountain Beast Claw|Frozen Peak|Mountain Beast|Berserker|
|Shadow Scale|Void Rift|Shadow Drake|Darkness Resistance; Shadow Oil|
|Dragon Claw|Dragon Valley|Dragon Whelp; Redscale Whelp; Wyvern|dragon recipes|
|Dragon Bone|Dragon Cave|Bonewing Remnant; Bone Dragon|dragon recipes|
|Bomb Powder|Goblin Forest|Goblin Bomber; Bandit Alchemist|Smoke Bomb; Fire Oil|
|Tattered Cloth|Bandit Camp|Bandit Scout|Smoke Bomb; Bandage alternatives|
|Sun Charm|Temple Gardens|Desert Shaman; Peak Guardian; Ruin Guardian|Lucky; Holy Resistance|
|Fire Essence|Ember Fields|Lava Slime; Flame Elemental; Fire Drake|Fire Resistance; Fire Oil|
|Dragon Relic|Obsidian Citadel|Dragon Priest; Dragon Knight Captain|Greater Purifying; Full recovery|
|Empty Bottle|Goblin Forest|Goblin Scout (20% supplemental); Bandit Scout (25% supplemental); Dragon Servant (20% supplemental)|Potion container|
|Empty Oil Flask|Goblin Forest|Goblin Bomber (50% supplemental); Bandit Alchemist (40% supplemental); Cinder Witch (35% supplemental)|Oil container|

`Redcap Mushroom` is a display alias for `Redcap`, not a second inventory item.

## Canonical recipes

|Output|Exact recipe|Unlock|
|---|---|---|
|Small Health Potion|1 Forest Herb + 1 Empty Bottle|Start.|
|Small Mana Potion|1 Mana Mushroom + 1 Empty Bottle|Start.|
|Health Potion|2 Forest Herb + 1 Redcap + 1 Empty Bottle|World Tier 3.|
|Mana Potion|1 Mana Mushroom + 1 Magic Crystal + 1 Empty Bottle|World Tier 2.|
|Greater Health Potion|2 Redcap + 1 Cactus Sap + 1 Empty Bottle|World Tier 4.|
|Greater Mana Potion|2 Magic Crystal + 1 Frost Crystal + 1 Empty Bottle|World Tier 4.|
|Rejuvenation Potion|1 Health Potion + 1 Mana Potion + 1 Redcap|World Tier 3.|
|Greater Rejuvenation Potion|1 Greater Health Potion + 1 Greater Mana Potion + 1 Ancient Dragon Scale|Complete `S-DRAGON-04`.|
|Antidote|1 Forest Herb + 1 Cactus Sap + 1 Empty Bottle|After Desert Border.|
|Bandage|1 Beast Claw + 1 Forest Herb|Start.|
|Burn Salve|1 Cactus Sap + 1 Ice Moss + 1 Empty Bottle|After Mountain Foothills.|
|Mind Tonic|1 Mana Mushroom + 1 Cactus Sap + 1 Empty Bottle|After Desert Border.|
|Awakening Potion|1 Ice Moss + 1 Mana Mushroom + 1 Empty Bottle|After Mountain Foothills.|
|Purifying Potion|1 Holy Crystal + 1 Cactus Sap + 1 Empty Bottle|After Sunlit Road.|
|Greater Purifying Potion|1 Holy Crystal + 1 Desert Spirit Dust + 1 Dragon Relic + 1 Empty Bottle|Dragon content.|
|Strength Potion|1 Beast Claw + 1 Forest Herb + 1 Empty Bottle|Start.|
|Focus Potion|1 Mana Mushroom + 1 Magic Crystal + 1 Empty Bottle|World Tier 2.|
|Iron Skin Potion|1 Stone Core + 1 Iron Ore + 1 Empty Bottle|World Tier 2.|
|Warding Potion|1 Magic Crystal + 1 Holy Crystal + 1 Empty Bottle|World Tier 2.|
|Swiftness Potion|1 Harpy Feather + 1 Air Crystal + 1 Empty Bottle|World Tier 2.|
|Precision Potion|1 Harpy Feather + 1 Ancient Coin + 1 Empty Bottle|World Tier 3.|
|Evasion Potion|1 Spider Silk + 1 Harpy Feather + 1 Empty Bottle|World Tier 3.|
|Critical Potion|1 Beast Claw + 1 Ancient Coin + 1 Empty Bottle|World Tier 3.|
|Berserker Potion|1 Mountain Beast Claw + 1 Ember Core + 1 Empty Bottle|World Tier 5.|
|Concentration Potion|1 Dark Crystal + 1 Frost Crystal + 1 Empty Bottle|World Tier 4.|
|Fire / Water / Earth / Air Resistance Potion|Matching element material + matching support material + 1 Empty Bottle|World Tier 3.|
|Darkness / Holy Resistance Potion|Dark Crystal or Holy Crystal + Shadow Scale or Sun Charm + 1 Empty Bottle|Dragon content.|
|Elemental Ward Potion|Fire Essence + Frost Crystal + Stone Core + Air Crystal + Shadow Scale + Holy Crystal + Empty Bottle|Dragon content.|
|Each elemental Oil|Matching element material + listed supporting material + Empty Oil Flask|World Tier 3 or later.|
|Smoke Bomb|1 Bomb Powder + 1 Tattered Cloth|World Tier 2.|
|Treasure Sense Potion|1 Ancient Coin + 1 Mana Mushroom + 1 Empty Bottle|World Tier 3.|
|Invisibility Potion|1 Spider Silk + 1 Shadow Scale + 1 Empty Bottle|Dragon content.|
|Lucky Potion|1 Ancient Coin + 1 Sun Charm + 1 Empty Bottle|World Tier 3.|
|Full Health Potion|2 Greater Health Potion + 1 Ancient Dragon Scale + 1 Dragon Relic + 1 Empty Bottle|Complete `S-DRAGON-04`.|
|Full Mana Potion|2 Greater Mana Potion + 1 Ancient Dragon Scale + 1 Dragon Relic + 1 Empty Bottle|Complete `S-DRAGON-04`.|
|Phoenix Potion|1 Full Health Potion + 1 Mythic Ember + 1 Holy Crystal + 1 Empty Bottle|Complete `S-DRAGON-04`.|
|Last Stand Potion|1 Full Health Potion + 1 Obsidian Core + 1 Ancient Dragon Fang + 1 Empty Bottle|Complete `S-DRAGON-04`.|
|Vampiric Potion|1 Greater Rejuvenation Potion + 1 Shadow Scale + 1 Ancient Dragon Fang + 1 Empty Bottle|Complete `S-DRAGON-04`.|
|Experience Potion|1 Greater Rejuvenation Potion + 1 Mythic Ember + 1 Ancient Coin + 1 Empty Bottle|Complete `S-DRAGON-04`.|
|Gold Potion|1 Greater Rejuvenation Potion + 1 Mythic Ember + 1 Sun Charm + 1 Empty Bottle|Complete `S-DRAGON-04`.|

## Coverage reconciliation

Every canonical status above has at least one Player Skill, Enemy Skill, Trait/Grade Effect, Potion, or Passive source. The detailed source mapping is held in the appropriate gameplay documents: Player sources in [Player skills](04_Player_and_Skills.md), Enemy sources in [Enemy AI patterns](13_Enemy_AI_Patterns.md), and Equipment sources in [Equipment](05_Equipment_and_Drop_Pools.md).

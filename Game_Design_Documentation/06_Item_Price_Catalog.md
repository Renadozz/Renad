# Item Price Catalog

## Linked documents

[Equipment](05_Equipment_and_Drop_Pools.md) · [Economy and Alchemy](07_Economy_Market_and_Alchemy.md) · [Town](09_Town_Quests_and_Contracts.md) · [Enemy Codex](12_Enemy_Codex.md)

## Pricing rules

|Rule|Implementation|
|---|---|
|Standard sell value|`Floor(Buy Price × 0.25)` when a Market buy price exists.|
|Drop-only material|This catalog assigns a reference value and a sell value of 25% of that reference value.|
|Equipment sell value|`Floor(Equipment Base Value × 0.25)`.|
|Quest Items|Never sellable, discardable, upgradeable, salvageable, or disenchantable.|
|Legendary/Mythic equipment|No buy price is provided because it is player-created; sale value is 25% of its derived base value if selling is permitted.|
|Crafting decision|Market sale, Blacksmith salvage, and Enchanter disenchanting are mutually exclusive item-destruction choices.|



> **Value interpretation override:** `Reference Value` is used for sell calculations, reward balancing, and recipe economic comparisons. It is **not** a Market purchase offer unless the item is explicitly listed in the Market stock rule. The only completed Potions with normal Market stock are Small Health Potion and Small Mana Potion.

## Materials, ingredients, and crafting utilities

|Item|Category|Availability / note|Reference Value|Sell Value|
|---|---|---|---|---|
|Forest Herb|Ingredient|Monster/Quest farmed; no normal Market sale.|12 Gold|3 Gold|
|Mana Mushroom|Ingredient|Monster/Quest farmed; no normal Market sale.|18 Gold|4 Gold|
|Redcap|Ingredient|Monster/Quest farmed; no normal Market sale.|25 Gold|6 Gold|
|Redcap Mushroom|Ingredient|Monster/Quest farmed; no normal Market sale.|25 Gold|6 Gold|
|Spider Silk|Ingredient|Monster/Quest farmed; no normal Market sale.|30 Gold|7 Gold|
|Beast Claw|Ingredient|Monster/Quest farmed; no normal Market sale.|35 Gold|8 Gold|
|Cactus Sap|Ingredient|Monster/Quest farmed; no normal Market sale.|30 Gold|7 Gold|
|Venom Sac|Ingredient|Monster/Quest farmed; no normal Market sale.|65 Gold|16 Gold|
|Harpy Feather|Ingredient|Monster/Quest farmed; no normal Market sale.|45 Gold|11 Gold|
|Desert Spirit Dust|Ingredient|Monster/Quest farmed; no normal Market sale.|55 Gold|13 Gold|
|Air Crystal|Ingredient|Monster/Quest farmed; no normal Market sale.|70 Gold|17 Gold|
|Ice Moss|Ingredient|Monster/Quest farmed; no normal Market sale.|60 Gold|15 Gold|
|Frost Crystal|Ingredient|Monster/Quest farmed; no normal Market sale.|80 Gold|20 Gold|
|Cursed Twig|Ingredient|Monster/Quest farmed; no normal Market sale.|85 Gold|21 Gold|
|Ancient Coin|Ingredient|Monster/Quest farmed; no normal Market sale.|120 Gold|30 Gold|
|Holy Crystal|Ingredient|Monster/Quest farmed; no normal Market sale.|150 Gold|37 Gold|
|Iron Scrap|Smithing Material|Farm-first; Market emergency stock is 3 per restock at 60 Gold.|60 Gold|15 Gold|
|Iron Ore|Smithing Material|Monster/Quest farmed; no normal Market sale.|50 Gold|12 Gold|
|Crystal Shard|Smithing Material|Monster/Quest farmed; no normal Market sale.|85 Gold|21 Gold|
|Magic Crystal|Smithing Material|Monster/Quest farmed; no normal Market sale.|180 Gold|45 Gold|
|Obsidian Fragment|Smithing Material|Monster/Quest farmed; no normal Market sale.|220 Gold|55 Gold|
|Molten Core|Smithing Material|Monster/Quest farmed; no normal Market sale.|400 Gold|100 Gold|
|Obsidian Core|Smithing Material|Monster/Quest farmed; no normal Market sale.|800 Gold|200 Gold|
|Enchantment Dust|Enchantment Material|Monster/Quest farmed; no normal Market sale.|100 Gold|25 Gold|
|Enchantment Fragment|Enchantment Material|Monster/Quest farmed; no normal Market sale.|300 Gold|75 Gold|
|Enchantment Crystal|Enchantment Material|Monster/Quest farmed; no normal Market sale.|700 Gold|175 Gold|
|Dragon Rune|Enchantment Material|Monster/Quest farmed; no normal Market sale.|700 Gold|175 Gold|
|Ancient Dragon Scale|Boss Material|Monster/Quest farmed; no normal Market sale.|1500 Gold|375 Gold|
|Ancient Dragon Fang|Boss Material|Monster/Quest farmed; no normal Market sale.|2000 Gold|500 Gold|
|Mythic Ember|Boss Material|Monster/Quest farmed; no normal Market sale.|3000 Gold|750 Gold|
|Beetle Shell|Ingredient|Monster/Quest farmed; no normal Market sale.|25 Gold|6 Gold|
|Scorpion Tail|Ingredient|Monster/Quest farmed; no normal Market sale.|45 Gold|11 Gold|
|Stone Core|Ingredient|Monster/Quest farmed; no normal Market sale.|100 Gold|25 Gold|
|Dark Crystal|Ingredient|Monster/Quest farmed; no normal Market sale.|150 Gold|37 Gold|
|Ember Core|Ingredient|Monster/Quest farmed; no normal Market sale.|120 Gold|30 Gold|
|Mountain Beast Claw|Ingredient|Monster/Quest farmed; no normal Market sale.|140 Gold|35 Gold|
|Shadow Scale|Ingredient|Monster/Quest farmed; no normal Market sale.|180 Gold|45 Gold|
|Dragon Claw|Ingredient|Monster/Quest farmed; no normal Market sale.|220 Gold|55 Gold|
|Dragon Bone|Ingredient|Monster/Quest farmed; no normal Market sale.|260 Gold|65 Gold|
|Bomb Powder|Ingredient|Monster/Quest farmed; no normal Market sale.|70 Gold|17 Gold|
|Tattered Cloth|Ingredient|Monster/Quest farmed; no normal Market sale.|20 Gold|5 Gold|
|Sun Charm|Ingredient|Monster/Quest farmed; no normal Market sale.|160 Gold|40 Gold|
|Fire Essence|Ingredient|Monster/Quest farmed; no normal Market sale.|130 Gold|32 Gold|
|Dragon Relic|Ingredient|Monster/Quest farmed; no normal Market sale.|350 Gold|87 Gold|
|Empty Bottle|Crafting Utility|Monster loot source; Market convenience container unlimited.|5 Gold|1 Gold|
|Empty Oil Flask|Crafting Utility|Monster loot source; Market convenience container unlimited.|8 Gold|2 Gold|

## Consumables, potions, oils, and utilities

|Item|Category|Effect / availability|Reference Value|Sell Value|
|---|---|---|---|---|
|Small Health Potion|Consumable|Market or craft; restore 45 HP.|35 Gold|8 Gold|
|Health Potion|Consumable|Restore 120 HP; craft only (reference value, not Market stock).|140 Gold|35 Gold|
|Greater Health Potion|Consumable|Restore 300 HP; craft only (reference value, not Market stock).|420 Gold|105 Gold|
|Full Health Potion|Unique Consumable|Restore all missing HP and remove Burn; Endgame craft only (reference value, not Market stock).|1,400 Gold|350 Gold|
|Small Mana Potion|Consumable|Market or craft; restore 18 MP.|40 Gold|10 Gold|
|Mana Potion|Consumable|Restore 55 MP; craft only (reference value, not Market stock).|160 Gold|40 Gold|
|Greater Mana Potion|Consumable|Restore 140 MP; craft only (reference value, not Market stock).|480 Gold|120 Gold|
|Full Mana Potion|Unique Consumable|Restore all missing MP and remove Silence; Endgame craft only (reference value, not Market stock).|1,400 Gold|350 Gold|
|Rejuvenation Potion|Consumable|Restore 90 HP and 45 MP; craft only (reference value, not Market stock).|330 Gold|82 Gold|
|Greater Rejuvenation Potion|Endgame Consumable|Restore 260 HP and 130 MP; craft only (reference value, not Market stock).|1,050 Gold|262 Gold|
|Antidote|Consumable|Remove Poison; craft only (reference value, not Market stock).|40 Gold|10 Gold|
|Bandage|Consumable|Remove Bleeding; craft only (reference value, not Market stock).|35 Gold|8 Gold|
|Burn Salve|Consumable|Remove Burn; +10% Fire Resistance for 2 own actions; craft only (reference value, not Market stock).|70 Gold|17 Gold|
|Mind Tonic|Consumable|Remove Confusion, Fear, Silence, or Blind by priority; craft only (reference value, not Market stock).|95 Gold|23 Gold|
|Awakening Potion|Consumable|Remove Stun, Freeze, or Sleep by priority; craft only (reference value, not Market stock).|150 Gold|37 Gold|
|Purifying Potion|Consumable|Remove up to 2 removable negative effects; craft only (reference value, not Market stock).|250 Gold|62 Gold|
|Greater Purifying Potion|Endgame Consumable|Remove all removable negative effects; +20% Status Resistance for 2 actions; craft only (reference value, not Market stock).|850 Gold|212 Gold|
|Strength Potion|Buff Consumable|Temporary Physical Attack bonus; craft only (reference value, not Market stock).|85 Gold|21 Gold|
|Focus Potion|Buff Consumable|Temporary Magic Power/Accuracy bonus; craft only (reference value, not Market stock).|120 Gold|30 Gold|
|Iron Skin Potion|Buff Consumable|Temporary Defense bonus; craft only (reference value, not Market stock).|130 Gold|32 Gold|
|Warding Potion|Buff Consumable|Temporary Magical Defense bonus; craft only (reference value, not Market stock).|180 Gold|45 Gold|
|Swiftness Potion|Buff Consumable|Temporary Speed bonus; craft only (reference value, not Market stock).|170 Gold|42 Gold|
|Precision Potion|Buff Consumable|Temporary Accuracy bonus; craft only (reference value, not Market stock).|120 Gold|30 Gold|
|Evasion Potion|Buff Consumable|Temporary Evasion bonus; craft only (reference value, not Market stock).|125 Gold|31 Gold|
|Critical Potion|Buff Consumable|Temporary Critical Chance bonus; craft only (reference value, not Market stock).|150 Gold|37 Gold|
|Berserker Potion|Endgame Buff Consumable|Temporary Berserk; craft only (reference value, not Market stock).|450 Gold|112 Gold|
|Concentration Potion|Endgame Buff Consumable|Temporary Focus/Status resistance; craft only (reference value, not Market stock).|420 Gold|105 Gold|
|Fire Resistance Potion|Elemental Consumable|Temporary Fire Resistance; craft only (reference value, not Market stock).|180 Gold|45 Gold|
|Water Resistance Potion|Elemental Consumable|Temporary Water Resistance; craft only (reference value, not Market stock).|180 Gold|45 Gold|
|Earth Resistance Potion|Elemental Consumable|Temporary Earth Resistance; craft only (reference value, not Market stock).|180 Gold|45 Gold|
|Air Resistance Potion|Elemental Consumable|Temporary Air Resistance; craft only (reference value, not Market stock).|180 Gold|45 Gold|
|Darkness Resistance Potion|Endgame Consumable|Temporary Darkness Resistance; craft only (reference value, not Market stock).|300 Gold|75 Gold|
|Holy Resistance Potion|Endgame Consumable|Temporary Holy Resistance; craft only (reference value, not Market stock).|300 Gold|75 Gold|
|Elemental Ward Potion|Endgame Consumable|Temporary Elemental Ward; craft only (reference value, not Market stock).|600 Gold|150 Gold|
|Fire Oil|Weapon Oil|Temporary Fire coating; craft only (reference value, not Market stock).|160 Gold|40 Gold|
|Frost Oil|Weapon Oil|Temporary Water coating; craft only (reference value, not Market stock).|160 Gold|40 Gold|
|Earth Oil|Weapon Oil|Temporary Earth coating; craft only (reference value, not Market stock).|160 Gold|40 Gold|
|Gale Oil|Weapon Oil|Temporary Air coating; craft only (reference value, not Market stock).|160 Gold|40 Gold|
|Shadow Oil|Weapon Oil|Temporary Darkness coating; craft only (reference value, not Market stock).|280 Gold|70 Gold|
|Holy Oil|Weapon Oil|Temporary Holy coating; craft only (reference value, not Market stock).|280 Gold|70 Gold|
|Smoke Bomb|Battle Utility|Market utility; 75% escape from normal encounters only.|80 Gold|20 Gold|
|Recall Potion|Travel Utility|Market utility; return to Town outside combat only.|150 Gold|37 Gold|
|Treasure Sense Potion|Special Consumable|Temporary Gold/Item Find; craft only (reference value, not Market stock).|220 Gold|55 Gold|
|Invisibility Potion|Endgame Consumable|Encounter avoidance; craft only (reference value, not Market stock).|400 Gold|100 Gold|
|Lucky Potion|Special Consumable|Temporary reward modifier; craft only (reference value, not Market stock).|260 Gold|65 Gold|
|Phoenix Potion|Unique Consumable|At lethal damage: stay at 1 HP then restore 35% Max HP; Mythic craft only (reference value, not Market stock).|1000 Gold|250 Gold|
|Last Stand Potion|Unique Consumable|Barrier 35% Max HP + Fortify 25% for 3 actions; Mythic craft only (reference value, not Market stock).|850 Gold|212 Gold|
|Vampiric Potion|Unique Consumable|Gain 15% Lifesteal for 3 actions; Mythic craft only (reference value, not Market stock).|650 Gold|162 Gold|
|Experience Potion|Unique Consumable|Gain 50% XP for next 10 victories; Mythic craft only (reference value, not Market stock).|700 Gold|175 Gold|
|Gold Potion|Unique Consumable|Gain 50% Gold for next 10 victories; Mythic craft only (reference value, not Market stock).|700 Gold|175 Gold|

## Named equipment

The values below duplicate the equipment catalog for economic lookup.

|Item|Slot|Initial Grade|Base Value|Sell Value|Source|
|---|---|---|---|---|---|
|Rootwood Sword|Weapon|Common|500 Gold|125 Gold|Earth Tier 1 Normal Pool; Earth Tier 1 Elite Pool|
|Barkhide Vest|Armor|Common|420 Gold|105 Gold|Earth Tier 1 Normal Pool; Earth Tier 1 Elite Pool|
|Boulder Hammer of the Trail|Weapon|Uncommon|1150 Gold|287 Gold|Earth Tier 2 Normal Pool; Earth Tier 2 Elite Pool|
|Mossweave Armor of the Trail|Armor|Uncommon|980 Gold|245 Gold|Earth Tier 2 Normal Pool; Earth Tier 2 Elite Pool|
|Grove Staff of Resolve|Weapon|Rare|3200 Gold|800 Gold|Earth Tier 3 Normal Pool; Earth Tier 3 Elite Pool|
|Groveguard Plate of Resolve|Armor|Rare|2350 Gold|587 Gold|Earth Tier 3 Normal Pool; Earth Tier 3 Elite Pool|
|Thornshield of the Deep|Weapon|Epic|5900 Gold|1475 Gold|Earth Tier 4 Normal Pool; Earth Tier 4 Elite Pool|
|Druidic Robe of the Deep|Armor|Epic|5400 Gold|1350 Gold|Earth Tier 4 Normal Pool; Earth Tier 4 Elite Pool|
|Thornshield of the Sigil|Weapon|Epic|9300 Gold|2325 Gold|Earth Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Groveguard Plate of the Sigil|Armor|Epic|8600 Gold|2150 Gold|Earth Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Dune Saber|Weapon|Common|500 Gold|125 Gold|Air Tier 1 Normal Pool; Air Tier 1 Elite Pool|
|Sandstalker Leather|Armor|Common|420 Gold|105 Gold|Air Tier 1 Normal Pool; Air Tier 1 Elite Pool|
|Glasswing Bow of the Trail|Weapon|Uncommon|1350 Gold|337 Gold|Air Tier 2 Normal Pool; Air Tier 2 Elite Pool|
|Caravan Guardmail of the Trail|Armor|Uncommon|980 Gold|245 Gold|Air Tier 2 Normal Pool; Air Tier 2 Elite Pool|
|Windstep Dagger of Resolve|Weapon|Rare|2700 Gold|675 Gold|Air Tier 3 Normal Pool; Air Tier 3 Elite Pool|
|Dunewarden Plate of Resolve|Armor|Rare|2350 Gold|587 Gold|Air Tier 3 Normal Pool; Air Tier 3 Elite Pool|
|Zephyr Staff of the Deep|Weapon|Epic|7300 Gold|1825 Gold|Air Tier 4 Normal Pool; Air Tier 4 Elite Pool|
|Whispering Robe of the Deep|Armor|Epic|5400 Gold|1350 Gold|Air Tier 4 Normal Pool; Air Tier 4 Elite Pool|
|Windstep Dagger of the Sigil|Weapon|Epic|9800 Gold|2450 Gold|Air Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Dunewarden Plate of the Sigil|Armor|Epic|8600 Gold|2150 Gold|Air Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Icefang Dagger|Weapon|Common|500 Gold|125 Gold|Water Tier 1 Normal Pool; Water Tier 1 Elite Pool|
|Climber Coat|Armor|Common|420 Gold|105 Gold|Water Tier 1 Normal Pool; Water Tier 1 Elite Pool|
|Frostbound Staff of the Trail|Weapon|Uncommon|1350 Gold|337 Gold|Water Tier 2 Normal Pool; Water Tier 2 Elite Pool|
|Crystalweave Armor of the Trail|Armor|Uncommon|980 Gold|245 Gold|Water Tier 2 Normal Pool; Water Tier 2 Elite Pool|
|Climber Axe of Resolve|Weapon|Rare|2700 Gold|675 Gold|Water Tier 3 Normal Pool; Water Tier 3 Elite Pool|
|Peakbreaker Plate of Resolve|Armor|Rare|2350 Gold|587 Gold|Water Tier 3 Normal Pool; Water Tier 3 Elite Pool|
|Glacier Shield of the Deep|Weapon|Epic|5900 Gold|1475 Gold|Water Tier 4 Normal Pool; Water Tier 4 Elite Pool|
|Rime Robe of the Deep|Armor|Epic|5400 Gold|1350 Gold|Water Tier 4 Normal Pool; Water Tier 4 Elite Pool|
|Glacier Shield of the Sigil|Weapon|Epic|9300 Gold|2325 Gold|Water Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Peakbreaker Plate of the Sigil|Armor|Epic|8600 Gold|2150 Gold|Water Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Ashen Axe|Weapon|Common|500 Gold|125 Gold|Fire Tier 1 Normal Pool; Fire Tier 1 Elite Pool|
|Ashveil Leather|Armor|Common|420 Gold|105 Gold|Fire Tier 1 Normal Pool; Fire Tier 1 Elite Pool|
|Cinder Hammer of the Trail|Weapon|Uncommon|1150 Gold|287 Gold|Fire Tier 2 Normal Pool; Fire Tier 2 Elite Pool|
|Emberguard Mail of the Trail|Armor|Uncommon|980 Gold|245 Gold|Fire Tier 2 Normal Pool; Fire Tier 2 Elite Pool|
|Flamebrand Great Sword of Resolve|Weapon|Rare|3200 Gold|800 Gold|Fire Tier 3 Normal Pool; Fire Tier 3 Elite Pool|
|Forgeplate of Resolve|Armor|Rare|2350 Gold|587 Gold|Fire Tier 3 Normal Pool; Fire Tier 3 Elite Pool|
|Ember Staff of the Deep|Weapon|Epic|7300 Gold|1825 Gold|Fire Tier 4 Normal Pool; Fire Tier 4 Elite Pool|
|Cinder Robe of the Deep|Armor|Epic|5400 Gold|1350 Gold|Fire Tier 4 Normal Pool; Fire Tier 4 Elite Pool|
|Flamebrand Great Sword of the Sigil|Weapon|Epic|11550 Gold|2887 Gold|Fire Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Forgeplate of the Sigil|Armor|Epic|8600 Gold|2150 Gold|Fire Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Gloomblade Dagger|Weapon|Common|500 Gold|125 Gold|Darkness Tier 1 Normal Pool; Darkness Tier 1 Elite Pool|
|Shadeweave Leather|Armor|Common|420 Gold|105 Gold|Darkness Tier 1 Normal Pool; Darkness Tier 1 Elite Pool|
|Grave Staff of the Trail|Weapon|Uncommon|1350 Gold|337 Gold|Darkness Tier 2 Normal Pool; Darkness Tier 2 Elite Pool|
|Cryptguard Armor of the Trail|Armor|Uncommon|980 Gold|245 Gold|Darkness Tier 2 Normal Pool; Darkness Tier 2 Elite Pool|
|Dread Knight Sword of Resolve|Weapon|Rare|2700 Gold|675 Gold|Darkness Tier 3 Normal Pool; Darkness Tier 3 Elite Pool|
|Voidplate of Resolve|Armor|Rare|2350 Gold|587 Gold|Darkness Tier 3 Normal Pool; Darkness Tier 3 Elite Pool|
|Nightguard Shield of the Deep|Weapon|Epic|5900 Gold|1475 Gold|Darkness Tier 4 Normal Pool; Darkness Tier 4 Elite Pool|
|Mourning Robe of the Deep|Armor|Epic|5400 Gold|1350 Gold|Darkness Tier 4 Normal Pool; Darkness Tier 4 Elite Pool|
|Nightguard Shield of the Sigil|Weapon|Epic|9300 Gold|2325 Gold|Darkness Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Voidplate of the Sigil|Armor|Epic|8600 Gold|2150 Gold|Darkness Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Sunlit Sword|Weapon|Common|500 Gold|125 Gold|Holy Tier 1 Normal Pool; Holy Tier 1 Elite Pool|
|Procession Leather|Armor|Common|420 Gold|105 Gold|Holy Tier 1 Normal Pool; Holy Tier 1 Elite Pool|
|Radiant Staff of the Trail|Weapon|Uncommon|1350 Gold|337 Gold|Holy Tier 2 Normal Pool; Holy Tier 2 Elite Pool|
|Temple Plate of the Trail|Armor|Uncommon|980 Gold|245 Gold|Holy Tier 2 Normal Pool; Holy Tier 2 Elite Pool|
|Temple Hammer of Resolve|Weapon|Rare|2700 Gold|675 Gold|Holy Tier 3 Normal Pool; Holy Tier 3 Elite Pool|
|Basilica Bulwark of Resolve|Armor|Rare|2350 Gold|587 Gold|Holy Tier 3 Normal Pool; Holy Tier 3 Elite Pool|
|Aegis Shield of the Deep|Weapon|Epic|5900 Gold|1475 Gold|Holy Tier 4 Normal Pool; Holy Tier 4 Elite Pool|
|Dawn Robe of the Deep|Armor|Epic|5400 Gold|1350 Gold|Holy Tier 4 Normal Pool; Holy Tier 4 Elite Pool|
|Aegis Shield of the Sigil|Weapon|Epic|9300 Gold|2325 Gold|Holy Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Basilica Bulwark of the Sigil|Armor|Epic|8600 Gold|2150 Gold|Holy Tier 6 Elite Pool; Regional Boss Challenge Pool|
|Dragonscale Sword|Weapon|Rare|12500 Gold|3125 Gold|Dragon Tier 1 Normal Pool; Dragon Tier 1 Elite Pool|
|Dragonhide Leather|Armor|Rare|11000 Gold|2750 Gold|Dragon Tier 1 Normal Pool; Dragon Tier 1 Elite Pool|
|Wyrmwing Bow of the Cave|Weapon|Rare|19450 Gold|4862 Gold|Dragon Tier 2 Normal Pool; Dragon Tier 2 Elite Pool|
|Citadel Mail of the Cave|Armor|Rare|14500 Gold|3625 Gold|Dragon Tier 2 Normal Pool; Dragon Tier 2 Elite Pool|
|Citadel War Staff of the Citadel|Weapon|Epic|26550 Gold|6637 Gold|Dragon Tier 3 Normal Pool; Dragon Tier 3 Elite Pool|
|Ancient Scale Plate of the Citadel|Armor|Epic|20000 Gold|5000 Gold|Dragon Tier 3 Normal Pool; Dragon Tier 3 Elite Pool|
|Obsidian Aegis of the Nest|Weapon|Epic|29000 Gold|7250 Gold|Dragon Tier 4 Normal Pool; Dragon Tier 4 Elite Pool|
|Eclipse Robe of the Nest|Armor|Epic|27000 Gold|6750 Gold|Dragon Tier 4 Normal Pool; Dragon Tier 4 Elite Pool|
|Thornward Ring|Accessory|Rare|3500 Gold|875 Gold|Fixed story reward S-T3-01; never random drop|
|Dune Watcher's Charm|Accessory|Rare|3700 Gold|925 Gold|Fixed story reward S-T3-02; never random drop|
|Echo Miner Pendant|Accessory|Rare|5200 Gold|1300 Gold|Fixed story reward S-T4-03; never random drop|
|Forgehand Bracer|Accessory|Epic|7600 Gold|1900 Gold|Fixed story reward S-T4-04; never random drop|
|Mourning Veil|Armor|Epic|5400 Gold|1350 Gold|Fixed story reward S-T4-05; never random drop|
|Dawnkeeper Brooch|Accessory|Epic|8500 Gold|2125 Gold|Fixed story reward S-T4-06; never random drop|
|Dragonwatch Band|Accessory|Epic|18000 Gold|4500 Gold|Fixed story reward S-DRAGON-03; never random drop|

## Story, collection, and bounty inventory

All listed items have a fixed price state of **Not sellable**. They are still listed individually so the implementation can validate every item ID.

|Item|Category|Inventory rule|Sell price|
|---|---|---|---|
|Wayfinder Compass|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Surveyor Marker|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Caravan Ledger|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Frostbitten Locket|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Cinder Scout Report|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Lantern of Lost Names|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Dawn Processional Bell|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Earthen Totem Shard|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Singing Sand Vial|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Resonance Crystal|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Ember Collar|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Marsh Hunter's Token|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Sunroot Seed|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Thornheart Knot|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Stormbound Standard|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Miner's Drill Key|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Molten Pressure Valve|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Epitaph Seal|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Sanctum Cipher Plate|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Ancient Sap Vial|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Astral Lens|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Frozen Star Chart|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Forge Heart Key|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Void Compass|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Oath Feather [Story]|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Royal Clearing Key|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Guardian Oath Plate|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Shrine Prayer Cord|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Core Binding Chain|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Veilbreaker Sigil|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Dawn Trial Seal|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Earth Sigil|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Air Sigil|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Water Sigil|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Fire Sigil|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Darkness Sigil|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Holy Sigil|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Dominion Map|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Dragonwatch Signal Horn|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Ashen Draconic Tablet|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Citadel Gate Sigil|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Ancient Memory Scale|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Dragon King's Seal|Story Quest Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Trail Survey Tag|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Caravan Wheel Seal|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Climber Route Flag|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Evacuation Route Token|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Pilgrim Name Strip|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Procession Ribbon|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Goblin Patrol Token|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Singing Sand Packet|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Pass Supply Tag|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Heatproof Sample|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Marsh Trail Marker|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Sunroot Pollen|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Thorn Sap Sample|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Bandit Supply Seal|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Mine Claim Stamp|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Fissure Heat Sample|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Crypt Seal Fragment|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Sanctum Archive Seal|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Grove Memory Shard|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Observatory Gear Segment|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Ice Cave Survey Chip|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Forge Calibration Plate|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Rift Stabilizer Fragment|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Basilica Ward Fragment|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Peak Prayer Bead|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Dragonwatch Route Mark|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Cave Binding Fragment|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Citadel Armory Tag|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Nest Survey Fragment|Collection Contract Item|0 Backpack slots; Quest Item inventory|Not sellable|
|Barkhide Tusk|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Dustrunner Carapace|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Whitefang Pelt|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Ashfang Collar|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Lantern Wick|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Sunwing Feather|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Boneknife Insignia|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Glasswing Feather|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Echo Fragment|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Magmaheart Core|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Bogshade Token|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Blighted Petal|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Webmother Gland|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Captain's Badge|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Quartzback Core|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Embermaw Fang|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Gravebound Crest|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Veiled Seal|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Hollowroot Bark|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Scribe's Tablet|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Icefang Fang|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Sentinel Core|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Rift Echo Shard|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Oath Feather [Bounty]|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|King's Crown Shard|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Guardian Core Plate|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Stormclaw Plume|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Inferno Ember|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Dread Veil Fragment|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Oracle's Trial Seal|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Titan Glacier Heart|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Redscale Horn|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Bonewing Scale|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Warden Command Sigil|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|
|Ancient Dragon Memory Scale|Bounty / Boss Proof|0 Backpack slots; Quest Item inventory|Not sellable|

## Explicit exclusions

|Legacy name|Canonical state|
|---|---|
|Dragon King's Heart|Legacy-only, unobtainable, and **Not sellable**. It remains in the preserved source for history; the active Dragon King drops only the Seal.|
|Redcap Mushroom|Display alias for `Redcap`; both names must resolve to the same item ID and price.|
|Generic `Equipment`|Not an item ID. Resolve the named pool to one item from [05_Equipment_and_Drop_Pools.md](05_Equipment_and_Drop_Pools.md).|

This catalog covers every specifically named inventory item in the supplied documents plus the added active recipe materials and the complete new equipment catalog.


## Economy Balance 2.0 Override

### Sale-value anti-arbitrage rule

`Sell Value = Floor(original +0 Base Value × 0.25)`.

Blacksmith upgrades, Grade upgrades, Grade Effects, and Grade Passives **never increase the sell value**. This deliberately prevents a player from converting Gold and materials into a profit through repeated upgrading and resale. Equipment should be upgraded because it improves a build, not because it creates a sale loop.

### Market equipment: base loadouts

The Market sells the following low-cost, ungraded `+0` base equipment from the beginning. The tutorial grants one selected Training Weapon and one selected Training Armor for free so the Player cannot be locked out by early Gold.

|Item|Slot / requirement|+0 stats|Built-in identity|Buy|Sell|
|---|---|---|---|---:|---:|
|Training Sword|One-hand Sword|Physical Attack +18; Accuracy +2|Balanced melee.|100|25|
|Training Great Sword|Two-hand Great Sword|Physical Attack +28; Critical Chance +2%|High damage; Off Hand locked.|150|37|
|Training Axe|One-hand Axe|Physical Attack +21; Critical Chance +2%|Bleed-oriented melee.|110|27|
|Training Hammer|One-hand Hammer|Physical Attack +19; Defense +4|Control-oriented melee.|110|27|
|Training Dagger|One-hand Dagger|Physical Attack +16; Speed +2; Evasion +2%|Fast evasive melee.|95|23|
|Training Bow|Two-hand Bow|Physical Attack +24; Accuracy +6|Accurate ranged damage; Off Hand locked.|145|36|
|Apprentice Staff|Two-hand Staff|Magic Power +26; Max Mana +12|Required for Staff and Elemental Magic Skills.|150|37|
|Training Shield|One-hand Shield|Defense +16; Magical Defense +11|Enables Shield Skills.|115|28|
|Scout Leather|Light Armor|Defense +12; Evasion +4%; Speed +1|Evasion / speed build.|110|27|
|Guard Mail|Normal Armor|Defense +17; Magical Defense +12|Balanced build.|125|31|
|Recruit Plate|Heavy Armor|Defense +24; Magical Defense +14; Speed -1|Defense / Barrier build.|155|38|
|Apprentice Robe|Robe|Magic Power +12; Magical Defense +14; Max Mana +10|Magic / heal build.|130|32|

### Completed consumable purchase restriction

The only completed Potions the Market sells are `Small Health Potion` and `Small Mana Potion`. Every mid-tier, strong, resistance, buff, medicine, oil, and endgame Potion is **craft only** or a specified quest/chest/boss reward. Smoke Bomb and Recall Potion are non-Potion utilities and remain purchasable.

|Completed consumable|Market state|Reason|
|---|---|---|
|Small Health Potion / Small Mana Potion|Available unlimited|Emergency low-power recovery.|
|Health Potion / Mana Potion and all stronger recovery|Not sold; craft only|Keeps alchemy and monster ingredient farming relevant.|
|Antidote, Bandage, Burn Salve, Mind Tonic, Awakening, Purifying|Not sold; craft only|Status relief is part of preparation and farming.|
|Buff Potions, Resistance Potions, Oils|Not sold; craft only|Build preparation must use farmed inputs.|
|Full / Phoenix / Last Stand / Vampiric / Experience / Gold Potions|No normal sale|Boss, chest, quest, or event sources only.|

### Price relation check

|Check|Result|
|---|---|
|Starter gear vs starting Gold|A free tutorial selection prevents a blocked start; optional replacements are 95–155 Gold.|
|Tier 1 drop sale vs low Potion|A Tier 1 item sells for about 100–125 Gold, enough for several emergency Potions but not enough to bypass crafting.|
|Upgrade vs resale|The fixed original-base sale value means no Blacksmith or Enchanter resale profit exists.|
|Dragon gear vs Dragon income|Dragon equipment costs 12,500–30,500 Gold; Dragon normal enemies, quests, bounties, and saleable drops provide the matching endgame economy.|
|High-tier materials|Retain low sale-to-use value compared with upgrade impact; spending them on progression is normally more valuable than selling them.|


## Active price relation validation

|Relationship|Calculation|Result|
|---|---|---|
|Small Health Potion versus early Gold|35 Gold / 28 Gold per Tier 1 normal defeat|About 2 Tier 1 normal defeats per shop Potion; emergency recovery is useful but not freely spammed.|
|Small Mana Potion versus early Gold|40 Gold / 28 Gold per Tier 1 normal defeat|About 2 Tier 1 normal defeats per shop Potion.|
|Iron Scrap emergency purchase|3 × 60 Gold + 50 Gold for `+0 → +1`|230 Gold and a 3-unit restock cap make farming the normal route; the Market only prevents a hard block.|
|Starter weapon resale|100–155 Buy; 25–38 Sell|The 25% sell rule prevents buy/sell looping.|
|Tier 1 drop resale|Common Equipment normally sells for 105–125 Gold|Enough to fund a small number of emergency supplies, not enough to bypass crafting and upgrades.|
|Upgrade / Enchant resale|Sale stays `Floor(original +0 Base Value × 0.25)`|No Gold or material arbitrage; upgrades are build investments.|
|Epic-to-Mythic rerolls|Costs rise per individual item and never reset|Rerolling cannot be used to make sale value profit.|

All shop-facing prices are consistent with the 25% sale formula. Only Items with an explicit Market stock entry have a Buy price; all other reference values are for sell, reward, recipe, and balance calculations.

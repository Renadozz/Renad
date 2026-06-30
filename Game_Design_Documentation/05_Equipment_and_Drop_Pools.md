# Equipment Catalog and Monster Drop Pools

## Linked documents

[Player and skills](04_Player_and_Skills.md) · [Item price catalog](06_Item_Price_Catalog.md) · [Blacksmith and Enchanter](08_Blacksmith_and_Enchanter.md) · [Enemy codex](12_Enemy_Codex.md)

## Equipment-drop rules

|Rule|Canonical implementation|
|---|---|
|Normal enemies|Use their named `Normal Pool`; quality cap is Rare.|
|Elites, Story Uniques, Contract Uniques, regional bosses|Use their named `Elite Pool`; quality cap is Epic.|
|Legendary/Mythic|Never in a loot pool; created only through Enchanter grade upgrades.|
|One roll|A successful equipment roll awards exactly one listed item from the named pool.|
|Pool identity|An enemy's pool is recorded in [12_Enemy_Codex.md](12_Enemy_Codex.md); individual item membership is recorded below.|
|Quest gear|Fixed story rewards, never random drops.|
|Sale|Equipment sells for the displayed 25% value; salvaging/disenchanting remains an alternative.|

## Pool rules

|Pool ID|Used by|Grade cap|Equipment chance|Contents|
|---|---|---|---|---|
|Earth Tier 1 Normal Pool|Earth tier 1 normal enemies|Common–Uncommon|10% one-item roll|Items tagged `Earth Tier 1 Normal Pool` in the catalog.|
|Earth Tier 1 Elite Pool|Earth tier 1 Elite/Unique enemies|Uncommon–Rare|18% one-item roll|Normal-pool entries plus entries tagged `Earth Tier 1 Elite Pool`.|
|Earth Tier 2 Normal Pool|Earth tier 2 normal enemies|Uncommon–Rare|10% one-item roll|Items tagged `Earth Tier 2 Normal Pool` in the catalog.|
|Earth Tier 2 Elite Pool|Earth tier 2 Elite/Unique enemies|Rare|18% one-item roll|Normal-pool entries plus entries tagged `Earth Tier 2 Elite Pool`.|
|Earth Tier 3 Normal Pool|Earth tier 3 normal enemies|Rare|10% one-item roll|Items tagged `Earth Tier 3 Normal Pool` in the catalog.|
|Earth Tier 3 Elite Pool|Earth tier 3 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Earth Tier 3 Elite Pool`.|
|Earth Tier 4 Normal Pool|Earth tier 4 normal enemies|Rare–Epic|10% one-item roll|Items tagged `Earth Tier 4 Normal Pool` in the catalog.|
|Earth Tier 4 Elite Pool|Earth tier 4 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Earth Tier 4 Elite Pool`.|
|Earth Tier 6 Elite Pool|Earth boss/Challenge and elite content|Epic|25% one-item roll|Sigil equipment tagged `Earth Tier 6 Elite Pool`.|
|Air Tier 1 Normal Pool|Air tier 1 normal enemies|Common–Uncommon|10% one-item roll|Items tagged `Air Tier 1 Normal Pool` in the catalog.|
|Air Tier 1 Elite Pool|Air tier 1 Elite/Unique enemies|Uncommon–Rare|18% one-item roll|Normal-pool entries plus entries tagged `Air Tier 1 Elite Pool`.|
|Air Tier 2 Normal Pool|Air tier 2 normal enemies|Uncommon–Rare|10% one-item roll|Items tagged `Air Tier 2 Normal Pool` in the catalog.|
|Air Tier 2 Elite Pool|Air tier 2 Elite/Unique enemies|Rare|18% one-item roll|Normal-pool entries plus entries tagged `Air Tier 2 Elite Pool`.|
|Air Tier 3 Normal Pool|Air tier 3 normal enemies|Rare|10% one-item roll|Items tagged `Air Tier 3 Normal Pool` in the catalog.|
|Air Tier 3 Elite Pool|Air tier 3 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Air Tier 3 Elite Pool`.|
|Air Tier 4 Normal Pool|Air tier 4 normal enemies|Rare–Epic|10% one-item roll|Items tagged `Air Tier 4 Normal Pool` in the catalog.|
|Air Tier 4 Elite Pool|Air tier 4 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Air Tier 4 Elite Pool`.|
|Air Tier 6 Elite Pool|Air boss/Challenge and elite content|Epic|25% one-item roll|Sigil equipment tagged `Air Tier 6 Elite Pool`.|
|Water Tier 1 Normal Pool|Water tier 1 normal enemies|Common–Uncommon|10% one-item roll|Items tagged `Water Tier 1 Normal Pool` in the catalog.|
|Water Tier 1 Elite Pool|Water tier 1 Elite/Unique enemies|Uncommon–Rare|18% one-item roll|Normal-pool entries plus entries tagged `Water Tier 1 Elite Pool`.|
|Water Tier 2 Normal Pool|Water tier 2 normal enemies|Uncommon–Rare|10% one-item roll|Items tagged `Water Tier 2 Normal Pool` in the catalog.|
|Water Tier 2 Elite Pool|Water tier 2 Elite/Unique enemies|Rare|18% one-item roll|Normal-pool entries plus entries tagged `Water Tier 2 Elite Pool`.|
|Water Tier 3 Normal Pool|Water tier 3 normal enemies|Rare|10% one-item roll|Items tagged `Water Tier 3 Normal Pool` in the catalog.|
|Water Tier 3 Elite Pool|Water tier 3 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Water Tier 3 Elite Pool`.|
|Water Tier 4 Normal Pool|Water tier 4 normal enemies|Rare–Epic|10% one-item roll|Items tagged `Water Tier 4 Normal Pool` in the catalog.|
|Water Tier 4 Elite Pool|Water tier 4 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Water Tier 4 Elite Pool`.|
|Water Tier 6 Elite Pool|Water boss/Challenge and elite content|Epic|25% one-item roll|Sigil equipment tagged `Water Tier 6 Elite Pool`.|
|Fire Tier 1 Normal Pool|Fire tier 1 normal enemies|Common–Uncommon|10% one-item roll|Items tagged `Fire Tier 1 Normal Pool` in the catalog.|
|Fire Tier 1 Elite Pool|Fire tier 1 Elite/Unique enemies|Uncommon–Rare|18% one-item roll|Normal-pool entries plus entries tagged `Fire Tier 1 Elite Pool`.|
|Fire Tier 2 Normal Pool|Fire tier 2 normal enemies|Uncommon–Rare|10% one-item roll|Items tagged `Fire Tier 2 Normal Pool` in the catalog.|
|Fire Tier 2 Elite Pool|Fire tier 2 Elite/Unique enemies|Rare|18% one-item roll|Normal-pool entries plus entries tagged `Fire Tier 2 Elite Pool`.|
|Fire Tier 3 Normal Pool|Fire tier 3 normal enemies|Rare|10% one-item roll|Items tagged `Fire Tier 3 Normal Pool` in the catalog.|
|Fire Tier 3 Elite Pool|Fire tier 3 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Fire Tier 3 Elite Pool`.|
|Fire Tier 4 Normal Pool|Fire tier 4 normal enemies|Rare–Epic|10% one-item roll|Items tagged `Fire Tier 4 Normal Pool` in the catalog.|
|Fire Tier 4 Elite Pool|Fire tier 4 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Fire Tier 4 Elite Pool`.|
|Fire Tier 6 Elite Pool|Fire boss/Challenge and elite content|Epic|25% one-item roll|Sigil equipment tagged `Fire Tier 6 Elite Pool`.|
|Darkness Tier 1 Normal Pool|Darkness tier 1 normal enemies|Common–Uncommon|10% one-item roll|Items tagged `Darkness Tier 1 Normal Pool` in the catalog.|
|Darkness Tier 1 Elite Pool|Darkness tier 1 Elite/Unique enemies|Uncommon–Rare|18% one-item roll|Normal-pool entries plus entries tagged `Darkness Tier 1 Elite Pool`.|
|Darkness Tier 2 Normal Pool|Darkness tier 2 normal enemies|Uncommon–Rare|10% one-item roll|Items tagged `Darkness Tier 2 Normal Pool` in the catalog.|
|Darkness Tier 2 Elite Pool|Darkness tier 2 Elite/Unique enemies|Rare|18% one-item roll|Normal-pool entries plus entries tagged `Darkness Tier 2 Elite Pool`.|
|Darkness Tier 3 Normal Pool|Darkness tier 3 normal enemies|Rare|10% one-item roll|Items tagged `Darkness Tier 3 Normal Pool` in the catalog.|
|Darkness Tier 3 Elite Pool|Darkness tier 3 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Darkness Tier 3 Elite Pool`.|
|Darkness Tier 4 Normal Pool|Darkness tier 4 normal enemies|Rare–Epic|10% one-item roll|Items tagged `Darkness Tier 4 Normal Pool` in the catalog.|
|Darkness Tier 4 Elite Pool|Darkness tier 4 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Darkness Tier 4 Elite Pool`.|
|Darkness Tier 6 Elite Pool|Darkness boss/Challenge and elite content|Epic|25% one-item roll|Sigil equipment tagged `Darkness Tier 6 Elite Pool`.|
|Holy Tier 1 Normal Pool|Holy tier 1 normal enemies|Common–Uncommon|10% one-item roll|Items tagged `Holy Tier 1 Normal Pool` in the catalog.|
|Holy Tier 1 Elite Pool|Holy tier 1 Elite/Unique enemies|Uncommon–Rare|18% one-item roll|Normal-pool entries plus entries tagged `Holy Tier 1 Elite Pool`.|
|Holy Tier 2 Normal Pool|Holy tier 2 normal enemies|Uncommon–Rare|10% one-item roll|Items tagged `Holy Tier 2 Normal Pool` in the catalog.|
|Holy Tier 2 Elite Pool|Holy tier 2 Elite/Unique enemies|Rare|18% one-item roll|Normal-pool entries plus entries tagged `Holy Tier 2 Elite Pool`.|
|Holy Tier 3 Normal Pool|Holy tier 3 normal enemies|Rare|10% one-item roll|Items tagged `Holy Tier 3 Normal Pool` in the catalog.|
|Holy Tier 3 Elite Pool|Holy tier 3 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Holy Tier 3 Elite Pool`.|
|Holy Tier 4 Normal Pool|Holy tier 4 normal enemies|Rare–Epic|10% one-item roll|Items tagged `Holy Tier 4 Normal Pool` in the catalog.|
|Holy Tier 4 Elite Pool|Holy tier 4 Elite/Unique enemies|Rare–Epic|18% one-item roll|Normal-pool entries plus entries tagged `Holy Tier 4 Elite Pool`.|
|Holy Tier 6 Elite Pool|Holy boss/Challenge and elite content|Epic|25% one-item roll|Sigil equipment tagged `Holy Tier 6 Elite Pool`.|
|Dragon Tier 1 Normal Pool|Dragon region stage 1 normals|Rare|15% one-item roll|Dragon gear for stage 1.|
|Dragon Tier 1 Elite Pool|Dragon region stage 1 elites/uniques|Rare–Epic|22% one-item roll|Dragon gear for stage 1; may use Elite extension.|
|Dragon Tier 2 Normal Pool|Dragon region stage 2 normals|Rare|15% one-item roll|Dragon gear for stage 2.|
|Dragon Tier 2 Elite Pool|Dragon region stage 2 elites/uniques|Rare–Epic|22% one-item roll|Dragon gear for stage 2; may use Elite extension.|
|Dragon Tier 3 Normal Pool|Dragon region stage 3 normals|Rare–Epic|15% one-item roll|Dragon gear for stage 3.|
|Dragon Tier 3 Elite Pool|Dragon region stage 3 elites/uniques|Rare–Epic|22% one-item roll|Dragon gear for stage 3; may use Elite extension.|
|Dragon Tier 4 Normal Pool|Dragon region stage 4 normals|Rare–Epic|15% one-item roll|Dragon gear for stage 4.|
|Dragon Tier 4 Elite Pool|Dragon region stage 4 elites/uniques|Rare–Epic|22% one-item roll|Dragon gear for stage 4; may use Elite extension.|

## Weapon, armor, shield, and accessory catalog

Each entry is a real item that can appear in its stated loot pool or fixed reward. The `Base Value` is used for the market sale formula. All stats are original `+0` values.

|Item|Slot|Type|Hand|Initial Grade|Elements|Base stats|Built-in effect|Drop/reward source|Base Value|Sell Value|
|---|---|---|---|---|---|---|---|---|---|---|
|Rootwood Sword|Weapon|Sword|One-Hand|Common|Earth|Physical Attack +24; Defense +5|On direct Earth damage: +5% Rooted chance|Earth Tier 1 Normal Pool; Earth Tier 1 Elite Pool|500 Gold|125 Gold|
|Barkhide Vest|Armor|Light Armor|—|Common|Earth|Defense +14; Evasion +3%|Poison Resistance +8%|Earth Tier 1 Normal Pool; Earth Tier 1 Elite Pool|420 Gold|105 Gold|
|Boulder Hammer of the Trail|Weapon|Hammer|One-Hand|Uncommon|Earth|Physical Attack +46; Defense +11|+5% Stun chance|Earth Tier 2 Normal Pool; Earth Tier 2 Elite Pool|1150 Gold|287 Gold|
|Mossweave Armor of the Trail|Armor|Normal Armor|—|Uncommon|Earth|Defense +34; Magical Defense +23|Earth Resistance +8%|Earth Tier 2 Normal Pool; Earth Tier 2 Elite Pool|980 Gold|245 Gold|
|Grove Staff of Resolve|Weapon|Staff|Two-Hand|Rare|Earth|Magic Power +60; Earth Damage +5%|Earth spells gain +5% Barrier Strength|Earth Tier 3 Normal Pool; Earth Tier 3 Elite Pool|3200 Gold|800 Gold|
|Groveguard Plate of Resolve|Armor|Heavy Armor|—|Rare|Earth|Defense +65; Magical Defense +35|Rooted Resistance +10%|Earth Tier 3 Normal Pool; Earth Tier 3 Elite Pool|2350 Gold|587 Gold|
|Thornshield of the Deep|Weapon|Shield|One-Hand|Epic|Earth|Defense +95; Magical Defense +57|At battle start: Barrier 5% Max HP|Earth Tier 4 Normal Pool; Earth Tier 4 Elite Pool|5900 Gold|1475 Gold|
|Druidic Robe of the Deep|Armor|Robe|—|Epic|Earth|Magic Power +57; Magical Defense +86|Earth Resistance +10%|Earth Tier 4 Normal Pool; Earth Tier 4 Elite Pool|5400 Gold|1350 Gold|
|Thornshield of the Sigil|Weapon|Shield|One-Hand|Epic|Earth|Defense +120; Magical Defense +72|At battle start: Barrier 5% Max HP|Earth Tier 6 Elite Pool; Regional Boss Challenge Pool|9300 Gold|2325 Gold|
|Groveguard Plate of the Sigil|Armor|Heavy Armor|—|Epic|Earth|Defense +156; Magical Defense +84|Rooted Resistance +10%|Earth Tier 6 Elite Pool; Regional Boss Challenge Pool|8600 Gold|2150 Gold|
|Dune Saber|Weapon|Sword|One-Hand|Common|Air|Physical Attack +24; Accuracy +4%|Air damage +5%|Air Tier 1 Normal Pool; Air Tier 1 Elite Pool|500 Gold|125 Gold|
|Sandstalker Leather|Armor|Light Armor|—|Common|Air|Defense +14; Evasion +4%|Air Resistance +8%|Air Tier 1 Normal Pool; Air Tier 1 Elite Pool|420 Gold|105 Gold|
|Glasswing Bow of the Trail|Weapon|Bow|Two-Hand|Uncommon|Air|Physical Attack +42; Accuracy +6%|Basic Shots gain +5% Accuracy|Air Tier 2 Normal Pool; Air Tier 2 Elite Pool|1350 Gold|337 Gold|
|Caravan Guardmail of the Trail|Armor|Normal Armor|—|Uncommon|Air|Defense +34; Magical Defense +23|Blind Resistance +8%|Air Tier 2 Normal Pool; Air Tier 2 Elite Pool|980 Gold|245 Gold|
|Windstep Dagger of Resolve|Weapon|Dagger|One-Hand|Rare|Air|Physical Attack +45; Speed +10|Critical Chance +3%|Air Tier 3 Normal Pool; Air Tier 3 Elite Pool|2700 Gold|675 Gold|
|Dunewarden Plate of Resolve|Armor|Heavy Armor|—|Rare|Air|Defense +65; Magical Defense +35|Slow Resistance +10%|Air Tier 3 Normal Pool; Air Tier 3 Elite Pool|2350 Gold|587 Gold|
|Zephyr Staff of the Deep|Weapon|Staff|Two-Hand|Epic|Air|Magic Power +114; Air Damage +5%|Gale skills gain +5% Accuracy|Air Tier 4 Normal Pool; Air Tier 4 Elite Pool|7300 Gold|1825 Gold|
|Whispering Robe of the Deep|Armor|Robe|—|Epic|Air|Magic Power +57; Magical Defense +86|Air Resistance +10%|Air Tier 4 Normal Pool; Air Tier 4 Elite Pool|5400 Gold|1350 Gold|
|Windstep Dagger of the Sigil|Weapon|Dagger|One-Hand|Epic|Air|Physical Attack +108; Speed +24|Critical Chance +3%|Air Tier 6 Elite Pool; Regional Boss Challenge Pool|9800 Gold|2450 Gold|
|Dunewarden Plate of the Sigil|Armor|Heavy Armor|—|Epic|Air|Defense +156; Magical Defense +84|Slow Resistance +10%|Air Tier 6 Elite Pool; Regional Boss Challenge Pool|8600 Gold|2150 Gold|
|Icefang Dagger|Weapon|Dagger|One-Hand|Common|Water|Physical Attack +24; Critical Chance +3%|Water damage +5%|Water Tier 1 Normal Pool; Water Tier 1 Elite Pool|500 Gold|125 Gold|
|Climber Coat|Armor|Light Armor|—|Common|Water|Defense +14; Speed +5|Freeze Resistance +8%|Water Tier 1 Normal Pool; Water Tier 1 Elite Pool|420 Gold|105 Gold|
|Frostbound Staff of the Trail|Weapon|Staff|Two-Hand|Uncommon|Water|Magic Power +46; Water Damage +5%|Freeze chance +5% from Water magic|Water Tier 2 Normal Pool; Water Tier 2 Elite Pool|1350 Gold|337 Gold|
|Crystalweave Armor of the Trail|Armor|Normal Armor|—|Uncommon|Water|Defense +34; Magical Defense +27|Water Resistance +8%|Water Tier 2 Normal Pool; Water Tier 2 Elite Pool|980 Gold|245 Gold|
|Climber Axe of Resolve|Weapon|Axe|One-Hand|Rare|Water|Physical Attack +60; Defense +10|Crippled Resistance +8%|Water Tier 3 Normal Pool; Water Tier 3 Elite Pool|2700 Gold|675 Gold|
|Peakbreaker Plate of Resolve|Armor|Heavy Armor|—|Rare|Water|Defense +65; Magical Defense +40|Freeze Resistance +10%|Water Tier 3 Normal Pool; Water Tier 3 Elite Pool|2350 Gold|587 Gold|
|Glacier Shield of the Deep|Weapon|Shield|One-Hand|Epic|Water|Defense +95; Magical Defense +66|Water Resistance +10%|Water Tier 4 Normal Pool; Water Tier 4 Elite Pool|5900 Gold|1475 Gold|
|Rime Robe of the Deep|Armor|Robe|—|Epic|Water|Magic Power +57; Magical Defense +95|Water Resistance +10%|Water Tier 4 Normal Pool; Water Tier 4 Elite Pool|5400 Gold|1350 Gold|
|Glacier Shield of the Sigil|Weapon|Shield|One-Hand|Epic|Water|Defense +120; Magical Defense +84|Water Resistance +10%|Water Tier 6 Elite Pool; Regional Boss Challenge Pool|9300 Gold|2325 Gold|
|Peakbreaker Plate of the Sigil|Armor|Heavy Armor|—|Epic|Water|Defense +156; Magical Defense +96|Freeze Resistance +10%|Water Tier 6 Elite Pool; Regional Boss Challenge Pool|8600 Gold|2150 Gold|
|Ashen Axe|Weapon|Axe|One-Hand|Common|Fire|Physical Attack +29; Critical Chance +2%|Fire damage +5%|Fire Tier 1 Normal Pool; Fire Tier 1 Elite Pool|500 Gold|125 Gold|
|Ashveil Leather|Armor|Light Armor|—|Common|Fire|Defense +14; Evasion +3%|Fire Resistance +8%|Fire Tier 1 Normal Pool; Fire Tier 1 Elite Pool|420 Gold|105 Gold|
|Cinder Hammer of the Trail|Weapon|Hammer|One-Hand|Uncommon|Fire|Physical Attack +49; Defense +8|Burn Resistance +8%|Fire Tier 2 Normal Pool; Fire Tier 2 Elite Pool|1150 Gold|287 Gold|
|Emberguard Mail of the Trail|Armor|Normal Armor|—|Uncommon|Fire|Defense +38; Magical Defense +23|Fire Resistance +8%|Fire Tier 2 Normal Pool; Fire Tier 2 Elite Pool|980 Gold|245 Gold|
|Flamebrand Great Sword of Resolve|Weapon|Great Sword|Two-Hand|Rare|Fire|Physical Attack +80; Fire Damage +5%|Heavy Attack gains +5% Burn chance|Fire Tier 3 Normal Pool; Fire Tier 3 Elite Pool|3200 Gold|800 Gold|
|Forgeplate of Resolve|Armor|Heavy Armor|—|Rare|Fire|Defense +70; Magical Defense +35|Burn Resistance +10%|Fire Tier 3 Normal Pool; Fire Tier 3 Elite Pool|2350 Gold|587 Gold|
|Ember Staff of the Deep|Weapon|Staff|Two-Hand|Epic|Fire|Magic Power +124; Fire Damage +5%|Fire spells gain +5% Burn chance|Fire Tier 4 Normal Pool; Fire Tier 4 Elite Pool|7300 Gold|1825 Gold|
|Cinder Robe of the Deep|Armor|Robe|—|Epic|Fire|Magic Power +66; Magical Defense +86|Fire Resistance +10%|Fire Tier 4 Normal Pool; Fire Tier 4 Elite Pool|5400 Gold|1350 Gold|
|Flamebrand Great Sword of the Sigil|Weapon|Great Sword|Two-Hand|Epic|Fire|Physical Attack +192; Fire Damage +5%|Heavy Attack gains +5% Burn chance|Fire Tier 6 Elite Pool; Regional Boss Challenge Pool|11550 Gold|2887 Gold|
|Forgeplate of the Sigil|Armor|Heavy Armor|—|Epic|Fire|Defense +168; Magical Defense +84|Burn Resistance +10%|Fire Tier 6 Elite Pool; Regional Boss Challenge Pool|8600 Gold|2150 Gold|
|Gloomblade Dagger|Weapon|Dagger|One-Hand|Common|Darkness|Physical Attack +24; Evasion +3%|Darkness damage +5%|Darkness Tier 1 Normal Pool; Darkness Tier 1 Elite Pool|500 Gold|125 Gold|
|Shadeweave Leather|Armor|Light Armor|—|Common|Darkness|Defense +14; Evasion +4%|Darkness Resistance +8%|Darkness Tier 1 Normal Pool; Darkness Tier 1 Elite Pool|420 Gold|105 Gold|
|Grave Staff of the Trail|Weapon|Staff|Two-Hand|Uncommon|Darkness|Magic Power +49; Darkness Damage +5%|Curse chance +5% from Darkness magic|Darkness Tier 2 Normal Pool; Darkness Tier 2 Elite Pool|1350 Gold|337 Gold|
|Cryptguard Armor of the Trail|Armor|Normal Armor|—|Uncommon|Darkness|Defense +38; Magical Defense +27|Curse Resistance +8%|Darkness Tier 2 Normal Pool; Darkness Tier 2 Elite Pool|980 Gold|245 Gold|
|Dread Knight Sword of Resolve|Weapon|Sword|One-Hand|Rare|Darkness|Physical Attack +60; Defense +10|Fear Resistance +8%|Darkness Tier 3 Normal Pool; Darkness Tier 3 Elite Pool|2700 Gold|675 Gold|
|Voidplate of Resolve|Armor|Heavy Armor|—|Rare|Darkness|Defense +70; Magical Defense +40|Fear Resistance +10%|Darkness Tier 3 Normal Pool; Darkness Tier 3 Elite Pool|2350 Gold|587 Gold|
|Nightguard Shield of the Deep|Weapon|Shield|One-Hand|Epic|Darkness|Defense +95; Magical Defense +66|Darkness Resistance +10%|Darkness Tier 4 Normal Pool; Darkness Tier 4 Elite Pool|5900 Gold|1475 Gold|
|Mourning Robe of the Deep|Armor|Robe|—|Epic|Darkness|Magic Power +66; Magical Defense +95|Darkness Resistance +10%|Darkness Tier 4 Normal Pool; Darkness Tier 4 Elite Pool|5400 Gold|1350 Gold|
|Nightguard Shield of the Sigil|Weapon|Shield|One-Hand|Epic|Darkness|Defense +120; Magical Defense +84|Darkness Resistance +10%|Darkness Tier 6 Elite Pool; Regional Boss Challenge Pool|9300 Gold|2325 Gold|
|Voidplate of the Sigil|Armor|Heavy Armor|—|Epic|Darkness|Defense +168; Magical Defense +96|Fear Resistance +10%|Darkness Tier 6 Elite Pool; Regional Boss Challenge Pool|8600 Gold|2150 Gold|
|Sunlit Sword|Weapon|Sword|One-Hand|Common|Holy|Physical Attack +26; Accuracy +4%|Holy damage +5%|Holy Tier 1 Normal Pool; Holy Tier 1 Elite Pool|500 Gold|125 Gold|
|Procession Leather|Armor|Light Armor|—|Common|Holy|Defense +14; Speed +5|Holy Resistance +8%|Holy Tier 1 Normal Pool; Holy Tier 1 Elite Pool|420 Gold|105 Gold|
|Radiant Staff of the Trail|Weapon|Staff|Two-Hand|Uncommon|Holy|Magic Power +49; Holy Damage +5%|Heal restores +5% more|Holy Tier 2 Normal Pool; Holy Tier 2 Elite Pool|1350 Gold|337 Gold|
|Temple Plate of the Trail|Armor|Normal Armor|—|Uncommon|Holy|Defense +38; Magical Defense +27|Magic Vulnerability Resistance +8%|Holy Tier 2 Normal Pool; Holy Tier 2 Elite Pool|980 Gold|245 Gold|
|Temple Hammer of Resolve|Weapon|Hammer|One-Hand|Rare|Holy|Physical Attack +65; Defense +10|Stun Resistance +8%|Holy Tier 3 Normal Pool; Holy Tier 3 Elite Pool|2700 Gold|675 Gold|
|Basilica Bulwark of Resolve|Armor|Heavy Armor|—|Rare|Holy|Defense +70; Magical Defense +40|Holy Resistance +10%|Holy Tier 3 Normal Pool; Holy Tier 3 Elite Pool|2350 Gold|587 Gold|
|Aegis Shield of the Deep|Weapon|Shield|One-Hand|Epic|Holy|Defense +104; Magical Defense +76|Holy Resistance +10%|Holy Tier 4 Normal Pool; Holy Tier 4 Elite Pool|5900 Gold|1475 Gold|
|Dawn Robe of the Deep|Armor|Robe|—|Epic|Holy|Magic Power +66; Magical Defense +95|Healing Received +5%|Holy Tier 4 Normal Pool; Holy Tier 4 Elite Pool|5400 Gold|1350 Gold|
|Aegis Shield of the Sigil|Weapon|Shield|One-Hand|Epic|Holy|Defense +132; Magical Defense +96|Holy Resistance +10%|Holy Tier 6 Elite Pool; Regional Boss Challenge Pool|9300 Gold|2325 Gold|
|Basilica Bulwark of the Sigil|Armor|Heavy Armor|—|Epic|Holy|Defense +168; Magical Defense +96|Holy Resistance +10%|Holy Tier 6 Elite Pool; Regional Boss Challenge Pool|8600 Gold|2150 Gold|
|Dragonscale Sword|Weapon|Sword|One-Hand|Rare|Fire,Air,Darkness|Physical Attack +207; Fire Damage +8%|Dragon enemies take +5% damage from this weapon|Dragon Tier 1 Normal Pool; Dragon Tier 1 Elite Pool|12500 Gold|3125 Gold|
|Dragonhide Leather|Armor|Light Armor|—|Rare|Fire,Air,Darkness|Defense +115; Evasion +5%|Fire Resistance +12%|Dragon Tier 1 Normal Pool; Dragon Tier 1 Elite Pool|11000 Gold|2750 Gold|
|Wyrmwing Bow of the Cave|Weapon|Bow|Two-Hand|Rare|Fire,Air,Darkness|Physical Attack +247; Accuracy +7%|Air damage +8%|Dragon Tier 2 Normal Pool; Dragon Tier 2 Elite Pool|19450 Gold|4862 Gold|
|Citadel Mail of the Cave|Armor|Normal Armor|—|Rare|Fire,Air,Darkness|Defense +195; Magical Defense +143|Dragon Rune find +5%|Dragon Tier 2 Normal Pool; Dragon Tier 2 Elite Pool|14500 Gold|3625 Gold|
|Citadel War Staff of the Citadel|Weapon|Staff|Two-Hand|Epic|Fire,Air,Darkness|Magic Power +300; Darkness Damage +8%|Magic Penetration +5%|Dragon Tier 3 Normal Pool; Dragon Tier 3 Elite Pool|26550 Gold|6637 Gold|
|Ancient Scale Plate of the Citadel|Armor|Heavy Armor|—|Epic|Fire,Air,Darkness|Defense +300; Magical Defense +195|All Elemental Resistance +6%|Dragon Tier 3 Normal Pool; Dragon Tier 3 Elite Pool|20000 Gold|5000 Gold|
|Obsidian Aegis of the Nest|Weapon|Shield|One-Hand|Epic|Fire,Air,Darkness|Defense +320; Magical Defense +260|Fire and Darkness Resistance +8%|Dragon Tier 4 Normal Pool; Dragon Tier 4 Elite Pool|29000 Gold|7250 Gold|
|Eclipse Robe of the Nest|Armor|Robe|—|Epic|Fire,Air,Darkness|Magic Power +220; Magical Defense +300|Darkness Resistance +12%|Dragon Tier 4 Normal Pool; Dragon Tier 4 Elite Pool|27000 Gold|6750 Gold|
|Thornward Ring|Accessory|Ring|—|Rare|Earth|Earth Resistance +12%; Poison Resistance +12%|On first Poison resisted: gain 5% Barrier|Fixed story reward S-T3-01; never random drop|3500 Gold|875 Gold|
|Dune Watcher's Charm|Accessory|Charm|—|Rare|Air|Accuracy +8%; Air Resistance +12%|Blind Resistance +10%|Fixed story reward S-T3-02; never random drop|3700 Gold|925 Gold|
|Echo Miner Pendant|Accessory|Pendant|—|Rare|Water|Magical Defense +114; Freeze Resistance +15%|Gain +5% Water Resistance while below 50% HP|Fixed story reward S-T4-03; never random drop|5200 Gold|1300 Gold|
|Forgehand Bracer|Accessory|Bracer|—|Epic|Fire|Physical Attack +133; Fire Resistance +15%|Heavy Attack deals +5% Fire damage|Fixed story reward S-T4-04; never random drop|7600 Gold|1900 Gold|
|Mourning Veil|Armor|Robe|—|Epic|Darkness|Magic Power +142; Darkness Resistance +15%|Dark Bolt gains +5% Curse chance|Fixed story reward S-T4-05; never random drop|5400 Gold|1350 Gold|
|Dawnkeeper Brooch|Accessory|Brooch|—|Epic|Holy|Holy Resistance +15%; Healing Received +10%|Heal restores +5% more|Fixed story reward S-T4-06; never random drop|8500 Gold|2125 Gold|
|Dragonwatch Band|Accessory|Ring|—|Epic|Fire,Air,Darkness|Defense +150; Magical Defense +150|Dragon enemy damage received -5%|Fixed story reward S-DRAGON-03; never random drop|18000 Gold|4500 Gold|

## Grade and upgrade interaction

- `Grade` and `Upgrade Level` are independent.
- Weapons, Shields, Armor, and Helmets can be upgraded and graded when their item data supports it. Accessories never can.
- **Random grade traits** belong only to weapon types and shields, as defined in [08_Blacksmith_and_Enchanter.md](08_Blacksmith_and_Enchanter.md).
- Original numeric stats and built-in numeric effects scale from `+0`; rolled traits never scale.

## Added regional drop-pool content

The source loot tables named only broad categories such as `Common-Rare Equipment`. The catalog above turns those categories into explicit item pools while preserving the source grade caps. This makes every enemy's equipment result traceable and supports the exact reward resolution in [12_Enemy_Codex.md](12_Enemy_Codex.md).


## Equipment Balance 2.0 Override

The catalog above has been re-scaled so that a first dropped weapon is meaningful but late Dragon equipment has substantially higher Physical Attack, Magic Power, Defense, and Magical Defense. Flat values shown in the table are the **new canonical +0 values**. Existing elemental percentages and named built-in effects retain their identity; Grade Effects and Grade Passives below add the high-tier power growth.

### Item-stat bands

|Content source|Typical +0 one-hand offense|Typical +0 two-hand offense|Typical +0 armor Defense|Purpose|
|---|---:|---:|---:|---|
|Market starter|18–22|26–30|12–24|Lets every equipment path begin immediately.|
|Tier 1 Common|24–30|—|14–20|First upgrades from starter gear.|
|Tier 2 Uncommon|45–55|—|30–40|First specialization.|
|Tier 3 Rare|70–90|—|50–70|Established build gear.|
|Tier 4 Epic|105–140|—|80–110|Deep-area power spike.|
|Tier 6 Sigil Epic|150–200|—|110–145|Regional-boss build gear.|
|Dragon Tier 1–2|190–260|230–310|135–190|Endgame transition.|
|Dragon Tier 3–4|300–420|360–500|210–320|Final build base before upgrades/grades.|

### Grade Effects and Grade Passives

A built-in item effect in the catalog is separate from a Grade Effect. Grade Effects are gained through the Enchanter and remain on the item on later upgrades. **A Weapon or Shield created directly at Epic Grade immediately rolls exactly one random compatible Epic Trait from the Epic Trait pool. Armor created directly at Epic Grade immediately rolls exactly one compatible Epic Armor Grade Effect.** It does not wait for another Enchanter action. Legendary and Mythic items are player-created only, so their later Grade Effects and Grade Passives arrive through their successful grade upgrades.

|Equipment grade|Weapon / Shield added Grade Effects|Armor added Grade Effects|Permanent Grade Passives|
|---|---:|---:|---:|
|Common|0|0|0|
|Uncommon|0|0|0|
|Rare|0; retains built-in effect only|0; retains built-in effect only|0|
|Epic|+1 compatible Epic Grade Effect|+1 compatible Epic Armor Effect|0|
|Legendary|Keep Epic + add +1 compatible Legendary Grade Effect|Keep Epic + add +1 compatible Legendary Armor Effect|+1 compatible permanent Grade Passive|
|Mythic (one-hand / shield / armor)|Keep prior + add +1 compatible Mythic Grade Effect|Keep prior + add +1 compatible Mythic Armor Effect|+1 additional compatible permanent Grade Passive|
|Mythic two-hand weapon|Keep prior + add **2** compatible Mythic Grade Effects|—|Add **2** compatible Mythic Grade Passives at Mythic instead of 1|

A normal Mythic weapon or armor therefore has 3 Grade Effects and 2 Grade Passives in total. A Mythic two-hand weapon has 4 Grade Effects and 3 Grade Passives in total: Epic 1, Legendary 1, Mythic 2; Legendary 1, Mythic 2 passives.

### Armor Grade Effect pool

|Grade|Armor type|Effect|Exact result|
|---|---|---|---|
|Epic|Light Armor|Fleet Lining|After evading a Physical hit, gain Haste +15% Speed for 1 own action.|
|Epic|Normal Armor|Balanced Plates|At battle start, gain Fortify +12% Defense and Magical Defense for 2 own actions.|
|Epic|Heavy Armor|Aegis Rivets|At battle start, create Barrier equal to 8% Max HP.|
|Epic|Robe|Mana Weave|After a direct Magic hit, restore 4% Max Mana.|
|Epic|Any Armor|Elemental Stitching|After receiving elemental Damage, gain +12% resistance to that element for 2 own actions.|
|Legendary|Light Armor|Ghost Seam|After evading, gain Evasion Up +18% for 2 own actions.|
|Legendary|Normal Armor|Veteran Lining|When HP falls to 50% or lower, gain Regeneration 5% Max HP for 2 own actions; once per battle.|
|Legendary|Heavy Armor|Bulwark Frame|While Barrier is active, gain 10% Damage Reduction.|
|Legendary|Robe|Spellguard Thread|After casting Magic, gain Magic Ward +20% Magical Defense for 2 own actions.|
|Mythic|Light Armor|Windwoven Mantle|At battle start, gain Haste +20% and Evasion Up +15% for 2 own actions.|
|Mythic|Normal Armor|Unbroken Harness|The first time HP drops below 35%, create Barrier equal to 18% Max HP; once per battle.|
|Mythic|Heavy Armor|Citadel Shell|At battle start, create Barrier equal to 18% Max HP and gain Fortify +20% for 2 own actions.|
|Mythic|Robe|Astral Robe|Gain +10% Magic Penetration and restore 6% Max Mana after first direct Magic hit each battle.|

### Weapon Grade Passive pool

|Passive family|Compatible items|Legendary passive|Mythic passive|
|---|---|---|---|
|Martial power|Sword, Great Sword, Axe, Hammer|+8% Physical Attack|+15% Physical Attack and +5% Physical Penetration|
|Precision|Sword, Dagger, Bow|+8 Accuracy and +5% Critical Chance|+15 Accuracy and +12% Critical Chance|
|Assassin|Dagger, Bow|+10% Damage against targets with a negative Status|+20% Damage against targets with a negative Status|
|Arcane power|Staff|+10% Magic Power|+18% Magic Power and +5% Magic Penetration|
|Elemental mastery|Any elemental weapon|+10% matching Element Damage|+18% matching Element Damage and +10% matching Resistance|
|Guardian|Shield|+10% Barrier Strength and +8% Defense|+20% Barrier Strength, +12% Defense, and +10% Magical Defense|
|Two-hand momentum|Great Sword, Bow, Staff, two-hand Axe/Hammer|+12% Damage with this weapon type|At Mythic select two: +15% damage, +10% penetration, +12% critical chance, +12% Speed after a defeat|

### Accessory restriction

- There is exactly **one Accessory slot**.
- Accessories can be sold when they are not Quest Items, but cannot be Blacksmith-upgraded, Enchanter-graded, salvaged, or disenchanted.
- Accessories keep their fixed Rare/Epic story identity and can enable defensive, healing, damage, accuracy, or utility builds without consuming a weapon or armor slot.


## Build templates

|Build|Primary Equipment|Skill families|Stat priorities|Play pattern|
|---|---|---|---|---|
|Defense / Barrier|Sword + Shield or Shield-only; Heavy Armor; defensive Accessory|Shield; Heavy Armor; Earth; Holy|Defense; Magical Defense; Barrier Strength; Status Resistance|Absorb pressure, cleanse control, and win through sustained damage.|
|Two-hand damage|Great Sword or two-hand Axe/Hammer; Heavy or Normal Armor|General Melee; weapon skills; Fire/Earth|Physical Attack; Critical; Penetration; Armor Break|High burst; compensates for no Off Hand through powerful Mythic two-hand effects and passives.|
|Precision ranged|Bow; Light Armor; Accuracy Accessory|General Ranged; Bow; Air|Accuracy; Critical; Speed; Winded / Slow chance|Acts early in the gauge, marks targets, and uses control.|
|Evasion assassin|One or two Daggers; Light Armor; Evasion Accessory|Dagger; Light Armor; Darkness/Air|Speed; Evasion; Critical; Poison/Bleeding|Avoids Physical damage and exploits Status Hunter bonuses.|
|Elemental mage|Staff; Robe; elemental Accessory|Staff; chosen Elemental School|Magic Power; Element Damage; Mana; Magic Penetration|Uses setup effects and Area spells; prepares against Silence.|
|Heal / ward support|Staff; Robe or Normal Armor; Holy Accessory|Holy; Water; Robe; Staff|Healing Received; Max Mana; Magical Defense; Status Resistance|Sustain, cleanse, Barrier, and marked judgment.|
|Debuff controller|Staff or Bow; Robe/Light Armor|Darkness; Air; Bow/Staff|Accuracy; Speed; Status Chance; Mana|Applies marks, Fear, Silence, Blind, and priority control.|
|Buff tempo|Sword/Dagger/Bow; Light or Normal Armor|Air; Armor; General Melee/Ranged|Speed; Haste; Focus; Fortify|Maintains short timed buffs and converts extra actions into pressure.|

## Direct Epic generation and effect totals

|Item state|Weapon / Shield result|Armor result|Passive result|
|---|---|---|---|
|Drops as Epic|Roll **one random compatible Epic Trait** immediately. This is the same selection rule as Rare → Epic.|Roll one compatible Epic Armor Grade Effect immediately.|None.|
|Upgrades Rare → Epic|Roll one random compatible Epic Trait immediately.|Roll one compatible Epic Armor Grade Effect immediately.|None.|
|Upgrades Epic → Legendary|Keep Epic Trait/Effect; roll one compatible Legendary Trait/Effect.|Keep Epic Effect; roll one compatible Legendary Armor Effect.|Add one compatible permanent Grade Passive.|
|Upgrades Legendary → Mythic, one-hand / Shield / Armor|Keep prior; roll one Mythic Trait/Effect.|Keep prior; roll one Mythic Armor Effect.|Add one Mythic Grade Passive, for two total.|
|Upgrades Legendary → Mythic, two-hand Weapon|Keep prior; roll **two** compatible Mythic Traits.|Not applicable.|Add **two** Mythic Grade Passives, for three total.|

A Trait's family cannot duplicate another Trait family on the same Weapon. A reroll replaces all rolled Traits or all Grade Passives of that item while retaining its Grade and upgrade level; see [Blacksmith and Enchanter](08_Blacksmith_and_Enchanter.md#trait-and-grade-passive-rerolls).

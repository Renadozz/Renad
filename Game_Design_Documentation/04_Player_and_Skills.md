# Player, Skills, and Passive System

## Linked documents

[Combat formulas](02_Attributes_and_Combat.md) · [Status effects and consumables](03_Status_Effects_and_Consumables.md) · [Equipment](05_Equipment_and_Drop_Pools.md) · [Town and Quest progression](09_Town_Quests_and_Contracts.md)

## Canonical skill-point budget and choice pressure

The Player begins with **4 Skill Points**. One point is awarded at every even Level through Level 100 (50 points), the six Regional Sigil quests award 6 points, and `S-DRAGON-04` awards 1 point. A Level 100 completionist therefore owns **61 Skill Points**.

|Acquisition|Points|Running total at Level 100|
|---|---:|---:|
|Start|4|4|
|Even Levels 2–100|50|54|
|Six Regional Sigil quests|6|60|
|`S-DRAGON-04`|1|61|

The library contains far more than 61 points of valid purchases. The player cannot unlock every skill and passive on one character. A full respec may be offered by a future Training Hall, but a partial respec is not supported.

|Purchase type|Cost|
|---|---:|
|Tier I–II active skill|1 Skill Point|
|Tier III–IV active skill|2 Skill Points|
|Tier V active skill|3 Skill Points|
|Tier VI active skill|4 Skill Points|
|Standard passive|2 Skill Points|
|Advanced passive|3 Skill Points|

## Global and regional Tier unlock rules

|Tier|Weapon / armor / general family|Elemental school|
|---|---|---|
|I|Reach any World Tier 1 Area.|Reach that element's World Tier 1 Area.|
|II|Reach World Tier 2; branch prerequisite required.|Reach that element's World Tier 2 Area.|
|III|Reach World Tier 3; branch prerequisite required.|Reach that element's World Tier 3 Area.|
|IV|Reach World Tier 4; branch prerequisite required.|Reach that element's World Tier 4 Area.|
|V|Reach World Tier 5; branch prerequisite required.|Reach that element's World Tier 5 Area.|
|VI|Defeat the first regional boss; branch prerequisite required.|Defeat that element's Regional Boss.|

A branch prerequisite means that a Tier II Skill needs one learned Tier I Skill in its own family; Tier III needs two prior family Skills; Tier IV needs three; Tier V needs four; Tier VI needs five. A passive does not count as a branch prerequisite.

## Skill notation

`P130 Primary` means 130% of Current Physical Attack and the equipped weapon's Primary Element; it uses hit and critical rules. `M120 Fire` means 120% of Current Magic Power as Fire Magic Damage; it always hits and cannot Crit. Every listed status chance is checked after damage using Status Resistance. Exact equations are in [Combat formulas](02_Attributes_and_Combat.md).

# Complete Active and Passive Skill Library

## System Overview

The Player uses Active Skills and Passive Skills.

Active Skills are selected during the Player's Action.

The Player can use every learned and currently valid Active Skill in combat. There are no Active Skill Slots.

Passive Skills are permanently active while equipped in a Passive Slot. They do not require Mana,do not use Cooldowns,and do not consume an Action.

|System|Rule|
|---|---|
|Basic Attack|Always available. Does not cost Mana and does not require a learned Skill.|
|Active Skills|Every learned Active Skill is available in combat when its Equipment Requirement,Mana Cost,and Cooldown are valid.|
|Active Skill Slots|There are no Active Skill Slots.|
|Active Skill Menu|The combat interface groups learned Skills by Physical,Armor,Shield,Staff,and Elemental Magic categories.|
|Physical Skills|Use Mana and Cooldowns. They use Physical Hit Chance and can Crit.|
|Armor Skills|Use Mana and Cooldowns. They are Self-targeted support Skills.|
|Shield Skills|Use Mana and Cooldowns. They require a Shield and can be offensive or defensive.|
|Magic Skills|Use Mana and Cooldowns. Magic Damage always hits and cannot Crit.|
|Passive Skill Slots|The Player may equip up to 3 learned Passive Skills.|
|Mythic Weapon Passive Grants|A Mythic Weapon may grant up to 2 additional Weapon Passive Effects. They do not use Passive Skill Slots.|
|Maximum Active Passive Effects|The Player can have at most 5 passive effects active:3 equipped Passive Skills and up to 2 Mythic Weapon Passive Effects.|
|Skill Duration|Buffs,Debuffs,and Status Effects use the affected unit's own Actions.|
|Skill Cooldowns|Cooldowns decrease by 1 at the start of the skill owner's own Action.|
|Status Reapplication|Do not apply the same Status or Buff if it still has at least 1 Action remaining.|
|Maximum Enemies|Combat contains at most 3 living Enemies,including Summons.|

---

# Core Rules

## Active Skill Availability

|Rule|Implementation|
|---|---|
|All Learned Skills|Every learned and valid Active Skill can be selected during combat.|
|No Loadout Limit|The Player does not equip or remove Active Skills before combat.|
|Equipment Requirement|A Skill is hidden or disabled when its required Weapon,Shield,Armor,or Staff is not equipped.|
|Mana Requirement|A Skill is disabled when Current Mana is lower than its Mana Cost.|
|Cooldown Requirement|A Skill is disabled while its Current Cooldown is above 0.|
|Silence|Silence disables Magic and Staff Skills,but does not disable Physical,Armor,or Shield Skills.|
|Player Action|The Player selects one valid Active Skill,one Basic Attack,or an allowed Item Action during each Player Action.|
|Target Limit|Every Active Skill lists its maximum number of targets.|
|Area Skills|`All Enemies` always means up to 3 living Enemies. Each target resolves Damage,Status Chance,and Resistance separately.|

## Universal Mana Rule

Every Active Skill except Basic Attack uses Mana.

This includes Physical,Melee,Ranged,Armor,and Shield Skills.

|Skill Tier|Recommended Physical Mana Cost|Recommended Armor or Shield Mana Cost|Recommended Magic Mana Cost|
|---|---:|---:|---:|
|Tier I|3-5 Mana|4-6 Mana|7-10 Mana|
|Tier II|6-8 Mana|7-10 Mana|12-15 Mana|
|Tier III|10-12 Mana|11-14 Mana|18-22 Mana|

> Physical Skills cost less Mana than Magic Skills because Physical Skills can miss and must pass Defense.  
> Magic Skills cost more Mana because they always hit and often add elemental Damage,control,or support.

## Target Terms

|Target|Max Targets|Meaning|
|---|---:|---|
|Self|1|The Player.|
|Enemy|1|One selected living Enemy.|
|All Enemies|3|Every living Enemy in the encounter.|
|No Target|0|The Skill creates an effect without selecting another combatant.|

---

# Skill Points and Learning

## Skill Points

|Rule|Implementation|
|---|---|
|Starting Skill Points|Start with 4 Skill Points.|
|Level Reward|Gain 1 Skill Point at every even Player Level: Levels 2, 4, ..., 100.|
|Story Reward|Each of the six Regional Sigil quests grants 1 point; `S-DRAGON-04` grants 1 point.|
|Skill Cost|Tier I–II Active: 1; Tier III–IV Active: 2; Tier V Active: 3; Tier VI Active: 4; standard Passive: 2; advanced Passive: 3.|
|Skill Rank|Skills have one fixed Rank. There are no skill-level upgrades.|
|Learned Active Skill|A learned Active Skill is immediately available whenever valid.|
|Learned Passive Skill|A learned Passive Skill must be placed into one of the 3 Passive Skill Slots to become active.|
|Respec|A future Training Hall may allow a full Skill Point respec.|

## Active Skill Unlock Tiers

|Tier|Requirement|Typical Skill Role|
|---|---|---|
|Tier I|Reach the first Area for the related weapon/armor/element path.|Core damage; basic support; basic debuff.|
|Tier II|Reach the related Tier 2 Area and learn one Tier I Skill in that family.|Specialization and control.|
|Tier III|Reach the related Tier 3 Area and learn two earlier-family Skills.|Strong damage; area play; strong support.|
|Tier IV|Reach the related Tier 4 Area and learn three earlier-family Skills.|Deep build identity and counters.|
|Tier V|Reach the related Tier 5 Area and learn four earlier-family Skills.|High-impact sustain or burst.|
|Tier VI|Complete the related regional boss Quest; martial/armor Tier VI unlocks after the first Regional Sigil and each elemental Tier VI after that element's Boss.|Late-game capstone.|


## Equipment Requirements

|Skill Category|Required Equipment|
|---|---|
|General Melee Skills|Sword,Great Sword,Axe,Hammer,or Dagger in Main Hand.|
|General Ranged Skills|Bow in Main Hand.|
|Sword Skills|Sword in Main Hand.|
|Great Sword Skills|Great Sword in Main Hand.|
|Axe Skills|Axe in Main Hand.|
|Hammer Skills|Hammer in Main Hand.|
|Dagger Skills|Dagger in Main Hand.|
|Bow Skills|Bow in Main Hand.|
|Staff Skills|Staff in Main Hand.|
|Shield Skills|Shield equipped in Main Hand or Off Hand.|
|Light Armor Skills|Light Armor equipped.|
|Normal Armor Skills|Normal Armor equipped.|
|Heavy Armor Skills|Heavy Armor equipped.|
|Robe Skills|Robe equipped.|
|Elemental Magic Skills|Staff in Main Hand unless a future magical Weapon explicitly allows Magic Skills.|

---

# Basic Attacks

|Equipment|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|Melee Weapon|Basic Attack|Enemy|1|P100 Primary|0|0|Uses Physical Hit Chance and can Crit.|
|Bow|Basic Shot|Enemy|1|P100 Primary|0|0|Uses Physical Hit Chance and can Crit.|
|Staff|Arcane Tap|Enemy|1|M80 Primary|0|0|Always hits and cannot Crit.|
|Shield Only|Shield Bash|Enemy|1|P70 Primary|0|0|Uses Physical Hit Chance and can Crit.|

---

# Physical Damage Skill Trees

## General Melee Skills

General Melee Skills are available to Sword,Great Sword,Axe,Hammer,and Dagger users.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Quick Strike|Enemy|1|P80 Primary|3|0|Gain +15% Accuracy for this attack.|
|I|Heavy Attack|Enemy|1|P130 Primary|5|1|High single-target Damage.|
|I|Piercing Attack|Enemy|1|P105 Primary|5|1|Ignores 25% Defense.|
|II|Guard Break|Enemy|1|P95 Primary|7|2|65% chance to apply Armor Break for 2 Actions.|
|II|Charge|Enemy|1|P115 Primary|7|2|35% chance to apply Crippled for 2 Actions.|
|III|Relentless Assault|Enemy|1|P150 Primary|11|3|Can only be used if the target has Armor Break,Cracked,or Weakness.|

## General Ranged Skills

General Ranged Skills are available to Bow users.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Quick Shot|Enemy|1|P80 Primary|3|0|Gain +15% Accuracy for this attack.|
|I|Aimed Shot|Enemy|1|P110 Primary|5|1|Gain +30% Accuracy for this attack.|
|I|Piercing Shot|Enemy|1|P100 Primary|5|1|Ignores 25% Defense.|
|II|Suppressing Shot|Enemy|1|P85 Air|7|2|60% chance to apply Slow for 2 Actions.|
|II|Blind Shot|Enemy|1|P75 Air|7|2|65% chance to apply Blind for 2 Actions.|
|III|Rain of Arrows|All Enemies|3|P80 Primary|11|3|Each target resolves Hit Chance and Critical Hit separately.|

---

# Weapon-Specific Skills

## Sword Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Duelist Slash|Enemy|1|P105 Primary|4|1|Gain +10% Critical Chance for this attack.|
|II|Riposte Stance|Self|1|None|7|3|Gain Fortify with +20% Defense and Magical Defense for 2 Actions. If a Physical Attack misses you,gain Haste with +20% Speed for 1 Action.|
|III|Blade of Precision|Enemy|1|P125 Primary|10|2|Gain +25% Accuracy and +15% Critical Chance for this attack.|

## Great Sword Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Cleave|All Enemies|3|P85 Primary|5|2|Each target resolves Hit Chance and Critical Hit separately.|
|II|Executioner Strike|Enemy|1|P145 Primary|8|3|Deal 25% more final Damage when the target is at or below 35% HP.|
|III|Rending Arc|Enemy|1|P120 Primary|10|2|50% chance to apply Bleeding for 3 Actions.|

## Axe Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Wild Chop|Enemy|1|P120 Primary|4|1|Gain Berserk with +15% Physical Attack and -10% Defense for 2 Actions.|
|II|Blood Axe|Enemy|1|P100 Primary|7|2|55% chance to apply Bleeding for 3 Actions.|
|III|Sundering Chop|Enemy|1|P115 Primary|10|3|Ignores 20% Defense and has a 60% chance to apply Armor Break for 2 Actions.|

## Hammer Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Crushing Blow|Enemy|1|P115 Primary|4|1|35% chance to apply Cracked for 2 Actions.|
|II|Stun Slam|Enemy|1|P100 Primary|7|2|35% chance to apply Stun for 1 Action.|
|III|Earthshatter|All Enemies|3|P100 Earth|11|3|45% chance to apply Slow for 2 Actions to each hit target.|

## Dagger Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Backstab|Enemy|1|P110 Primary|4|1|Gain +25% Critical Chance for this attack.|
|II|Venom Cut|Enemy|1|P85 Primary|7|2|60% chance to apply Poison for 3 Actions.|
|III|Shadowstep|Self|1|None|10|3|Gain Evasion Up with +30% Evasion and Haste with +20% Speed for 2 Actions.|

## Bow Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Pinning Shot|Enemy|1|P85 Air|4|2|60% chance to apply Slow for 2 Actions.|
|II|Hunter's Mark|Enemy|1|None|7|2|Apply Shadow Mark for 2 Actions.|
|III|Windpiercer|Enemy|1|P125 Air|10|3|Ignores 30% Defense and gains +20% Accuracy for this attack.|

## Staff Skills

Staff Skills are non-elemental magical techniques. They require a Staff but do not belong to one Elemental Magic School.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Arcane Bolt|Enemy|1|M100 Neutral|6|0|Always hits and cannot Crit.|
|II|Mana Channel|Self|1|None|0|3|Restore 12% of Max Mana.|
|III|Arcane Ward|Self|1|None|10|3|Gain Magic Ward with +25% Magical Defense for 2 Actions.|

---

# Armor Skill Trees

Armor Skills require the listed Armor Type.

## Light Armor Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Evasive Roll|Self|1|None|4|3|Gain Evasion Up with +25% Evasion for 2 Actions.|
|II|Fleet Step|Self|1|None|7|3|Gain Haste with +25% Speed for 2 Actions.|
|III|Elusive Guard|Self|1|None|11|4|Gain Evasion Up with +35% Evasion and +15% Status Resistance for 2 Actions.|

## Normal Armor Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Combat Readiness|Self|1|None|4|3|Gain Fortify with +15% Defense and Magical Defense for 2 Actions.|
|II|Balanced Recovery|Self|1|None|7|3|Gain Regeneration that restores 5% Max HP at the end of your next 3 Actions.|
|III|Steady Advance|Self|1|None|11|4|Gain Fortify with +20% Defense and Magical Defense and Haste with +15% Speed for 2 Actions.|

## Heavy Armor Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Iron Wall|Self|1|None|5|3|Gain Fortify with +30% Defense and Magical Defense for 2 Actions.|
|II|Unstoppable|Self|1|None|8|4|Remove Slow,Crippled,and Rooted. Gain +25% Status Resistance for 2 Actions.|
|III|Bulwark|Self|1|None|12|4|Create a Barrier equal to 15% of Max HP for 2 Actions.|

## Robe Skills

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Mana Veil|Self|1|None|4|3|Gain Magic Ward with +25% Magical Defense for 2 Actions.|
|II|Meditation|Self|1|None|0|3|Restore 15% of Max Mana.|
|III|Elemental Cloak|Self|1|None|11|4|Gain Elemental Ward with +25% Resistance to the next Elemental Damage Type received for 2 Actions.|

---

# Shield Skill Tree

Shield Skills require a Shield in either Hand.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Shield Bash|Enemy|1|P90 Primary|4|1|25% chance to apply Stun for 1 Action.|
|I|Guard Stance|Self|1|None|4|3|Gain Fortify with +20% Defense and Magical Defense for 2 Actions.|
|II|Barrier Wall|Self|1|None|8|3|Create a Barrier equal to 15% of Max HP for 2 Actions.|
|II|Shield Charge|Enemy|1|P110 Primary|7|2|40% chance to apply Crippled for 2 Actions.|
|III|Aegis Pulse|Self|1|None|12|4|Create a Barrier equal to 20% of Max HP and gain Magic Ward with +20% Magical Defense for 2 Actions.|

---

# Elemental Magic Schools

## Magic School Access

|Magic School|Related Region|Tier I Area|Tier II Area|Tier III Area|Primary Role|Secondary Roles|
|---|---|---|---|---|---|---|
|Earth Magic|Earth Forest|Forest Entrance|Overgrown Trail|Deep Woods|Defense and Control|Damage,Barrier,Rooted,Cracked|
|Air Magic|Desert|Desert Border|Bandit Camp|Ancient Ruins|Speed and Evasion|Damage,Blind,Slow,Winded|
|Water Magic|Mountain|Mountain Foothills|Echo Mine|Ice Caves|Control and Sustain|Damage,Wet,Freeze,Regeneration|
|Fire Magic|Ember Wastes|Ashen Border|Lava Fissures|Magma Forge|Direct Damage|Burn,Scorched,Damage Buffs|
|Darkness Magic|Umbral Region|Gloomwood|Forgotten Crypt|Void Rift|Debuffs and Lifesteal|Damage,Curse,Fear,Silence|
|Holy Magic|Sanctum|Sunlit Road|Sanctum Halls|Dawn Basilica|Healing and Protection|Damage,Cleanse,Holy Mark,Magic Vulnerability|

> Every Elemental School contains Damage,Buff,and Debuff Skills.  
> The stated Primary Role determines the school's strongest and most frequent effects.

---

# Earth Magic

Earth Magic specializes in Defense,Barriers,and battlefield control.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Earth Bolt|Enemy|1|M100 Earth|7|0|Always hits and cannot Crit.|
|I|Stone Skin|Self|1|None|8|3|Gain Fortify with +25% Defense and Magical Defense for 2 Actions.|
|I|Root Snare|Enemy|1|None|8|3|65% chance to apply Rooted for 2 Actions.|
|II|Stone Spear|Enemy|1|M120 Earth|13|2|45% chance to apply Cracked for 2 Actions.|
|II|Earthen Barrier|Self|1|None|12|3|Create a Barrier equal to 15% of Max HP for 2 Actions.|
|II|Quicksand|Enemy|1|None|12|3|65% chance to apply Slow for 2 Actions.|
|III|Earthquake|All Enemies|3|M95 Earth|20|4|45% chance to apply Slow for 2 Actions to each target.|
|III|Fortress of Stone|Self|1|None|18|4|Gain Fortify with +35% Defense and Magical Defense and create a Barrier equal to 12% of Max HP for 2 Actions.|

---

# Air Magic

Air Magic specializes in Speed,Accuracy,Evasion,and disruptive control.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Gale Blast|Enemy|1|M100 Air|7|0|50% chance to apply Winded for 2 Actions.|
|I|Tailwind|Self|1|None|8|3|Gain Haste with +25% Speed for 2 Actions.|
|I|Dust Veil|Enemy|1|None|8|3|70% chance to apply Blind for 2 Actions.|
|II|Razor Wind|Enemy|1|M120 Air|13|2|Gain +15% Accuracy for this Spell.|
|II|Evasive Current|Self|1|None|12|3|Gain Evasion Up with +30% Evasion for 2 Actions.|
|II|Pressure Drop|Enemy|1|None|12|3|65% chance to apply Slow for 2 Actions.|
|III|Tempest|All Enemies|3|M95 Air|20|4|50% chance to apply Winded for 2 Actions to each target.|
|III|Storm Focus|Self|1|None|18|4|Gain Haste with +25% Speed and Focus with +20% Magic Power and Accuracy for 2 Actions.|

---

# Water Magic

Water Magic specializes in Freeze,Wet,Regeneration,and defensive sustain.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Frost Lance|Enemy|1|M105 Water|8|2|40% chance to apply Freeze for 1 Action.|
|I|Flowing Recovery|Self|1|None|8|3|Gain Regeneration that restores 6% Max HP at the end of your next 3 Actions.|
|I|Chilling Mist|Enemy|1|M75 Water|10|3|Apply Wet for 2 Actions and roll 55% chance to apply Slow for 2 Actions.|
|II|Ice Shard|Enemy|1|M125 Water|14|2|Deals 20% more final Damage when the target has Wet.|
|II|Tidal Barrier|Self|1|None|12|3|Create a Barrier equal to 12% of Max HP and gain +20% Water Resistance for 2 Actions.|
|II|Undertow|Enemy|1|None|12|3|Apply Wet for 2 Actions and roll 50% chance to apply Crippled for 2 Actions.|
|III|Glacial Wave|All Enemies|3|M90 Water|20|4|Apply Wet for 2 Actions to each target.|
|III|Frozen Prison|Enemy|1|M115 Water|18|4|Apply Wet for 2 Actions and roll 55% chance to apply Freeze for 1 Action.|

---

# Fire Magic

Fire Magic specializes in the highest direct Damage and Burn-based pressure.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Fire Bolt|Enemy|1|M110 Fire|8|0|45% chance to apply Burn for 3 Actions.|
|I|Flame Focus|Self|1|None|8|3|Gain Focus with +25% Magic Power and +20% Accuracy for 2 Actions.|
|I|Scorching Brand|Enemy|1|None|9|3|70% chance to apply Scorched for 2 Actions.|
|II|Flame Wave|All Enemies|3|M90 Fire|14|3|50% chance to apply Burn for 3 Actions to each target.|
|II|Ember Ward|Self|1|None|12|3|Gain +25% Fire Resistance and +15% Fire Damage for 2 Actions.|
|II|Cinder Weakness|Enemy|1|M85 Fire|13|2|60% chance to apply Weakness for 2 Actions.|
|III|Infernal Nova|All Enemies|3|M125 Fire|22|4|70% chance to apply Burn for 3 Actions to each target.|
|III|Combustion|Enemy|1|M145 Fire|20|4|Deals 25% more final Damage when the target has Burn or Scorched.|

---

# Darkness Magic

Darkness Magic specializes in Curse,Marks,Fear,Silence,and Lifesteal.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Dark Bolt|Enemy|1|M100 Darkness|7|0|45% chance to apply Curse for 3 Actions.|
|I|Shadow Veil|Self|1|None|8|3|Gain Evasion Up with +25% Evasion for 2 Actions.|
|I|Shadow Mark|Enemy|1|None|8|3|Apply Shadow Mark for 2 Actions.|
|II|Soul Rend|Enemy|1|M115 Darkness|14|2|50% chance to apply Magic Break for 2 Actions.|
|II|Life Drain|Enemy|1|M90 Darkness|12|2|Restore Health equal to 50% of Health Damage dealt after Barrier absorption.|
|II|Fear Hex|Enemy|1|None|12|3|60% chance to apply Fear for 1 Action.|
|III|Voidstorm|All Enemies|3|M105 Darkness|20|4|Apply Shadow Mark for 2 Actions to each target.|
|III|Silence Hex|Enemy|1|None|18|4|65% chance to apply Silence for 1 Action.|

---

# Holy Magic

Holy Magic specializes in Healing,Cleanse,Protection,and marked judgment.

|Tier|Skill|Target|Max Targets|Damage|Mana|Cooldown|Effect|
|---|---|---|---:|---:|---:|---:|---|
|I|Holy Bolt|Enemy|1|M100 Holy|7|0|35% chance to apply Holy Mark for 2 Actions.|
|I|Heal|Self|1|None|10|3|Restore 18% of Max HP.|
|I|Purifying Light|Self|1|None|8|3|Remove 1 negative Status Effect.|
|II|Judgment Beam|Enemy|1|M120 Holy|14|2|50% chance to apply Magic Vulnerability for 2 Actions.|
|II|Holy Ward|Self|1|None|12|3|Gain Magic Ward with +25% Magical Defense and +20% Holy Resistance for 2 Actions.|
|II|Blessed Renewal|Self|1|None|12|3|Gain Regeneration that restores 7% Max HP at the end of your next 3 Actions.|
|III|Solar Verdict|All Enemies|3|M110 Holy|20|4|50% chance to apply Holy Mark for 2 Actions to each target.|
|III|Sanctified Judgment|Enemy|1|M140 Holy|20|4|Deals 25% more final Damage when the target has Holy Mark or Magic Vulnerability.|

---

# Passive Skill System

## Passive Slot Rules

|Rule|Implementation|
|---|---|
|Player Passive Slots|The Player has exactly 3 Passive Skill Slots.|
|Equipped Passive Limit|At most 3 learned Passive Skills may be active from the Player Skill System.|
|Mythic Weapon Passive Grants|A Mythic Weapon can grant at most 2 additional Weapon Passive Effects.|
|Trait Interaction|Weapon Passive Effects are separate from learned Passive Skills and do not use a Passive Skill Slot.|
|Total Passive Limit|At most 5 passive effects can be active:3 Player Passives plus up to 2 Mythic Weapon Passives.|
|Duplicate Named Passive|The same named Passive cannot be active twice. Use the strongest value only.|
|Equipment Requirement|A Weapon,Armor,or Elemental Passive turns off immediately when its requirement is no longer met.|
|No Combat Changes|Passive Slot choices cannot be changed during combat.|
|Outside Combat Changes|Passive Skills can be equipped or removed in the Player Menu outside combat.|
|Mythic Weapon Change|Changing the Mythic Weapon immediately removes the passive effects granted by the old Weapon.|

## General Passives

|Passive|Requirement|Effect|
|---|---|---|
|Physical Conditioning|None|Gain +10% Max Health.|
|Arcane Discipline|None|Gain +10% Max Mana.|
|Combat Training|None|Gain +5% Physical Attack.|
|Arcane Training|None|Gain +5% Magic Power.|
|Iron Skin|None|Gain +5% Defense.|
|Arcane Shell|None|Gain +5% Magical Defense.|
|Fleet Footwork|None|Gain +5% Speed.|
|Steady Aim|None|Gain +5% Accuracy.|
|Evasion Training|None|Gain +5% Evasion.|
|Critical Focus|None|Gain +5% Critical Chance.|
|Enduring Will|None|Gain +10% Global Status Resistance.|
|Field Medicine|None|Gain +10% Healing Received.|
|Potion Training|None|Health and Mana Potions restore 15% more of their fixed HP/MP amount; Full Potions are unaffected.|
|Alchemist's Pouch|None|Once per combat, after using a Potion, immediately use one different Potion without consuming a second Player action. Both Items still obey their own cooldowns and cannot be the same item.|
|Treasure Sense|None|Gain +10% Gold Find and +5% Item Find if those reward modifiers are implemented.|

## Weapon and Armor Passives

|Passive|Requirement|Effect|
|---|---|---|
|Melee Mastery|Sword,Great Sword,Axe,Hammer,or Dagger equipped|Gain +8% Physical Attack.|
|Ranged Mastery|Bow equipped|Gain +8% Physical Attack and +5% Accuracy.|
|Staff Mastery|Staff equipped|Gain +8% Magic Power.|
|Shield Mastery|Shield equipped|Gain +8% Defense and +8% Magical Defense.|
|Sword Discipline|Sword equipped|Gain +5% Accuracy and +5% Critical Chance.|
|Great Sword Discipline|Great Sword equipped|Gain +10% Physical Attack and -5% Speed.|
|Axe Discipline|Axe equipped|Gain +10% Bleeding Chance from Axe Skills.|
|Hammer Discipline|Hammer equipped|Gain +10% Stun Chance from Hammer Skills.|
|Dagger Discipline|Dagger equipped|Gain +10% Poison Chance from Dagger Skills.|
|Bow Discipline|Bow equipped|Gain +10% Accuracy for Bow Skills.|
|Light Armor Training|Light Armor equipped|Gain +8% Evasion and +5% Speed.|
|Normal Armor Training|Normal Armor equipped|Gain +6% Defense and +6% Magical Defense.|
|Heavy Armor Training|Heavy Armor equipped|Gain +12% Defense and +10% Stun Resistance.|
|Robe Training|Robe equipped|Gain +10% Magic Power and +10% Magical Defense.|

## Elemental Passives

|Passive|Requirement|Effect|
|---|---|---|
|Earth Affinity|Earth Magic unlocked|Gain +10% Earth Damage and +10% Earth Resistance.|
|Air Affinity|Air Magic unlocked|Gain +10% Air Damage and +10% Air Resistance.|
|Water Affinity|Water Magic unlocked|Gain +10% Water Damage and +10% Water Resistance.|
|Fire Affinity|Fire Magic unlocked|Gain +10% Fire Damage and +10% Fire Resistance.|
|Darkness Affinity|Darkness Magic unlocked|Gain +10% Darkness Damage and +10% Darkness Resistance.|
|Holy Affinity|Holy Magic unlocked|Gain +10% Holy Damage and +10% Holy Resistance.|
|Stone Heart|Earth Magic unlocked|Gain +10% Barrier Strength.|
|Windwalker|Air Magic unlocked|Gain +10% Speed.|
|Tidekeeper|Water Magic unlocked|Restore 3% of Max Mana at the end of every Player Action.|
|Flamecaller|Fire Magic unlocked|Gain +10% Burn Chance from Fire Magic Skills.|
|Nightwalker|Darkness Magic unlocked|Gain +10% Curse Chance from Darkness Magic Skills.|
|Dawnkeeper|Holy Magic unlocked|Gain +10% Healing Received and +10% Holy Mark Chance from Holy Magic Skills.|

---

# Mythic Weapon Passive Grants

A Mythic Weapon may grant up to 2 Weapon Passive Effects through its Trait System.

These are not learned Player Passives.

|Rule|Implementation|
|---|---|
|Maximum|One Mythic Weapon can grant 0,1,or 2 Weapon Passive Effects.|
|Passive Slot Cost|Weapon Passive Effects use 0 Player Passive Slots.|
|Compatibility|A Weapon Passive Effect must match the Weapon's Type,Combat Style,and Element Types.|
|Trait Source|A Weapon Passive Effect may come from a compatible Mythic Trait or a future Mythic Weapon-specific passive roll.|
|Duplicate Rule|It cannot duplicate a learned equipped Passive or another Weapon Passive Effect by name.|
|Removal|Unequipping the Mythic Weapon removes all passive effects granted by that Weapon.|
|Balance Limit|The weapon cannot grant more than 2 passive effects even if it has more Trait effects.|

## Example

```text
Player Passive Slots:
1. Staff Mastery
2. Arcane Discipline
3. Water Affinity

Mythic Water Staff Passive Effects:
1. +12% Water Damage
2. Restore 4% Max Mana after direct Water Magic Damage

Total Active Passive Effects:
5
```

---

# Skill Resolution Rules

## Physical Skill Resolution

```text
1. Check Weapon,Shield,or Armor Requirement.
2. Check Current Mana against Mana Cost.
3. Check Skill Cooldown.
4. Check target validity and Max Targets.
5. Spend Mana.
6. Use Physical Hit Chance for every selected target.
7. If a target is hit,check Physical Critical Chance for that target.
8. Resolve Physical Damage.
9. Resolve the Skill's listed Status Chance or Buff.
10. Put the Skill on its listed Cooldown.
```

## Magic Skill Resolution

```text
1. Check Staff Requirement.
2. Check Current Mana against Mana Cost.
3. Check Skill Cooldown.
4. Check target validity and Max Targets.
5. Spend Mana.
6. Magic Damage automatically hits every selected target.
7. Magic Damage cannot Crit.
8. Resolve Magic Damage.
9. Resolve the Skill's listed Status Chance or Buff.
10. Put the Skill on its listed Cooldown.
```

## Support Skill Resolution

```text
1. Check Equipment Requirement,Mana Cost,and Cooldown.
2. Check target validity and Max Targets.
3. Check whether the target already has the same Buff.
4. Spend Mana.
5. Apply the Buff,Barrier,Heal,Cleanse,or Regeneration.
6. Do not reduce Duration during the Action in which the effect was applied.
7. Put the Skill on its listed Cooldown.
```

## Multi-Target Resolution

```text
For All Enemies Skills:

1. Select every living Enemy.
2. Limit targets to 3.
3. Resolve each target separately.
4. Physical Skills roll Hit Chance and Critical Chance separately for each target.
5. Magic Skills hit every target automatically.
6. Status Resistance is calculated separately for each target.
```

---

# Recommended Character Build Examples

## Sword and Shield Defender

|Type|Suggested Skills or Passives|
|---|---|
|Active Skills|Duelist Slash,Guard Stance,Barrier Wall,Iron Wall,Earth Bolt,Fortress of Stone|
|Equipped Passives|Shield Mastery,Heavy Armor Training,Stone Heart|
|Mythic Weapon Passives|Up to 2 compatible Shield or Earth Weapon Passive Effects|
|Role|Physical defense,Barrier protection,and Earth control.|

## Dagger and Light Armor Assassin

|Type|Suggested Skills or Passives|
|---|---|
|Active Skills|Backstab,Venom Cut,Shadowstep,Quick Strike,Windpiercer,Blind Shot|
|Equipped Passives|Dagger Discipline,Light Armor Training,Critical Focus|
|Mythic Weapon Passives|Up to 2 compatible Dagger passive effects|
|Role|Fast physical Damage,Critical Hits,Poison,and Evasion.|

## Fire Staff Damage Caster

|Type|Suggested Skills or Passives|
|---|---|
|Active Skills|Fire Bolt,Flame Wave,Flame Focus,Scorching Brand,Infernal Nova,Combustion|
|Equipped Passives|Staff Mastery,Arcane Training,Fire Affinity|
|Mythic Weapon Passives|Up to 2 compatible Fire Staff passive effects|
|Role|High direct Fire Damage,Burn,and Scorched pressure.|

## Water and Holy Sustain Caster

|Type|Suggested Skills or Passives|
|---|---|
|Active Skills|Frost Lance,Flowing Recovery,Heal,Purifying Light,Judgment Beam,Blessed Renewal|
|Equipped Passives|Staff Mastery,Water Affinity,Holy Affinity|
|Mythic Weapon Passives|Up to 2 compatible Water or Holy Staff passive effects|
|Role|Freeze,Wet,Regeneration,Healing,and Cleanse.|

## Air Bow Controller

|Type|Suggested Skills or Passives|
|---|---|
|Active Skills|Aimed Shot,Blind Shot,Pinning Shot,Hunter's Mark,Rain of Arrows,Windpiercer|
|Equipped Passives|Ranged Mastery,Bow Discipline,Air Affinity|
|Mythic Weapon Passives|Up to 2 compatible Air Bow passive effects|
|Role|Accuracy,Blind,Slow,Marks,and multi-target pressure.|

---

# Quick Reference

```text
Basic Attack:
0 Mana
0 Cooldown
Always available

Physical,Armor,and Shield Skills:
Use Mana
Use Cooldowns
Physical Damage can miss and Crit

Magic Skills:
Use Mana
Use Cooldowns
Always hit
Cannot Crit

Active Skills:
No Active Skill Slots
Every learned valid Skill is usable

Passive Skills:
3 equipped Player Passive Slots
Up to 2 additional Passive Effects from a Mythic Weapon
Maximum 5 active passive effects
```

```text
Maximum Targets:

Self = 1
Enemy = 1
All Enemies = 3
```

---

## Documentation Links

This preserved source is retained in full. The canonical integrated design is in
[04_Player_and_Skills.md](04_Player_and_Skills.md); the documentation index is [00_README.md](00_README.md).
Where this source conflicts with newer documents, see
[16_Consistency_Audit.md](16_Consistency_Audit.md) rather than deleting this record.


---

## Tier IV–VI Martial and Ranged Skills

|Tier|Skill|Requirement|Target|Damage / Mana / CD|Exact description|
|---|---|---|---|---|---|
|I|Guarding Strike|Sword, Great Sword, Axe, Hammer, or Dagger|Enemy|P85 Primary / 3 / 0|After a hit, gain Fortify +10% Defense and Magical Defense for 1 own action.|
|II|Serrated Lunge|Sword, Great Sword, Axe, or Dagger|Enemy|P105 Primary / 6 / 1|50% chance to apply Bleeding for 3 own actions.|
|II|Disarming Cut|Sword, Great Sword, Axe, Hammer, or Dagger|Enemy|P90 Primary / 6 / 2|60% chance to apply Weakness for 2 own actions.|
|III|Sweeping Break|Sword, Great Sword, Axe, or Hammer|All Enemies|P75 Primary / 9 / 3|Each hit resolves normally; 40% chance to apply Armor Break for 2 own actions to each hit target.|
|III|Combat Feint|Sword or Dagger|Self|None / 8 / 3|Gain Evasion Up +20% and Accuracy +15 for 2 own actions.|
|IV|Vanguard Slam|Sword, Great Sword, Axe, or Hammer|Enemy|P140 Primary / 13 / 3|Ignores 20% Defense and 60% chance to apply Crippled for 2 own actions.|
|IV|Relentless Rhythm|Any Melee Weapon|Self|None / 11 / 4|Gain Haste +20% Speed and Berserk +15% Physical Attack/-8% Defense for 2 own actions.|
|V|Execution Chain|Sword, Great Sword, Axe, Hammer, or Dagger|Enemy|P160 Primary / 17 / 4|Deals 30% more final Damage when target has Bleeding, Armor Break, Cracked, or Weakness.|
|V|Iron Resolve|Sword, Great Sword, Axe, or Hammer|Self|None / 15 / 4|Remove Weakness, Armor Break, Crippled, and Slow. Gain Fortify +25% for 2 own actions.|
|VI|Warbreaker|Sword, Great Sword, Axe, or Hammer|Enemy|P180 Primary / 24 / 5|Ignores 35% Defense; 75% chance Armor Break for 2 own actions. If it lands on an Armor-Broken target, gain 15% Barrier from Max HP.|
|VI|Predator’s Tempo|Dagger or Bow|Self|None / 20 / 5|Gain Haste +35% Speed, Evasion Up +20%, and +15% Critical Chance for 3 own actions.|
|II|Barbed Volley|Bow|All Enemies|P70 Primary / 7 / 2|Each target resolves a Physical hit; hit targets have 45% chance to receive Bleeding for 3 own actions.|
|IV|Piercing Gale|Bow|Enemy|P145 Air / 13 / 3|Ignores 30% Defense and 65% chance to apply Winded for 2 own actions.|
|V|Rain of Suppression|Bow|All Enemies|P95 Air / 16 / 4|Each target has 60% chance to receive Slow for 2 own actions after hit resolution.|
|VI|Horizon Splitter|Bow|Enemy|P175 Air / 24 / 5|Gain +30 Accuracy for this attack; ignores 40% Defense and has +25% Critical Chance for this attack.|

## Tier IV–VI Armor, Shield, Staff, Buff, Debuff, and Healing Skills

|Tier|Skill|Requirement|Target|Damage / Mana / CD|Exact description|
|---|---|---|---|---|---|
|II|First Aid|Light Armor, Normal Armor, Heavy Armor, or Robe|Self|None / 7 / 3|Restore 12% Max HP and remove Bleeding. This is a Skill, not a Potion.|
|III|Guarded Recovery|Normal Armor or Heavy Armor|Self|None / 10 / 4|Restore 15% Max HP and gain Fortify +15% Defense and Magical Defense for 2 own actions.|
|IV|Mobile Guard|Light Armor|Self|None / 12 / 4|Gain Evasion Up +30% and Haste +20% for 2 own actions; remove Rooted.|
|IV|Formation Guard|Normal Armor|Self|None / 12 / 4|Gain Fortify +25% Defense and Magical Defense and Magic Ward +15% Magical Defense for 2 own actions.|
|IV|Iron Bastion|Heavy Armor|Self|None / 14 / 5|Create Barrier equal to 20% Max HP and gain +20% Stun, Freeze, and Crippled Resistance for 2 own actions.|
|IV|Restorative Weave|Robe|Self|None / 12 / 4|Gain Regeneration restoring 8% Max HP at end of next 3 own actions and restore 10% Max Mana.|
|V|Emergency Ward|Any Armor|Self|None / 17 / 5|When current HP is 50% or lower, create Barrier equal to 28% Max HP and remove one negative Status; fails if HP exceeds 50%.|
|V|Shared Discipline|Normal Armor or Heavy Armor|Self|None / 16 / 5|Gain Fortify +30% and +20% Global Status Resistance for 3 own actions.|
|VI|Unyielding Form|Heavy Armor|Self|None / 24 / 6|Create Barrier equal to 35% Max HP; gain Fortify +35% and Damage Reduction +12% for 3 own actions.|
|VI|Sage’s Sanctuary|Robe|Self|None / 22 / 6|Restore 30% Max HP, restore 25% Max Mana, remove up to 2 negative effects, and gain Magic Ward +30% for 2 own actions.|
|III|Interception|Shield in either hand|Self|None / 10 / 3|Gain Barrier equal to 12% Max HP. While active, gain +15% Damage Reduction for 2 own actions.|
|IV|Shield Quake|Shield in either hand|All Enemies|P90 Earth / 13 / 3|Each hit target has 50% chance to receive Cracked for 2 own actions.|
|V|Aegis Recovery|Shield in either hand|Self|None / 17 / 5|Create Barrier equal to 25% Max HP; restore 15% Max HP; gain Magic Ward +20% for 2 own actions.|
|VI|Citadel Pulse|Shield in either hand|All Enemies|P110 Holy / 24 / 6|Each hit target has 55% chance to receive Holy Mark; Player gains Barrier equal to 25% Max HP.|
|IV|Arcane Burst|Staff|Enemy|M145 Neutral / 15 / 3|Always hits. If target has Magic Break or Magic Vulnerability, deal 25% more final Damage.|
|V|Mana Spring|Staff|Self|None / 0 / 5|Restore 30% Max Mana and gain Mana Regeneration restoring 5% Max Mana at end of next 3 own actions.|
|VI|Runic Collapse|Staff|All Enemies|M115 Neutral / 24 / 6|Always hits; 60% chance to apply Magic Break for 2 own actions to each target.|

## Tier IV–VI Elemental Magic Skills

Each Elemental School requires a Staff in Main Hand. The listed tier must be globally unlocked and the corresponding magic school must already be learned through its first elemental region.

|School / Tier|Skill|Target|Damage / Mana / CD|Exact description|
|---|---|---|---|---|
|Earth IV|Granite Lance|Enemy|M140 Earth / 15 / 3|60% chance to apply Cracked for 2 own actions. If target is Rooted, deal +20% final Damage.|
|Earth V|Living Rampart|Self|None / 17 / 5|Create Barrier equal to 25% Max HP and gain Fortify +25% for 3 own actions.|
|Earth VI|World Pillar|All Enemies|M125 Earth / 24 / 6|55% chance Rooted and 45% chance Cracked for 2 own actions, rolled separately per target.|
|Air IV|Cyclone Spear|Enemy|M140 Air / 15 / 3|65% chance to apply Winded for 2 own actions. Magic Damage always hits; this Skill does not use an Accuracy roll.|
|Air V|Mistwalk|Self|None / 16 / 5|Gain Haste +35% Speed and Evasion Up +25% for 3 own actions.|
|Air VI|Skyfall|All Enemies|M125 Air / 24 / 6|60% chance Blind and 50% chance Slow for 2 own actions, rolled separately per target.|
|Water IV|Rime Volley|All Enemies|M100 Water / 15 / 3|Apply Wet for 2 own actions; 45% chance Freeze for 1 own action per target.|
|Water V|Deep Current|Self|None / 17 / 5|Restore 25% Max HP, gain Regeneration 8% Max HP for 3 own actions, and +25% Water Resistance for 3 own actions.|
|Water VI|Absolute Tides|Enemy|M165 Water / 24 / 6|Apply Wet for 2 own actions; if target is already Wet, deal +35% final Damage and 65% chance Freeze for 1 own action.|
|Fire IV|Searing Comet|Enemy|M150 Fire / 15 / 3|70% chance Burn for 3 own actions and 50% chance Scorched for 2 own actions; roll both separately.|
|Fire V|Phoenix Ward|Self|None / 17 / 5|Gain +35% Fire Resistance, Focus +25% Magic Power/+15 Accuracy, and Regeneration 5% Max HP for 3 own actions.|
|Fire VI|Cataclysm|All Enemies|M145 Fire / 25 / 6|70% chance Burn for 3 own actions; targets with Burn or Scorched take +30% final Damage.|
|Darkness IV|Umbral Cage|Enemy|M130 Darkness / 15 / 3|Apply Shadow Mark for 2 own actions and 55% chance Fear for 1 own action.|
|Darkness V|Siphon Veil|Self|None / 16 / 5|Gain Lifesteal +12% and Evasion Up +20% for 3 own actions.|
|Darkness VI|Eclipsing Ruin|All Enemies|M130 Darkness / 25 / 6|Apply Shadow Mark; 55% chance Magic Break for 2 own actions. Restore HP equal to 20% of Health Damage dealt across all targets.|
|Holy IV|Halo Lance|Enemy|M145 Holy / 15 / 3|65% chance Holy Mark and 55% chance Magic Vulnerability for 2 own actions.|
|Holy V|Divine Shelter|Self|None / 17 / 5|Restore 25% Max HP, create Barrier equal to 18% Max HP, and gain +20% Holy Resistance for 3 own actions.|
|Holy VI|Dawn Rebirth|Self|None / 25 / 6|Restore 45% Max HP, remove all removable negative effects, and gain Regeneration 8% Max HP for 3 own actions.|

## Advanced Passive Skills

|Passive|Requirement|Cost|Exact effect|Build role|
|---|---|---:|---|---|
|Two-Hand Discipline|Two-hand weapon equipped|2|Gain +10% damage with the equipped two-hand weapon; lose no extra Defense beyond the item’s own values.|Damage|
|Dual-Wield Rhythm|Two one-hand weapons equipped|2|Off-hand offensive contribution becomes 60% instead of 50%; gain +5% Speed.|Speed / damage|
|Bulwark Training|Shield equipped|2|Gain +12% Barrier Strength and +8% Damage Reduction while Barrier is active.|Defense|
|Combat Medic|Any Armor|2|Healing Skills and Potions restore +15% more HP.|Heal|
|Debilitating Precision|Dagger, Bow, or Staff|2|Gain +10 percentage points to skill-applied Weakness, Blind, Crippled, Magic Break, or Magic Vulnerability chances.|Debuff|
|Status Hunter|Any weapon|2|Deal +12% final Damage to targets with any negative Status.|Damage / debuff|
|Evasive Instinct|Light Armor equipped|2|After a Physical evade, gain +10 Accuracy and +10% Critical Chance for 1 own action.|Evasion|
|Battle Alchemy|None|2|Buff Potions last +1 own action; healing Potions remove one additional matching DoT when applicable.|Buff / heal|
|Elemental Conduit|Staff equipped|3|Gain +8% Damage for a Skill whose Elemental School is unlocked. This bonus does not stack once per unlocked school; each Skill checks only its own matching School.|Elemental damage|
|Wardbreaker|Physical weapon or Staff|3|Gain +10% Physical and Magic Penetration against targets with Barrier.|Damage|
|Merciful Light|Holy Magic unlocked|3|When you restore HP with a Skill, gain 4% Max Mana; once per own action.|Heal / sustain|
|Shadow Opportunist|Darkness Magic unlocked|3|After applying Fear, Silence, or Confusion, gain Focus +15% Magic Power and Accuracy for 1 own action.|Debuff / magic|

## Equipment validity matrix

|Skill category|Required equipment / state|Cannot be used when|
|---|---|---|
|Sword / Great Sword / Axe / Hammer / Dagger skills|Matching main-hand Weapon type.|The matching Weapon is not in Main Hand or a two-hand conflict exists.|
|Bow skills|Two-hand Bow in Main Hand.|Any other Main Hand weapon; Off Hand remains locked.|
|Staff / Elemental skills|Two-hand Staff in Main Hand.|Silenced, no Staff, insufficient Mana, or cooldown active.|
|Shield skills|Shield in Main Hand or Off Hand.|No equipped Shield.|
|Light / Normal / Heavy / Robe skills|Matching Armor type equipped.|Another armor type equipped.|
|General Melee|Sword, Great Sword, Axe, Hammer, or Dagger in Main Hand.|Bow/Staff/Shield-only loadout.|
|General Ranged|Bow in Main Hand.|No Bow.|
|Passives|Exact item/school requirement while equipped/unlocked.|The requirement stops being true; passive turns off immediately.|



## Passive compatibility list

This table is the single lookup for which passive is valid with each Weapon or Armor type. A passive turns off immediately if its requirement is no longer valid.

|Passive category|Valid equipment / condition|Examples|
|---|---|---|
|General|No equipment requirement.|Physical Conditioning; Arcane Discipline; Potion Training; Alchemist's Pouch; Combat Medic.|
|Sword|Sword in Main Hand.|Melee Mastery; Sword Discipline; Two-Hand Discipline does not apply.|
|Great Sword|Great Sword in Main Hand.|Melee Mastery; Great Sword Discipline; Two-Hand Discipline.|
|Axe|Axe in Main Hand.|Melee Mastery; Axe Discipline; Two-Hand Discipline only for a two-hand Axe.|
|Hammer|Hammer in Main Hand.|Melee Mastery; Hammer Discipline; Two-Hand Discipline only for a two-hand Hammer.|
|Dagger|Dagger in Main Hand; Dual-Wield Rhythm additionally requires two one-hand Weapons.|Melee Mastery; Dagger Discipline; Debilitating Precision; Evasive Instinct with Light Armor.|
|Bow|Bow in Main Hand.|Ranged Mastery; Bow Discipline; Two-Hand Discipline; Debilitating Precision.|
|Staff|Staff in Main Hand.|Staff Mastery; Elemental Conduit; Wardbreaker; elemental Affinities.|
|Shield|Shield in either hand.|Shield Mastery; Bulwark Training.|
|Light Armor|Light Armor equipped.|Light Armor Training; Evasive Instinct.|
|Normal Armor|Normal Armor equipped.|Normal Armor Training; Combat Medic.|
|Heavy Armor|Heavy Armor equipped.|Heavy Armor Training; Bulwark Training; Combat Medic.|
|Robe|Robe equipped.|Robe Training; Combat Medic; elemental Affinities when school is unlocked.|
|Elemental school|The named Magic School is unlocked.|Earth/Air/Water/Fire/Darkness/Holy Affinity; Stone Heart; Windwalker; Tidekeeper; Flamecaller; Nightwalker; Dawnkeeper; Merciful Light; Shadow Opportunist.|

## Equipment Grade Passives

Equipment-owned Grade Passives do not consume any of the three learned Passive slots. A non-two-hand Mythic Weapon, Shield, or Armor can grant two Grade Passives total. A Mythic two-hand Weapon grants three Grade Passives total. These effects are detailed in [Equipment](05_Equipment_and_Drop_Pools.md) and are separately rerolled at the Enchanter under [Blacksmith and Enchanter](08_Blacksmith_and_Enchanter.md).

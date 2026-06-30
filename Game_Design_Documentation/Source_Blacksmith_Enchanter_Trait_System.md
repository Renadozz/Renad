# Blacksmith,Enchanter,and Weapon Trait System

## Purpose

This document defines the full upgrade system for Equipment and the random Weapon Trait system gained from Epic,Legendary,and Mythic Grade upgrades.

|System|Result|
|---|---|
|Blacksmith|Raises every numeric value that belongs to the original `+0` Item.|
|Enchanter|Adds a Grade Bonus after Blacksmith scaling.|
|Epic Grade|Adds exactly 1 random compatible Epic Trait to a Weapon.|
|Legendary Grade|Keeps all existing Traits and adds exactly 1 random compatible Legendary Trait.|
|Mythic Grade|Keeps all existing Traits and adds exactly 1 random compatible Mythic Trait.|
|Equipment Drops|Normal,Elite,Boss,Quest,and Market Equipment can drop only from Common through Epic.|
|Legendary and Mythic|Can only be created through successful Enchanter upgrades.|

---

# Core Upgrade Rules

## Blacksmith Scaling

The Blacksmith scales every numeric value that originally belongs to the `+0` Item. This includes flat stats,percentage-point bonuses,and the numerical values of original built-in passives.

```text
Upgrade Multiplier =
1 + (Upgrade Level × 0.10)
```

```text
Blacksmith Flat Stat =
Floor(Original +0 Flat Stat × Upgrade Multiplier)
```

```text
Blacksmith Percentage Value =
RoundToOneDecimal(Original +0 Percentage Value × Upgrade Multiplier)
```

|Upgrade Level|Total Bonus from +0|Multiplier|
|---|---|---|
|+0|+0%|1.00|
|+1|+10%|1.10|
|+2|+20%|1.20|
|+3|+30%|1.30|
|+4|+40%|1.40|
|+5|+50%|1.50|

All Blacksmith calculations always use the original `+0` Item values. They never use the previous upgrade result as a new base.

## Enchanter Grade Bonus

The Grade Bonus applies after Blacksmith scaling. It raises every numeric original Item value but never alters a Trait value.

```text
Grade Bonus Amount =
Floor(Blacksmith Base Stat × Grade Bonus Percentage)
```

```text
Final Flat Item Stat =
Blacksmith Base Stat + Grade Bonus Amount
```

```text
Final Percentage Item Value =
RoundToOneDecimal(Blacksmith Percentage Value × (1 + Grade Bonus Percentage))
```

|Grade|Grade Bonus|Trait Added on Successful Upgrade|
|---|---|---|
|Common|+0%|None|
|Uncommon|+10%|None|
|Rare|+20%|None|
|Epic|+30%|1 random compatible Epic Trait|
|Legendary|+40%|1 random compatible Legendary Trait|
|Mythic|+50%|1 random compatible Mythic Trait|

## Trait Values Do Not Scale

|Value Source|Affected by Blacksmith?|Affected by Grade Bonus?|
|---|---|---|
|Original +0 Physical Attack,Magic Power,Defense,Magical Defense,Max Health,Speed|Yes|Yes|
|Original +0 Accuracy,Evasion,Critical Chance,Penetration,Resistance,and similar percentage values|Yes|Yes|
|Original built-in passive numeric values|Yes|Yes|
|Epic,Legendary,and Mythic Trait roll values|No|No|
|Trait duration,trigger condition,and target rule|No|No|

> A Trait rolls its value once when it is gained. That rolled value stays fixed on that individual Weapon.


---

# Weapon Trait Progression

|Successful Grade Upgrade|Trait Result|
|---|---|
|Rare → Epic|Add 1 Epic Trait.|
|Epic → Legendary|Keep the Epic Trait and add 1 Legendary Trait.|
|Legendary → Mythic|Keep all prior Traits and add 1 Mythic Trait.|

A Mythic Weapon therefore has exactly 3 Grade Traits: 1 Epic,1 Legendary,and 1 Mythic.

|Rule|Implementation|
|---|---|
|Weapons Only|Traits are granted only to Sword,Great Sword,Axe,Hammer,Staff,Bow,Dagger,and Shield.|
|No Trait Reroll|A successful Grade upgrade permanently assigns the Trait and its rolled value.|
|No Trait Loss|Failed enchantments never remove existing Traits.|
|No Duplicate Family|A Weapon cannot receive two Traits with the same Family.|
|Original Passives|Original Item passives remain separate from Grade Traits and may coexist with them.|
|No Invalid Element|A Trait requiring Fire can only be selected for a Weapon with Fire in its Element Types.|
|No Invalid Magic Trait|Magic-specific Traits can only be selected for Staff.|
|No Invalid Physical Trait|Physical-only Traits cannot be selected for Staff.|

---

# Weapon Compatibility Profile

Every Weapon must store the following trait-selection fields.

|Field|Examples|Purpose|
|---|---|---|
|Weapon Type|Sword,Great Sword,Axe,Hammer,Staff,Bow,Dagger,Shield|Filters traits by Allowed Weapons.|
|Combat Style|Physical or Magic|Prevents Magic-only traits from appearing on physical Weapons.|
|Element Types|Fire;Water;Earth;Air;Holy;Darkness|Filters elemental traits.|
|Primary Element|The first listed Element Type|Used by Primary Element Traits.|
|Existing Trait Families|Bleeding;Barrier;Elemental Damage|Prevents duplicate Families.|
|Existing Trait IDs|E01;L33;M17|Prevents duplicate Traits.|

## Compatibility Rules

|Trait Requirement|Weapon Must Have|
|---|---|
|Required Element = None|No elemental requirement.|
|Required Element = Fire,Water,Earth,Air,Holy,or Darkness|That exact Element must be in the Weapon's Element Types.|
|Required Element = Weapon Primary Element|The Weapon must have at least one Element Type;the Trait uses its first listed Element.|
|Allowed Weapons = All Weapons|Any Weapon Type may use the Trait if all other requirements are valid.|
|Allowed Weapons = Staff|Only a Staff may use the Trait.|
|Allowed Weapons excludes Staff|The Trait cannot appear on a Staff.|

> A Water Weapon cannot receive `Firebrand`,`Cinder Scar`,`Infernal Brand`,or any other Fire-required Trait. A Sword,Axe,Hammer,Bow,Dagger,or Shield cannot receive Staff-only Magic Traits.


---

# Trait Selection Formula

## Step 1: Build the Candidate List

```text
Eligible Traits =
All Traits where:

Trait Grade = New Grade
AND Weapon Type is in Trait Allowed Weapons
AND Required Element is None
    OR Required Element exists in Weapon Element Types
    OR Required Element = Weapon Primary Element and Weapon has an Element
AND Trait Family is not already on the Weapon
AND Trait ID is not already on the Weapon
```

## Step 2: Select the Trait

All valid candidates have equal chance by default.

```text
Selected Index =
Floor(Random(0,1) × Count(Eligible Traits))

Selected Trait =
Eligible Traits[Selected Index]
```

`Random(0,1)` returns a decimal from `0.000` up to,but not including,`1.000`.

## Step 3: Roll the Trait Value

Every Trait table uses `[R]` as its rolled value.

```text
RandomInteger(Minimum,Maximum) =
Minimum + Floor(
Random(0,1) × (Maximum - Minimum + 1)
)
```

```text
Trait Value R =
RandomInteger(Trait Minimum,Trait Maximum)
```

Example:

```text
Selected Trait = Firebrand
Roll Range = 12-18%

Random(0,1) = 0.64

R = 12 + Floor(0.64 × (18 - 12 + 1))
R = 12 + Floor(4.48)
R = 16

Final Trait:
On a direct Fire hit,roll 16% to apply Burn for 3 Actions.
```

## Step 4: Store the Result

```text
Weapon Trait Entry =
{
Trait ID,
Trait Name,
Trait Grade,
Trait Family,
Rolled Value R,
Trigger,
Effect,
Duration
}
```


---

# Trait Resolution Rules

## Status Trait Resolution

A Trait that applies a negative Status uses the existing Status Resistance rule.

```text
Trait Base Status Chance = R

Final Trait Status Chance =
Clamp(
R - Target Total Status Resistance,
0%,
100%
)
```

```text
Apply the Status when:
RollChance(Final Trait Status Chance) = True
```

## Trigger Order

```text
1. Resolve the selected Skill or Basic Attack.
2. Resolve its direct Damage and its own Status Effects.
3. Resolve valid Trait triggers from the Weapon.
4. For each Trait that applies a Status:
   - Skip it if the target already has that same Status.
   - Calculate Final Trait Status Chance.
   - Roll the chance.
5. Apply active Trait Buffs,Barriers,Healing,or Mana effects.
```

|Rule|Implementation|
|---|---|
|Direct Hit|A Trait marked `On a direct hit` does not trigger from Burn,Poison,Bleeding,Curse,or other Damage-Over-Time.|
|Status Reapplication|Traits obey the normal rule: do not apply the same Status if it still has at least 1 Action remaining.|
|Trait Status Limit|A Weapon can apply at most 1 additional negative Status from Traits per Action.|
|Multiple Successful Status Traits|Resolve Mythic first,then Legendary,then Epic. Skip lower-tier Status Traits after one Trait Status is applied.|
|Buff Traits|Non-status Buffs,Barrier,Healing,Mana Recovery,and passive stat Traits can resolve normally alongside a Status Trait.|
|Trait Criticals|Traits do not create extra Critical rolls. They only react to a Critical when their trigger says so.|
|Trait Values|The rolled `[R]` value does not change after later Blacksmith or Enchanter upgrades.|

## Standard Durations

|Effect|Trait Duration|
|---|---|
|Burn,Poison,Bleeding,Curse|3 Actions|
|Weakness,Magic Break,Armor Break,Magic Vulnerability,Blind,Slow,Crippled,Wet,Scorched,Cracked,Winded,Shadow Mark,Holy Mark|2 Actions|
|Stun,Freeze,Sleep,Confusion,Fear,Silence|1 Action|
|Haste,Focus,Fortify,Evasion Up,Magic Ward|As written in the Trait.|
|Barrier|As written in the Trait or until depleted.|
|Regeneration|As written in the Trait.|

---

# Trait Strength Bands

|Trait Category|Epic Range|Legendary Range|Mythic Range|
|---|---|---|---|
|Permanent Accuracy or Elemental Damage|+5% to +16%|+12% to +26%|+22% to +40%|
|Temporary Stat Buff|+8% to +15%|+15% to +28%|+30% to +45%|
|Regular Status Chance|+10% to +20%|+22% to +38%|+35% to +60%|
|Hard Control Status Chance|+6% to +12%|+18% to +25%|+30% to +40%|
|Barrier|8% to 12% Max Health|15% to 22% Max Health|25% to 35% Max Health|
|Lifesteal|+3% to +5%|+6% to +9%|+10% to +14%|
|Mana Recovery|3% to 5% Max Mana|7% to 10% Max Mana|12% to 16% Max Mana|

---

# Epic Trait Pool

Each successful `Rare → Epic` upgrade adds exactly 1 random compatible Trait from this pool.

|ID|Trait|Allowed Weapons|Required Element|Family|Effect|Roll Range|
|---|---|---|---|---|---|---|
|E01|Keen Edge|Sword,Dagger,Bow|None|Accuracy|While equipped,gain +R% Accuracy.|5-9%|
|E02|Bloodlet Edge|Sword,Great Sword,Axe,Dagger|None|Bleeding|On a direct Physical hit,roll R% to apply Bleeding for 3 Actions.|12-18%|
|E03|Sundered Edge|Sword,Great Sword,Axe,Hammer|None|Armor Break|On a direct Physical hit,roll R% to apply Armor Break for 2 Actions.|10-16%|
|E04|Momentum Grip|Sword,Great Sword,Axe,Hammer|None|Physical Attack|After the first direct Physical hit each battle,gain +R% Physical Attack for 2 own Actions.|8-12%|
|E05|Swift Assault|Sword,Dagger,Bow|None|Haste|After a Physical Critical Hit,gain Haste with +R% Speed for 1 own Action.|10-15%|
|E06|Iron Stance|Sword,Great Sword,Hammer,Shield|None|Fortify|After using a direct Physical Skill,gain Fortify with +R% Defense and Magical Defense for 1 own Action.|10-15%|
|E07|Trueflight String|Bow|None|Bow Accuracy|Basic Attacks gain +R% Accuracy.|10-16%|
|E08|Weakening Fletching|Bow|None|Weakness|On a direct Physical hit,roll R% to apply Weakness for 2 Actions.|10-16%|
|E09|Hamstring Arrow|Bow|Air|Slow|On a direct Air Physical hit,roll R% to apply Slow for 2 Actions.|12-18%|
|E10|Pinning Barbs|Bow|Air|Crippled|On a direct Air Physical hit,roll R% to apply Crippled for 2 Actions.|10-16%|
|E11|Venom Edge|Dagger|None|Poison|On a direct Physical hit,roll R% to apply Poison for 3 Actions.|12-18%|
|E12|Phantom Step|Dagger|None|Evasion Up|After a Physical Critical Hit,gain Evasion Up with +R% Evasion for 1 own Action.|10-15%|
|E13|Whispering Cut|Dagger,Staff|Darkness|Curse|On a direct Darkness hit,roll R% to apply Curse for 3 Actions.|10-16%|
|E14|Arcane Focus|Staff|None|Focus|After using a direct Magic Skill,gain Focus with +R% Magic Power and Accuracy for 1 own Action.|10-15%|
|E15|Mana Well|Staff|None|Mana Recovery|After a direct Magic hit,restore R% of Max Mana.|3-5%|
|E16|Spell Fracture|Staff|None|Magic Break|On a direct Magic hit,roll R% to apply Magic Break for 2 Actions.|12-18%|
|E17|Runic Ward|Staff|None|Magic Ward|After using a direct Magic Skill,gain Magic Ward with +R% Magical Defense for 1 own Action.|10-15%|
|E18|Aegis Spark|Shield|None|Barrier|At battle start,create a Barrier equal to R% of Max Health.|8-12%|
|E19|Shield Rattle|Shield|None|Stun|On a direct Physical hit,roll R% to apply Stun for 1 Action.|8-12%|
|E20|Guarded Wall|Shield|None|Damage Reduction|While a Barrier is active,gain R% Damage Reduction.|4-7%|
|E21|Firebrand|All Weapons|Fire|Burn|On a direct Fire hit,roll R% to apply Burn for 3 Actions.|12-18%|
|E22|Cinder Scar|All Weapons|Fire|Scorched|On a direct Fire hit,roll R% to apply Scorched for 2 Actions.|12-18%|
|E23|Frostbrand|All Weapons|Water|Freeze|On a direct Water hit,roll R% to apply Freeze for 1 Action.|8-12%|
|E24|Tidal Mark|All Weapons|Water|Wet|On a direct Water hit,roll R% to apply Wet for 2 Actions.|14-20%|
|E25|Stonebind|All Weapons|Earth|Rooted|On a direct Earth hit,roll R% to apply Rooted for 2 Actions.|14-20%|
|E26|Crag Split|All Weapons|Earth|Cracked|On a direct Earth hit,roll R% to apply Cracked for 2 Actions.|14-20%|
|E27|Wind Lash|All Weapons|Air|Winded|On a direct Air hit,roll R% to apply Winded for 2 Actions.|14-20%|
|E28|Gale Veil|All Weapons|Air|Blind|On a direct Air hit,roll R% to apply Blind for 2 Actions.|12-18%|
|E29|Dread Touch|All Weapons|Darkness|Fear|On a direct Darkness hit,roll R% to apply Fear for 1 Action.|10-16%|
|E30|Night Sigil|All Weapons|Darkness|Shadow Mark|On a direct Darkness hit,roll R% to apply Shadow Mark for 2 Actions.|14-20%|
|E31|Radiant Brand|All Weapons|Holy|Holy Mark|On a direct Holy hit,roll R% to apply Holy Mark for 2 Actions.|14-20%|
|E32|Judgment Glint|All Weapons|Holy|Magic Vulnerability|On a direct Holy hit,roll R% to apply Magic Vulnerability for 2 Actions.|10-16%|
|E33|Leeching Rune|Sword,Great Sword,Axe,Hammer,Staff,Bow,Dagger|None|Lifesteal|Direct Damage dealt by this Weapon gains +R% Lifesteal.|3-5%|
|E34|Elemental Resonance|All Weapons|Weapon Primary Element|Elemental Damage|While equipped,gain +R% Damage for the Weapon's Primary Element.|5-8%|
|E35|Prismatic Ward|All Weapons|None|Elemental Ward|After receiving Elemental Damage,gain R% Resistance to that same Element for 2 own Actions.|10-15%|
|E36|Vital Renewal|All Weapons|None|Regeneration|After defeating an Enemy,gain Regeneration that heals R% of Max Health at the end of your next 2 Actions.|3-5%|
|E37|Drowsing Mist|Staff|Water|Sleep|On a direct Water Magic hit,roll R% to apply Sleep for 1 Action.|6-10%|

---

# Legendary Trait Pool

Each successful `Epic → Legendary` upgrade keeps the Epic Trait and adds exactly 1 random compatible Trait from this pool.

|ID|Trait|Allowed Weapons|Required Element|Family|Effect|Roll Range|
|---|---|---|---|---|---|---|
|L01|Razor Discipline|Sword,Dagger,Bow|None|Accuracy|While equipped,gain +R% Accuracy.|12-18%|
|L02|Crimson Rend|Sword,Great Sword,Axe,Dagger|None|Bleeding|On a direct Physical hit,roll R% to apply Bleeding for 3 Actions.|25-35%|
|L03|Sundering Fury|Sword,Great Sword,Axe,Hammer|None|Armor Break|On a direct Physical hit,roll R% to apply Armor Break for 2 Actions.|22-30%|
|L04|Warpath|Sword,Great Sword,Axe,Hammer|None|Physical Attack|After the first direct Physical hit each battle,gain +R% Physical Attack for 2 own Actions.|15-22%|
|L05|Relentless Tempo|Sword,Dagger,Bow|None|Haste|After a Physical Critical Hit,gain Haste with +R% Speed for 2 own Actions.|20-28%|
|L06|Bastion Counter|Sword,Great Sword,Hammer,Shield|None|Fortify|After using a direct Physical Skill,gain Fortify with +R% Defense and Magical Defense for 2 own Actions.|20-28%|
|L07|Eagle Eye|Bow|None|Bow Accuracy|Basic Attacks gain +R% Accuracy.|18-26%|
|L08|Tempest Arrow|Bow|Air|Blind|On a direct Air Physical hit,roll R% to apply Blind for 2 Actions.|25-35%|
|L09|Suppressing Shot|Bow|Air|Slow|On a direct Air Physical hit,roll R% to apply Slow for 2 Actions.|28-38%|
|L10|Sapping Fletching|Bow|None|Weakness|On a direct Physical hit,roll R% to apply Weakness for 2 Actions.|22-30%|
|L11|Master Venom|Dagger|None|Poison|On a direct Physical hit,roll R% to apply Poison for 3 Actions.|25-35%|
|L12|Shadowstep|Dagger|None|Evasion Up|After a Physical Critical Hit,gain Evasion Up with +R% Evasion for 2 own Actions.|20-28%|
|L13|Abyssal Hex|Staff|Darkness|Confusion|On a direct Darkness Magic hit,roll R% to apply Confusion for 1 Action.|18-25%|
|L14|Grand Focus|Staff|None|Focus|After using a direct Magic Skill,gain Focus with +R% Magic Power and Accuracy for 2 own Actions.|18-25%|
|L15|Arcane Reservoir|Staff|None|Mana Recovery|After a direct Magic hit,restore R% of Max Mana.|7-10%|
|L16|Spell Sundering|Staff|None|Magic Break|On a direct Magic hit,roll R% to apply Magic Break for 2 Actions.|25-35%|
|L17|Runic Bastion|Staff|None|Magic Ward|After using a direct Magic Skill,gain Magic Ward with +R% Magical Defense for 2 own Actions.|20-28%|
|L18|Aegis Core|Shield|None|Barrier|At battle start,create a Barrier equal to R% of Max Health.|15-22%|
|L19|Quaking Bash|Shield|Earth|Stun|On a direct Earth Physical hit,roll R% to apply Stun for 1 Action.|18-25%|
|L20|Bastion Plate|Shield|None|Damage Reduction|While a Barrier is active,gain R% Damage Reduction.|8-12%|
|L21|Infernal Brand|All Weapons|Fire|Burn|On a direct Fire hit,roll R% to apply Burn for 3 Actions.|25-35%|
|L22|Inferno Scar|All Weapons|Fire|Scorched|On a direct Fire hit,roll R% to apply Scorched for 2 Actions.|25-35%|
|L23|Glacial Prison|All Weapons|Water|Freeze|On a direct Water hit,roll R% to apply Freeze for 1 Action.|18-25%|
|L24|Undertow Mark|All Weapons|Water|Wet|On a direct Water hit,roll R% to apply Wet for 2 Actions.|28-38%|
|L25|Earth Shackle|All Weapons|Earth|Rooted|On a direct Earth hit,roll R% to apply Rooted for 2 Actions.|28-38%|
|L26|Faultline|All Weapons|Earth|Cracked|On a direct Earth hit,roll R% to apply Cracked for 2 Actions.|28-38%|
|L27|Tempest Lash|All Weapons|Air|Winded|On a direct Air hit,roll R% to apply Winded for 2 Actions.|28-38%|
|L28|Storm Silence|Staff|Air|Silence|On a direct Air Magic hit,roll R% to apply Silence for 1 Action.|18-25%|
|L29|Nightmare Touch|All Weapons|Darkness|Fear|On a direct Darkness hit,roll R% to apply Fear for 1 Action.|22-30%|
|L30|Abyssal Sigil|All Weapons|Darkness|Shadow Mark|On a direct Darkness hit,roll R% to apply Shadow Mark for 2 Actions.|28-38%|
|L31|Divine Brand|All Weapons|Holy|Holy Mark|On a direct Holy hit,roll R% to apply Holy Mark for 2 Actions.|28-38%|
|L32|Condemning Light|All Weapons|Holy|Magic Vulnerability|On a direct Holy hit,roll R% to apply Magic Vulnerability for 2 Actions.|22-30%|
|L33|Vampiric Rune|Sword,Great Sword,Axe,Hammer,Staff,Bow,Dagger|None|Lifesteal|Direct Damage dealt by this Weapon gains +R% Lifesteal.|6-9%|
|L34|Greater Resonance|All Weapons|Weapon Primary Element|Elemental Damage|While equipped,gain +R% Damage for the Weapon's Primary Element.|12-18%|
|L35|Prismatic Aegis|All Weapons|None|Elemental Ward|After receiving Elemental Damage,gain R% Resistance to that same Element for 2 own Actions.|20-28%|
|L36|Regrowth Seal|All Weapons|None|Regeneration|After defeating an Enemy,gain Regeneration that heals R% of Max Health at the end of your next 2 Actions.|6-9%|
|L37|Battle Trance|Sword,Great Sword,Axe,Hammer,Bow,Dagger|None|Berserk|When current Health is 40% or lower,gain Berserk with +R% Physical Attack and -10% Defense for 2 own Actions.|18-25%|

---

# Mythic Trait Pool

Each successful `Legendary → Mythic` upgrade keeps all existing Traits and adds exactly 1 random compatible Trait from this pool.

|ID|Trait|Allowed Weapons|Required Element|Family|Effect|Roll Range|
|---|---|---|---|---|---|---|
|M01|Flawless Edge|Sword,Dagger,Bow|None|Accuracy|While equipped,gain +R% Accuracy.|22-30%|
|M02|Blood Eclipse|Sword,Great Sword,Axe,Dagger|None|Bleeding|On a direct Physical hit,roll R% to apply Bleeding for 3 Actions.|42-55%|
|M03|Cataclysm Sunder|Sword,Great Sword,Axe,Hammer|None|Armor Break|On a direct Physical hit,roll R% to apply Armor Break for 2 Actions.|40-50%|
|M04|Tyrant's Momentum|Sword,Great Sword,Axe,Hammer|None|Physical Attack|After the first direct Physical hit each battle,gain +R% Physical Attack for 2 own Actions.|30-40%|
|M05|Timecut|Sword,Dagger,Bow|None|Haste|After a Physical Critical Hit,gain Haste with +R% Speed for 2 own Actions.|35-45%|
|M06|Adamant Resolve|Sword,Great Sword,Hammer,Shield|None|Fortify|After using a direct Physical Skill,gain Fortify with +R% Defense and Magical Defense for 2 own Actions.|35-45%|
|M07|Sovereign Arrow|Bow|None|Bow Accuracy|Basic Attacks gain +R% Accuracy.|30-40%|
|M08|Eclipse Arrow|Bow|Air|Blind|On a direct Air Physical hit,roll R% to apply Blind for 2 Actions.|42-55%|
|M09|Rupturing Shot|Bow|Air|Crippled|On a direct Air Physical hit,roll R% to apply Crippled for 2 Actions.|40-50%|
|M10|Sovereign Venom|Dagger|None|Poison|On a direct Physical hit,roll R% to apply Poison for 3 Actions.|42-55%|
|M11|Void Madness|Staff|Darkness|Confusion|On a direct Darkness Magic hit,roll R% to apply Confusion for 1 Action.|30-40%|
|M12|Ghoststride|Dagger|None|Evasion Up|After a Physical Critical Hit,gain Evasion Up with +R% Evasion for 2 own Actions.|35-45%|
|M13|Unending Hex|Dagger,Staff|Darkness|Curse|On a direct Darkness hit,roll R% to apply Curse for 3 Actions.|35-45%|
|M14|Archmage Focus|Staff|None|Focus|After using a direct Magic Skill,gain Focus with +R% Magic Power and Accuracy for 2 own Actions.|32-42%|
|M15|Endless Well|Staff|None|Mana Recovery|After a direct Magic hit,restore R% of Max Mana.|12-16%|
|M16|Void Fracture|Staff|None|Magic Break|On a direct Magic hit,roll R% to apply Magic Break for 2 Actions.|42-55%|
|M17|Celestial Ward|Staff|None|Magic Ward|After using a direct Magic Skill,gain Magic Ward with +R% Magical Defense for 2 own Actions.|35-45%|
|M18|Immortal Aegis|Shield|None|Barrier|At battle start,create a Barrier equal to R% of Max Health.|25-35%|
|M19|Worldbreaker Bash|Shield|Earth|Stun|On a direct Earth Physical hit,roll R% to apply Stun for 1 Action.|30-40%|
|M20|Absolute Guard|Shield|None|Damage Reduction|While a Barrier is active,gain R% Damage Reduction.|15-20%|
|M21|Phoenix Brand|All Weapons|Fire|Burn|On a direct Fire hit,roll R% to apply Burn for 3 Actions.|42-55%|
|M22|Solar Scorch|All Weapons|Fire|Scorched|On a direct Fire hit,roll R% to apply Scorched for 2 Actions.|42-55%|
|M23|Absolute Zero|All Weapons|Water|Freeze|On a direct Water hit,roll R% to apply Freeze for 1 Action.|30-40%|
|M24|Drowning Current|All Weapons|Water|Wet|On a direct Water hit,roll R% to apply Wet for 2 Actions.|45-60%|
|M25|Worldroot|All Weapons|Earth|Rooted|On a direct Earth hit,roll R% to apply Rooted for 2 Actions.|45-60%|
|M26|Seismic Rupture|All Weapons|Earth|Cracked|On a direct Earth hit,roll R% to apply Cracked for 2 Actions.|45-60%|
|M27|Tempest Collapse|All Weapons|Air|Winded|On a direct Air hit,roll R% to apply Winded for 2 Actions.|45-60%|
|M28|Eye of the Storm|Staff|Air|Silence|On a direct Air Magic hit,roll R% to apply Silence for 1 Action.|30-40%|
|M29|Abyssal Terror|All Weapons|Darkness|Fear|On a direct Darkness hit,roll R% to apply Fear for 1 Action.|35-45%|
|M30|Sovereign Shadow|All Weapons|Darkness|Shadow Mark|On a direct Darkness hit,roll R% to apply Shadow Mark for 2 Actions.|45-60%|
|M31|Seraphic Brand|All Weapons|Holy|Holy Mark|On a direct Holy hit,roll R% to apply Holy Mark for 2 Actions.|45-60%|
|M32|Final Judgment|All Weapons|Holy|Magic Vulnerability|On a direct Holy hit,roll R% to apply Magic Vulnerability for 2 Actions.|35-45%|
|M33|Blood Sovereignty|Sword,Great Sword,Axe,Hammer,Staff,Bow,Dagger|None|Lifesteal|Direct Damage dealt by this Weapon gains +R% Lifesteal.|10-14%|
|M34|Mythic Resonance|All Weapons|Weapon Primary Element|Elemental Damage|While equipped,gain +R% Damage for the Weapon's Primary Element.|22-30%|
|M35|Primal Ward|All Weapons|None|Elemental Ward|After receiving Elemental Damage,gain R% Resistance to that same Element for 2 own Actions.|35-45%|
|M36|Immortal Renewal|All Weapons|None|Regeneration|After defeating an Enemy,gain Regeneration that heals R% of Max Health at the end of your next 2 Actions.|10-14%|
|M37|War God's Oath|Sword,Great Sword,Axe,Hammer,Bow,Dagger|None|Berserk|When current Health is 40% or lower,gain Berserk with +R% Physical Attack and -10% Defense for 2 own Actions.|30-40%|

---

# Trait Examples

## Example 1: Water Staff Reaches Epic

```text
Weapon Type = Staff
Combat Style = Magic
Element Types = Water
Primary Element = Water
Existing Trait Families = None
```

The candidate list can include Staff traits,All Weapon traits,Water traits,and Weapon Primary Element traits.

It cannot include physical-only Sword,Axe,Hammer,Bow,Dagger,or Shield traits. It also cannot include Fire,Earth,Air,Darkness,or Holy traits.

```text
Possible valid Epic candidates include:
- Arcane Focus
- Mana Well
- Spell Fracture
- Runic Ward
- Frostbrand
- Tidal Mark
- Elemental Resonance
- Prismatic Ward
- Vital Renewal
- Drowsing Mist
```

If `Drowsing Mist` is selected and `R = 8`:

```text
Final Trait:
On a direct Water Magic hit,roll 8% to apply Sleep for 1 Action.
```

## Example 2: Fire Axe Reaches Legendary

```text
Weapon Type = Axe
Combat Style = Physical
Element Types = Fire
Primary Element = Fire
Existing Epic Trait Family = Bleeding
```

The candidate list excludes every Staff-only trait,every non-Fire elemental trait,and every Trait with Family `Bleeding`.

It can include physical Axe traits,Fire traits,and universal traits.

If `Infernal Brand` is selected and `R = 31`:

```text
Final Trait:
On a direct Fire hit,roll 31% to apply Burn for 3 Actions.
```

## Example 3: Mythic Shield

```text
Weapon Type = Shield
Combat Style = Physical
Element Types = Earth
Primary Element = Earth
Epic Trait = Aegis Spark with R = 10
Legendary Trait = Quaking Bash with R = 22
```

A Mythic Trait cannot have Family `Barrier` or `Stun`,because those Families already exist. It can still roll `Absolute Guard`,`Worldroot`,`Seismic Rupture`,`Primal Ward`,or another valid non-duplicate Family.


---

# Item Display Format

```text
Ember Fang Dagger +3
Grade: Mythic
Element Types: Fire

Physical Attack: 104 (+50% Grade Bonus) = 156
Critical Chance: +5.2% (+50% Grade Bonus) = +7.8%
Fire Damage: +13.0% (+50% Grade Bonus) = +19.5%

Original Passive:
- Fire Damage +10.0%

Epic Trait:
- Firebrand: On a direct Fire hit,roll 16% to apply Burn for 3 Actions.

Legendary Trait:
- Master Venom: On a direct Physical hit,roll 29% to apply Poison for 3 Actions.

Mythic Trait:
- Tyrant's Momentum: After the first direct Physical hit each battle,gain +36% Physical Attack for 2 own Actions.
```


---

# Quick Reference

```text
Blacksmith Base Stat =
Original +0 Value × (1 + Upgrade Level × 0.10)

Final Item Stat =
Blacksmith Base Stat + Grade Bonus

Epic = 1 random Epic Trait
Legendary = Epic Trait + 1 random Legendary Trait
Mythic = Epic Trait + Legendary Trait + 1 random Mythic Trait
```

```text
Trait Value R =
Minimum + Floor(Random(0,1) × (Maximum - Minimum + 1))
```

```text
Trait selection filters out:
- wrong Weapon Types
- wrong Combat Style
- wrong Element
- duplicate Trait IDs
- duplicate Trait Families
```

---

## Documentation Links

This preserved source is retained in full. The canonical integrated design is in
[08_Blacksmith_and_Enchanter.md](08_Blacksmith_and_Enchanter.md); the documentation index is [00_README.md](00_README.md).
Where this source conflicts with newer documents, see
[16_Consistency_Audit.md](16_Consistency_Audit.md) rather than deleting this record.

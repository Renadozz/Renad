# Skills System

## Overview
The skills system in this RPG game is divided into two main types:

- Active Skills (used during combat)
- Passive Skills (always active effects)

Each skill has:
- Name
- Mana Cost (MP)
- Level
- Skill EXP (progression system)

---

# Active Skills

## Concept
Active skills are abilities used during battle.  
They consume Mana (MP) and MAY have cooldowns (EXP: cant use this skill again till 2 rounds).

---

## Active Skill Properties

Each active skill includes:

- Damage (how much it deals)
- Mana Cost (MP required)
- Cooldown (turns before reuse)
- Target Type:
  - Single Enemy
  - All Enemies
  - Self

---

## Example Active Skills

### Power Strike
- Deals higher damage than normal attack
- Medium MP cost
- Short/maybe no cooldown

Purpose:
Main early-game damage skill.

---

### Heal
- Restores HP to the player
- Uses MP
- Has cooldown for balance

Purpose:
Allows survival without relying only on potions.

---

### Fireball (future skill)
- Magic-based damage
- Scales with Magic stat
- Targets one enemy

---

# Passive Skills

## Concept
Passive skills are always active and do not need to be triggered.

---

## Passive Skill Properties

- Always active
- No MP cost
- No cooldown
- Directly affects player stats

---

## Example Passive Skills

### Defender
- Permanently increases Defense by +5

---

### Speed Boost
- Increases Speed
- Helps player act earlier in combat

---

### Mana Efficiency
- Reduces MP cost of skills

---

# Player Skill System

## Concept
The player has a list of skills.

- Starts with basic skills
- Unlocks new skills through progression
- Some skills unlock at specific levels

---

## Starting Skills

At the beginning of the game:
- Power Strike
- Heal
- Defender

---

## Later Skills

As the game progresses:
- Fireball
- Shield Block (Incoming damage is reduced/partially ignored Effect lasts for a limited number of turns)
- Buff Skills

---

# Skill Progression System

## Concept
Each skill levels up individually through use.

### How it works:
- Using a skill gives Skill EXP
- When EXP reaches a threshold → skill levels up

---

## Example

Power Strike:
- Level 1: Normal damage
- Level 2: Increased damage
- Level 3: Higher damage + reduced MP cost

---

# Combat Integration

## Player Turn Flow:

1. Player selects a skill
2. System checks MP cost
3. If enough MP → skill is used
4. Effect is applied (damage/heal/etc.)
5. If Active Skill → cooldown starts

---

## Battle Loop:

- Player uses Skill / Attack / Item
- Enemy takes action
- Repeat until one side is defeated

---

# Skill Range System

To keep it simple, only 3 target types are used:

- Single Target → one enemy
- Self → player only
- All Enemies → affects all enemies

---

# MVP Skills (Start Small)

Start with only:

## Active Skills:
- Power Strike
- Heal

## Passive Skills:
- Defender

---

# Future Expansion Ideas

Later i will add:
- Buff / Debuff system
- Area of Effect (AoE) skills
- Status Effects (Poison, Stun, Burn) *not really sure about this one tho*
- Skill Trees
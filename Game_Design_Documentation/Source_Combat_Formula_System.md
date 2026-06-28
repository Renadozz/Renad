# Combat Formula System

## System Overview

This combat system uses a Continuous Action Gauge System.

There are no fixed shared rounds.

Every living combatant has an Action Gauge that fills based on Effective Speed. A combatant acts whenever its Action Gauge reaches `100`.

A fast combatant can act multiple times before a slower combatant acts once.

| System                 | Rule                                                                                            |
| ---------------------- | ----------------------------------------------------------------------------------------------- |
| Action Gauge Threshold | A combatant acts when its Action Gauge reaches `100`.                                           |
| Combat Time            | Combat uses internal continuous time. This value does not need to be shown to the Player.       |
| Speed                  | Determines how quickly a combatant fills its Action Gauge.                                      |
| Extra Actions          | A combatant with sufficiently high Speed can act multiple times before a slower combatant acts. |
| No Global Round        | There is no shared round where every unit acts exactly once.                                    |
| Effect Duration        | Buffs,Debuffs,and Status Effects use the affected unit's own Actions.                           |
| Cooldowns              | Cooldowns decrease at the start of the skill owner's own Action.                                |
| Potions                | Potion limits use Player Actions instead of rounds.                                             |
| Summons                | A summoned enemy starts with `0` Action Gauge and cannot act immediately.                       |
| Physical Crits         | Only direct Physical Damage Skills can Crit.                                                    |
| Magic Crits            | Magic Damage Skills cannot Crit.                                                                |
| Damage-Over-Time Crits | Burn,Poison,Bleeding,and Curse Damage cannot Crit.                                              |

---

# Numeric Rules

| Rule                    | Implementation                                                                                                                               |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Internal Percentages    | Store percentages internally as decimals. Example: `25% = 0.25`.                                                                             |
| Displayed Percentages   | Show percentages to the Player as whole values. Example: `0.25` is shown as `25%`.                                                           |
| Rounding                | Round final Damage,Healing,Barrier,and Current Stat values down with `Floor()`.                                                              |
| Minimum Damage          | A successful damaging hit always deals at least `1` Damage after all reductions.                                                             |
| Random Damage           | Do not use random Damage variance. Damage should remain predictable.                                                                         |
| Current Stats           | All combat formulas use Current Attributes after Equipment,Passives,Buffs,and Debuffs are applied.                                           |
| Action Gauge Threshold  | Use `100` as the default Action Gauge Threshold.                                                                                             |
| Minimum Effective Speed | Effective Speed can never be lower than `1`.                                                                                                 |
| Neutral Element         | Neutral Damage has no Elemental Matchup,does not use Elemental Damage Bonus,and ignores Elemental Resistance.                                |
| Primary Element         | A skill with `Primary` Element uses the first Element Type listed on the attacker.                                                           |
| Maximum Element Types   | A unit should normally have one or two Element Types. More than two is not recommended because it makes Matchup calculations harder to read. |

---

# Helper Functions

## Clamp

```text
Clamp(Value,Minimum,Maximum)
```

`Clamp` keeps a value inside a defined range.

* If `Value` is lower than `Minimum`,return `Minimum`.
* If `Value` is higher than `Maximum`,return `Maximum`.
* Otherwise,return `Value`.

```text
Clamp(120,0,100) = 100
Clamp(-10,0,100) = 0
Clamp(45,0,100) = 45
```

Use `Clamp` for values that must not become too high or too low.

| Usage                | Example                                      |
| -------------------- | -------------------------------------------- |
| Hit Chance           | `Clamp(Raw Hit Chance,10%,95%)`              |
| Status Chance        | `Clamp(Base Chance - Resistance,0%,100%)`    |
| Elemental Resistance | `Clamp(All Resistance Sources,-75%,75%)`     |
| Damage Reduction     | `Clamp(All Damage Reduction Sources,0%,75%)` |
| Critical Chance      | `Clamp(Current Critical Chance,0%,75%)`      |

---

## Floor

```text
Floor(Value)
```

`Floor` rounds a decimal number down to the next whole number.

```text
Floor(18.9) = 18
Floor(18.0) = 18
Floor(0.99) = 0
```

Use `Floor` only at the final step of a calculation.

```text
Correct:
Final Damage = Floor(53.79 × 1.20)

Avoid:
Floor(53.79) × Floor(1.20)
```

The second version creates unnecessary rounding errors.

---

## Min

```text
Min(ValueA,ValueB)
```

`Min` returns the lower of two values.

```text
Min(120,85) = 85
Min(40,75) = 40
```

Use `Min` when a value cannot exceed another value.

```text
Barrier Absorbed Damage =
Min(Current Barrier,Final Damage)
```

A Barrier with `80` value cannot absorb more than `80` Damage.

---

## Max

```text
Max(ValueA,ValueB)
```

`Max` returns the higher of two values.

```text
Max(0,-15) = 0
Max(30,12) = 30
```

Use `Max` when a value may not fall below a limit.

```text
Effective Defense =
Max(0,Target Defense × (1 - Penetration))
```

This prevents Defense from becoming negative.

---

## Sum

```text
Sum(Value List)
```

`Sum` adds every value in a list.

```text
Sum(10%,15%,-5%) = 20%
Sum(0.10,0.15,-0.05) = 0.20
```

Use `Sum` when multiple modifiers stack.

```text
Total Status Resistance =
Sum(
Base Status Resistance,
Equipment Status Resistance,
Buff Status Resistance,
Specific Status Resistance
)
```

---

## Average

```text
Average(Value List)
```

`Average` adds every value in a list and divides the result by the number of values.

```text
Average(25%,-20%) = 2.5%
Average(0%,25%) = 12.5%
Average(25%,0%,0%) = 8.33%
```

Use `Average` for Elemental Matchup Modifiers against multi-element targets.

```text
Average Matchup Modifier =
Average(
Matchup Modifier against Target Element 1,
Matchup Modifier against Target Element 2
)
```

If the target has no Element Types,the result is `0%`.

```text
Average(Empty List) = 0%
```

---

## Random

```text
Random(Minimum,Maximum)
```

`Random` returns a random decimal number from `Minimum` up to,but not including,`Maximum`.

```text
Random(0,1)
```

returns a value such as:

```text
0.000
0.184
0.572
0.999
```

Use this for chance rolls.

```text
Chance succeeds when:

Random(0,1) < Final Chance
```

Example:

```text
Final Status Chance = 45% = 0.45
Random Roll = 0.31

0.31 < 0.45

Status is applied.
```

---

## RollChance

```text
RollChance(Chance)
```

`RollChance` is a readable helper based on `Random`.

```text
RollChance(Chance) =
Random(0,1) < Chance
```

Example:

```text
RollChance(0.65)
```

has a `65%` chance to return `True`.

```text
RollChance(0.00) = always False
RollChance(1.00) = always True
```

---

# Current Attribute Calculation

## Current Stat Formula

Physical Attack,Magic Power,Defense,Magical Defense,and Speed use relative percentage modifiers.

```text
Current Stat =
Floor(
Base Stat × (1 + Total Stat Modifier)
)
```

For all attributes except Speed:

```text
Current Stat =
Max(
0,
Floor(
Base Stat × (1 + Total Stat Modifier)
)
)
```

For Speed:

```text
Effective Speed =
Max(
1,
Floor(
Base Speed × (1 + Total Speed Modifier)
)
)
```

## Stat Modifier Example

```text
Base Defense = 40

Fortify = +25% Defense
Armor Break = -25% Defense

Total Defense Modifier =
25% - 25% =
0%

Current Defense =
Floor(40 × (1 + 0))

Current Defense = 40
```

## Stat Modifier Stacking Rules

| Attribute Type             | Stacking Rule                                                                                        | Recommended Cap                      |
| -------------------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------ |
| Physical Attack            | Add all positive and negative relative modifiers before applying them to Base Physical Attack.       | Minimum `-75%`,Maximum `+100%`       |
| Magic Power                | Add all positive and negative relative modifiers before applying them to Base Magic Power.           | Minimum `-75%`,Maximum `+100%`       |
| Defense                    | Add all positive and negative relative modifiers before applying them to Base Defense.               | Minimum `-75%`,Maximum `+100%`       |
| Magical Defense            | Add all positive and negative relative modifiers before applying them to Base Magical Defense.       | Minimum `-75%`,Maximum `+100%`       |
| Speed                      | Add all positive and negative relative modifiers before applying them to Base Speed.                 | Minimum `-75%`,Maximum `+100%`       |
| Accuracy                   | Add Accuracy modifiers as percentage points.                                                         | No cap before Hit Chance calculation |
| Evasion                    | Add Evasion modifiers as percentage points.                                                          | Maximum `85%`                        |
| Critical Chance            | Add Critical Chance modifiers as percentage points.                                                  | Maximum `75%`                        |
| Status Resistance          | Add all sources as percentage points.                                                                | Minimum `-50%`,Maximum `80%`         |
| Specific Status Resistance | Add all matching sources as percentage points.                                                       | Minimum `-50%`,Maximum `100%`        |
| Elemental Resistance       | Add all matching Elemental Resistance sources as percentage points.                                  | Minimum `-75%`,Maximum `75%`         |
| Damage Reduction           | Add all Damage Reduction sources as percentage points.                                               | Minimum `0%`,Maximum `75%`           |
| Physical Penetration       | Add all Physical Penetration sources as percentage points before Skill-specific Defense Ignore.      | Minimum `0%`,Maximum `75%`           |
| Magic Penetration          | Add all Magic Penetration sources as percentage points before Skill-specific Magical Defense Ignore. | Minimum `0%`,Maximum `75%`           |

> `+25% Defense` means a relative modifier.
> `+15% Accuracy` means `+15 percentage points`.
> `+20% Fire Resistance` means `20 percentage points` of Fire Resistance.

## Speed Modifier Example

```text
Base Speed = 20

Haste = +25% Speed
Slow = -25% Speed

Total Speed Modifier =
25% - 25% =
0%

Effective Speed =
Floor(20 × (1 + 0))

Effective Speed = 20
```

---

# Unified Resistance Rules

## Resistance Principle

All Resistance values use one simple additive rule.

First,add all sources of the relevant Resistance together.

Then,apply the final Resistance directly.

```text
Total Resistance =
Clamp(
Base Resistance
+
Equipment Resistance
+
Passive Resistance
+
Buff Resistance
+
Debuff Resistance,
Resistance Minimum,
Resistance Maximum
)
```

Resistance sources do not multiply each other.

```text
Correct:

20% Fire Resistance
+ 15% Fire Resistance
- 10% Fire Resistance

Total Fire Resistance =
25%
```

```text
Avoid:

20% × 15% × -10%
```

---

## Damage Resistance Rule

Elemental Resistance and Damage Reduction reduce Damage directly.

```text
Damage After Resistance =
Damage Before Resistance
×
(1 - Total Resistance)
```

Example:

```text
Damage Before Fire Resistance = 100
Total Fire Resistance = 20%

Damage After Fire Resistance =
100 × (1 - 0.20)

Damage After Fire Resistance = 80
```

A `20%` Resistance always reduces matching Damage by `20%`.

---

## Status Resistance Rule

Status Resistance reduces Status Chance directly.

```text
Final Status Chance =
Clamp(
Base Status Chance
-
Total Status Resistance,
0%,
100%
)
```

Example:

```text
Root Snare Base Chance = 65%
Target Total Rooted Resistance = 20%

Final Rooted Chance =
65% - 20%

Final Rooted Chance = 45%
```

A `20%` Status Resistance always removes `20 percentage points` from the Status Chance.

---

## Negative Resistance Rule

Negative Resistance increases incoming Damage or Status Chance.

```text
Fire Resistance = -25%

Fire Damage Multiplier =
1 - (-0.25)

Fire Damage Multiplier = 1.25
```

The target receives `25%` more Fire Damage.

```text
Burn Base Chance = 50%
Burn Resistance = -20%

Final Burn Chance =
50% - (-20%)

Final Burn Chance = 70%
```

The target has a `70%` chance to receive Burn.

---

## Resistance Types

| Resistance Type            | What It Affects                                                              | Formula                                      |
| -------------------------- | ---------------------------------------------------------------------------- | -------------------------------------------- |
| Fire Resistance            | Incoming Fire Damage                                                         | `Damage × (1 - Fire Resistance)`             |
| Water Resistance           | Incoming Water Damage                                                        | `Damage × (1 - Water Resistance)`            |
| Earth Resistance           | Incoming Earth Damage                                                        | `Damage × (1 - Earth Resistance)`            |
| Air Resistance             | Incoming Air Damage                                                          | `Damage × (1 - Air Resistance)`              |
| Darkness Resistance        | Incoming Darkness Damage                                                     | `Damage × (1 - Darkness Resistance)`         |
| Holy Resistance            | Incoming Holy Damage                                                         | `Damage × (1 - Holy Resistance)`             |
| Damage Reduction           | All incoming Damage after Defense,Magical Defense,and Elemental calculations | `Damage × (1 - Damage Reduction)`            |
| Global Status Resistance   | All negative Status Effects                                                  | `Status Chance - Global Status Resistance`   |
| Specific Status Resistance | One specific Status Effect                                                   | `Status Chance - Specific Status Resistance` |

> Defense and Magical Defense are not percentage Resistances. They use the Defense Mitigation Formula.

---

# Continuous Action Gauge System

## Core Rule

Every living combatant has an Action Gauge.

The Action Gauge fills continuously based on Effective Speed.

A combatant acts when its Action Gauge reaches `100`.

After completing an Action,subtract `100` from that combatant's Action Gauge.

```text
Action Gauge Threshold = 100
```

```text
After Action:

New Action Gauge =
Current Action Gauge - 100
```

> Do not reset Action Gauge to `0`.
> Always subtract `100` so any possible overflow remains.

## Time Until Next Action

```text
Time Until Next Action =
(Action Gauge Threshold - Current Action Gauge)
/
Effective Speed
```

The living combatant with the lowest Time Until Next Action acts next.

If one or more combatants already have at least `100` Action Gauge,do not advance Combat Time. Resolve one of those combatants immediately using the Tie Break Rules.

## Action Gauge Resolution

```text
1. Calculate Effective Speed for every living combatant.
2. Check whether any living combatant has at least 100 Action Gauge.
3. If one or more combatants have at least 100 Action Gauge:
   - Resolve one of them immediately using the Tie Break Rules.
   - Do not advance Combat Time.
4. If no combatant has 100 Action Gauge:
   - Calculate Time Until Next Action for every living combatant.
   - Find the lowest Time Until Next Action.
   - Advance Combat Time by that amount.
   - Increase every living combatant's Action Gauge:
     Action Gauge += Effective Speed × Advanced Combat Time
5. Resolve the selected combatant's Action.
6. After the Action ends:
   Action Gauge -= 100
7. Repeat from step 1.
```

## Starting a Battle

```text
Combat Time = 0

Player Action Gauge = 0
Enemy 1 Action Gauge = 0
Enemy 2 Action Gauge = 0
Enemy 3 Action Gauge = 0
```

All living combatants begin with `0` Action Gauge unless a specific Passive,Skill,or encounter rule changes this.

## Example: Player Speed 20,Enemy 1 Speed 15,Enemy 2 Speed 9

```text
Player Effective Speed = 20
Enemy 1 Effective Speed = 15
Enemy 2 Effective Speed = 9
```

### First Action

```text
Player Time Until Next Action =
(100 - 0) / 20 =
5.000

Enemy 1 Time Until Next Action =
(100 - 0) / 15 =
6.667

Enemy 2 Time Until Next Action =
(100 - 0) / 9 =
11.111
```

The Player acts first.

| Combatant | Action Gauge Before Player Action | Action Gauge After Player Action |
| --------- | --------------------------------: | -------------------------------: |
| Player    |                           100.000 |                            0.000 |
| Enemy 1   |                            75.000 |                           75.000 |
| Enemy 2   |                            45.000 |                           45.000 |

```text
Combat Time = 5.000
```

### Second Action

```text
Player Time Until Next Action =
(100 - 0) / 20 =
5.000

Enemy 1 Time Until Next Action =
(100 - 75) / 15 =
1.667

Enemy 2 Time Until Next Action =
(100 - 45) / 9 =
6.111
```

Enemy 1 acts next.

| Combatant | Action Gauge Before Enemy 1 Action | Action Gauge After Enemy 1 Action |
| --------- | ---------------------------------: | --------------------------------: |
| Player    |                             33.333 |                            33.333 |
| Enemy 1   |                            100.000 |                             0.000 |
| Enemy 2   |                             60.000 |                            60.000 |

```text
Combat Time = 6.667
```

### Third Action

```text
Player Time Until Next Action =
(100 - 33.333) / 20 =
3.333

Enemy 1 Time Until Next Action =
(100 - 0) / 15 =
6.667

Enemy 2 Time Until Next Action =
(100 - 60) / 9 =
4.444
```

The Player acts next.

| Combatant | Action Gauge Before Player Action | Action Gauge After Player Action |
| --------- | --------------------------------: | -------------------------------: |
| Player    |                           100.000 |                            0.000 |
| Enemy 1   |                            50.000 |                           50.000 |
| Enemy 2   |                            90.000 |                           90.000 |

```text
Combat Time = 10.000
```

### Fourth Action

```text
Player Time Until Next Action =
(100 - 0) / 20 =
5.000

Enemy 1 Time Until Next Action =
(100 - 50) / 15 =
3.333

Enemy 2 Time Until Next Action =
(100 - 90) / 9 =
1.111
```

Enemy 2 acts next.

| Combatant | Action Gauge Before Enemy 2 Action | Action Gauge After Enemy 2 Action |
| --------- | ---------------------------------: | --------------------------------: |
| Player    |                             22.222 |                            22.222 |
| Enemy 1   |                             66.667 |                            66.667 |
| Enemy 2   |                            100.000 |                             0.000 |

```text
Combat Time = 11.111
```

## Resulting Action Order

```text
1. Player
2. Enemy 1
3. Player
4. Enemy 2
```

This matches the intended Speed behaviour.

> Higher Speed does not only decide who acts first.
> Higher Speed determines how often a unit acts over the full battle.

## Long-Term Speed Ratio

```text
Player Speed = 20
Enemy 1 Speed = 15
Enemy 2 Speed = 9
```

Over a long battle:

```text
For every 20 Player Actions:
Enemy 1 receives approximately 15 Actions.
Enemy 2 receives approximately 9 Actions.
```

## Speed Change During Combat

Speed changes affect future Action Gauge filling immediately after the Buff or Debuff is applied.

They do not retroactively add Action Gauge.

```text
Current Action Gauge = 40
Current Speed = 20

Haste changes Speed to 25
```

```text
Time Until Next Action before Haste =
(100 - 40) / 20 =
3.000
```

```text
Time Until Next Action after Haste =
(100 - 40) / 25 =
2.400
```

The unit keeps its current `40` Action Gauge but fills the remaining Gauge faster.

## Action Gauge Tie Break Rules

| Situation                                                | Rule                                                                                   |
| -------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Two units reach 100 Action Gauge at the same Combat Time | The unit with higher Effective Speed acts first.                                       |
| Same Action Gauge and same Effective Speed               | The Player acts first.                                                                 |
| Two identical enemies tie                                | Use their fixed spawn order.                                                           |
| A unit is defeated before acting                         | Remove it from Action Gauge calculations immediately.                                  |
| A unit is summoned                                       | Start with `0` Action Gauge and cannot act immediately.                                |
| A unit is Stunned,Frozen,or Asleep                       | It reaches 100 Action Gauge,loses its Action,and then has 100 Action Gauge subtracted. |
| Action Gauge Overflow                                    | Subtract only `100` after an Action. Keep all remaining Gauge.                         |
| No Living Enemy                                          | Combat ends immediately.                                                               |
| Player Defeated                                          | Combat ends immediately.                                                               |

---

# Action Lifecycle

## Start of Action

```text
1. A combatant reaches 100 Action Gauge.
2. Reduce the combatant's Skill Cooldowns by 1.
3. Check action-denial effects:
   Stun,Freeze,Sleep,and any future action-denial effect.
4. If an action-denial effect prevents the Action:
   - The combatant loses this Action.
   - Do not select a Skill,Attack,or Potion.
   - Remove the action-denial effect.
   - Continue to End of Action.
5. If the combatant can act:
   - The Player may use Potions.
   - The Player selects one valid Skill,Attack,or Item action.
   - An Enemy selects one valid Skill through AI Priority.
6. Resolve the selected Action.
```

## End of Action

```text
1. Apply end-of-action Damage-Over-Time:
   Burn,Poison,Curse,and similar effects.
2. Apply end-of-action Healing:
   Regeneration and similar effects.
3. Reduce durations of active Buffs,Debuffs,and Status Effects by 1.
4. Do not reduce effects applied during this same Action.
5. Remove effects whose Duration reaches 0.
6. Subtract 100 from the acting combatant's Action Gauge.
7. Continue to the next Action Gauge event.
```

## Effect Duration Tracking Rule

Every effect should store these values:

| Stored Value             | Description                                               |
| ------------------------ | --------------------------------------------------------- |
| Effect Name              | Name of the Buff,Debuff,or Status Effect.                 |
| Remaining Actions        | How many completed Actions of the affected target remain. |
| Applied To               | The affected combatant.                                   |
| Applied During Action ID | The Action ID in which the effect was applied.            |
| Source Combatant         | The unit that created the effect.                         |
| Stored Source Attribute  | Used only by Damage-Over-Time effects.                    |

When reducing Effect Duration:

```text
Reduce Duration only when:

Effect Applied During Action ID
is lower than
Current Action ID of the affected combatant.
```

This prevents an effect from losing Duration immediately after it is applied.

## Important Duration Rule

```text
Example:

Player uses Haste on self.
Haste Duration = 2 Actions.

The Player does not immediately lose 1 Duration.
Haste remains active for the Player's next 2 completed Actions.
```

## Duration Example

```text
Enemy applies Slow to the Player.
Slow Duration = 2 Actions.

Player's next Action:
Slow is active.
Player completes the Action.
Slow Duration becomes 1.

Player's following Action:
Slow is active.
Player completes the Action.
Slow Duration becomes 0.
Slow is removed.
```

## Action-Denial Example

```text
Enemy applies Stun to the Player.
Stun Duration = 1 Action.

The Player reaches 100 Action Gauge.
The Player loses this Action.
Stun is removed.
The Player starts filling the Action Gauge again.
```

---

# Potion Rules

## Potion Uses Per Action

```text
Potion Uses Per Action = 1
```

| Rule              | Implementation                                                                                                        |
| ----------------- | --------------------------------------------------------------------------------------------------------------------- |
| Default Limit     | The Player can use `1` Potion during each Player Action.                                                              |
| Potion Timing     | The Player can use Potions only during the Player's own Action.                                                       |
| Potion and Skill  | The Player may use the allowed Potions and then select one Skill,Attack,or Item action.                               |
| No Global Round   | Potion usage is not limited by shared rounds because shared rounds do not exist.                                      |
| Speed Interaction | A fast Player can receive multiple Actions before a slow enemy acts and may use Potions during each of those Actions. |
| Passive Bonus     | A Passive Skill,Accessory,or rare effect may grant `Potion Uses Per Action +1`.                                       |
| Enemy Rule        | Enemies do not use Potions. Enemy healing and buffs are controlled by Skills and AI Priority.                         |
| Smoke Bomb        | Uses its own battle rule and does not count as a Potion.                                                              |
| Recall Potion     | Cannot be used in battle unless a special effect explicitly allows it.                                                |

## Potion Example

```text
Player Potion Uses Per Action = 1

Player Speed = 20
Enemy Speed = 9

The Player receives two Actions before the Enemy's next Action.

The Player may use:
- 1 Potion during the first Player Action
- 1 Potion during the second Player Action
```

---

# Cooldown Rules

## Cooldown Formula

```text
At the start of the skill owner's Action:

New Cooldown =
Max(
0,
Current Cooldown - 1
)
```

## Using a Skill

```text
When a Skill is used:

Current Cooldown =
Skill Cooldown Value
```

A Skill is usable only when:

```text
Current Cooldown = 0
```

## Cooldown Example

```text
Earthquake Cooldown = 3

Action 1:
Enemy uses Earthquake.
Earthquake Current Cooldown becomes 3.

Action 2:
Start of Enemy Action:
Earthquake Cooldown becomes 2.
Earthquake cannot be used.

Action 3:
Start of Enemy Action:
Earthquake Cooldown becomes 1.
Earthquake cannot be used.

Action 4:
Start of Enemy Action:
Earthquake Cooldown becomes 0.
Earthquake can be used again.
```

> Cooldowns decrease only when the owner receives an Action.
> A fast unit recovers Skill Cooldowns faster because it acts more often.

## Cooldown and Action Denial

| Situation     | Rule                                                                          |
| ------------- | ----------------------------------------------------------------------------- |
| Stunned Unit  | Cooldowns still decrease at the start of its lost Action.                     |
| Frozen Unit   | Cooldowns still decrease at the start of its lost Action.                     |
| Sleeping Unit | Cooldowns still decrease at the start of its lost Action.                     |
| Defeated Unit | Cooldowns no longer decrease.                                                 |
| Summoned Unit | Starts with all Skill Cooldowns at `0` unless the summon rule says otherwise. |

---

# Hit Chance Formula

## Accuracy and Evasion Rule

Accuracy is an Accuracy Bonus.

Evasion is an Evasion Bonus.

Neither value is the default physical hit chance.

A unit with:

```text
Accuracy = 0%
Evasion = 0%
```

has the normal Physical Hit Chance cap of `95%`.

## Physical Hit Chance

```text
Raw Physical Hit Chance =
100%
-
Max(
0%,
Target Current Evasion
-
Attacker Current Accuracy
)
```

```text
Final Physical Hit Chance =
Clamp(
Raw Physical Hit Chance,
10%,
95%
)
```

## Physical Hit Example: Accuracy Does Not Exceed 100%

```text
Attacker Accuracy = 20%
Target Evasion = 10%
```

```text
Raw Physical Hit Chance =
100% - Max(0%,10% - 20%)

Raw Physical Hit Chance =
100% - 0%

Raw Physical Hit Chance = 100%
```

```text
Final Physical Hit Chance =
Clamp(100%,10%,95%)

Final Physical Hit Chance = 95%
```

The extra Accuracy cancels all Evasion,but cannot create more than the normal `95%` maximum Hit Chance.

## Physical Hit Example: Evasion Is Higher

```text
Attacker Accuracy = 15%
Target Evasion = 30%
```

```text
Raw Physical Hit Chance =
100% - Max(0%,30% - 15%)

Raw Physical Hit Chance =
100% - 15%

Raw Physical Hit Chance = 85%
```

```text
Final Physical Hit Chance =
Clamp(85%,10%,95%)

Final Physical Hit Chance = 85%
```

## Hit Chance Example: High Evasion

```text
Attacker Accuracy = 0%
Target Evasion = 95%
```

```text
Raw Physical Hit Chance =
100% - Max(0%,95% - 0%)

Raw Physical Hit Chance = 5%
```

```text
Final Physical Hit Chance =
Clamp(5%,10%,95%)

Final Physical Hit Chance = 10%
```

The `10%` minimum prevents a normal Physical Attack from becoming impossible.

## Hit Rules

| Attack Type                       | Hit Rule                                                            |
| --------------------------------- | ------------------------------------------------------------------- |
| Physical Damage Skill             | Uses Accuracy against Evasion.                                      |
| Physical Damage Skill with Status | Must hit before its Status Chance is checked.                       |
| Physical No-Damage Debuff         | Uses Accuracy against Evasion before Status Chance is checked.      |
| Magic Damage Skill                | Always hits.                                                        |
| Magic Damage Skill with Status    | Damage always hits,then Status Chance is checked.                   |
| Magic No-Damage Debuff            | Does not use Accuracy or Evasion. It only checks Status Resistance. |
| Cannot Miss Effect                | Final Hit Chance becomes `100%`.                                    |
| Guaranteed Dodge Effect           | Final Hit Chance becomes `0%` unless the attack Cannot Miss.        |
| Minimum Hit Chance                | A normal Physical Attack can never have less than `10%` Hit Chance. |
| Maximum Hit Chance                | A normal Physical Attack can never have more than `95%` Hit Chance. |
| Default Accuracy                  | Player and Enemy base Accuracy should normally start at `0%`.       |
| Default Evasion                   | Player and Enemy base Evasion should normally start at `0%`.        |

---

# Critical Hit Formula

## Critical Chance

```text
Final Critical Chance =
Clamp(
Current Critical Chance,
0%,
75%
)
```

```text
Physical Critical Hit succeeds when:

RollChance(Final Critical Chance) = True
```

## Critical Damage

```text
Critical Multiplier =
Current Critical Damage / 100
```

```text
Default Critical Damage = 150%
Default Critical Multiplier = 1.50
```

## Critical Rules

| Rule                       | Implementation                                                                                 |
| -------------------------- | ---------------------------------------------------------------------------------------------- |
| Physical Damage Skills     | Can Crit unless the individual Skill says otherwise.                                           |
| Magic Damage Skills        | Cannot Crit. Magic Damage always uses a Critical Multiplier of `1.00`.                         |
| Physical No-Damage Debuffs | Cannot Crit.                                                                                   |
| Magic No-Damage Debuffs    | Cannot Crit.                                                                                   |
| Damage-Over-Time           | Burn,Poison,Bleeding,and Curse Damage cannot Crit.                                             |
| Healing                    | Heal,Regeneration,Lifesteal,and Potions cannot Crit.                                           |
| Barrier                    | Barrier creation cannot Crit.                                                                  |
| Status Chance              | Critical Hits do not increase Status Chance unless a future Physical Skill explicitly says so. |

---

# Damage Formula

## Skill Coefficients

| Skill Value      | Coefficient |
| ---------------- | ----------: |
| `P75` or `M75`   |      `0.75` |
| `P80` or `M80`   |      `0.80` |
| `P85` or `M85`   |      `0.85` |
| `P90` or `M90`   |      `0.90` |
| `P95` or `M95`   |      `0.95` |
| `P100` or `M100` |      `1.00` |
| `P105` or `M105` |      `1.05` |
| `P115` or `M115` |      `1.15` |
| `P120` or `M120` |      `1.20` |
| `P125` or `M125` |      `1.25` |
| `P130` or `M130` |      `1.30` |
| `P135` or `M135` |      `1.35` |
| `P140` or `M140` |      `1.40` |
| `P145` or `M145` |      `1.45` |
| `P155` or `M155` |      `1.55` |

> `P` means Physical Damage.
> `M` means Magic Damage.

---

# Physical Damage Formula

## Raw Physical Damage

```text
Raw Physical Damage =
Attacker Current Physical Attack
×
Skill Coefficient
```

## Effective Physical Penetration

```text
Effective Physical Penetration =
1 - (
(1 - Attacker Physical Penetration)
×
(1 - Skill Defense Ignore)
)
```

## Effective Defense

```text
Effective Defense =
Max(
0,
Target Current Defense
×
(1 - Effective Physical Penetration)
)
```

## Physical Mitigation Multiplier

```text
Physical Mitigation Multiplier =
100
/
(100 + Effective Defense)
```

The Physical Mitigation Multiplier is the percentage of Raw Physical Damage that remains after Defense.

| Effective Defense | Physical Mitigation Multiplier | Damage Taken from 100 Raw Damage | Defense Reduction |
| ----------------: | -----------------------------: | -------------------------------: | ----------------: |
|                 0 |                         1.0000 |                              100 |                0% |
|                25 |                         0.8000 |                               80 |               20% |
|                50 |                         0.6667 |                               66 |             33.3% |
|                75 |                         0.5714 |                               57 |             42.9% |
|               100 |                         0.5000 |                               50 |               50% |
|               150 |                         0.4000 |                               40 |               60% |
|               200 |                         0.3333 |                               33 |             66.7% |
|               300 |                         0.2500 |                               25 |               75% |

## Physical Damage Before Final Modifiers

```text
Physical Damage Before Final Modifiers =
Raw Physical Damage
×
Physical Mitigation Multiplier
```

## Physical Damage Example

```text
Attacker Current Physical Attack = 60
Skill = Heavy Attack = P130
Attacker Physical Penetration = 10%
Skill Defense Ignore = 0%

Target Current Defense = 50
```

```text
Raw Physical Damage =
60 × 1.30 =
78
```

```text
Effective Physical Penetration =
1 - ((1 - 0.10) × (1 - 0.00))

Effective Physical Penetration =
10%
```

```text
Effective Defense =
50 × (1 - 0.10) =
45
```

```text
Physical Mitigation Multiplier =
100 / (100 + 45)

Physical Mitigation Multiplier =
0.6897
```

```text
Physical Damage Before Final Modifiers =
78 × 0.6897

Physical Damage Before Final Modifiers =
53.79
```

---

# Magic Damage Formula

## Raw Magic Damage

```text
Raw Magic Damage =
Attacker Current Magic Power
×
Skill Coefficient
```

## Effective Magic Penetration

```text
Effective Magic Penetration =
1 - (
(1 - Attacker Magic Penetration)
×
(1 - Skill Magical Defense Ignore)
)
```

## Effective Magical Defense

```text
Effective Magical Defense =
Max(
0,
Target Current Magical Defense
×
(1 - Effective Magic Penetration)
)
```

## Magic Mitigation Multiplier

```text
Magic Mitigation Multiplier =
100
/
(100 + Effective Magical Defense)
```

The Magic Mitigation Multiplier is the percentage of Raw Magic Damage that remains after Magical Defense.

| Effective Magical Defense | Magic Mitigation Multiplier | Damage Taken from 100 Raw Damage | Magical Defense Reduction |
| ------------------------: | --------------------------: | -------------------------------: | ------------------------: |
|                         0 |                      1.0000 |                              100 |                        0% |
|                        25 |                      0.8000 |                               80 |                       20% |
|                        50 |                      0.6667 |                               66 |                     33.3% |
|                        75 |                      0.5714 |                               57 |                     42.9% |
|                       100 |                      0.5000 |                               50 |                       50% |
|                       150 |                      0.4000 |                               40 |                       60% |
|                       200 |                      0.3333 |                               33 |                     66.7% |
|                       300 |                      0.2500 |                               25 |                       75% |

## Magic Damage Before Final Modifiers

```text
Magic Damage Before Final Modifiers =
Raw Magic Damage
×
Magic Mitigation Multiplier
```

## Magic Damage Example

```text
Attacker Current Magic Power = 70
Skill = Fire Bolt = M100
Attacker Magic Penetration = 15%
Skill Magical Defense Ignore = 0%

Target Current Magical Defense = 40
```

```text
Raw Magic Damage =
70 × 1.00 =
70
```

```text
Effective Magical Defense =
40 × (1 - 0.15)

Effective Magical Defense =
34
```

```text
Magic Mitigation Multiplier =
100 / (100 + 34)

Magic Mitigation Multiplier =
0.7463
```

```text
Magic Damage Before Final Modifiers =
70 × 0.7463

Magic Damage Before Final Modifiers =
52.24
```

> Magic Damage cannot Crit.
> The Magic Critical Multiplier is always `1.00`.

---

# Penetration Example

```text
Attacker Physical Penetration = 10%
Piercing Attack Defense Ignore = 25%
```

```text
Effective Physical Penetration =
1 - ((1 - 0.10) × (1 - 0.25))
```

```text
Effective Physical Penetration =
1 - (0.90 × 0.75)

Effective Physical Penetration =
32.5%
```

> Multiplicative Penetration prevents multiple sources from becoming too strong too quickly.

---

# Elemental Damage Formula

## Element Types

A unit can have one or two Element Types.

Examples:

```text
Forest Rat = Earth
Frost Titan = Water,Earth
Ancient Dragon = Fire,Air
Shadow Lord = Darkness
Oracle of Dawn = Holy
```

The order matters only for Skills with the `Primary` Element tag.

```text
Frost Titan Element Types = Water,Earth

Primary Element = Water
Secondary Element = Earth
```

```text
A Physical Skill with Element = Primary

uses Water when Frost Titan casts it.
```

A Skill with an explicit Element ignores the attacker's Primary Element.

```text
Dragonfire Breath Element = Fire
Storm Wing Element = Air
Eclipse Element = Darkness
```

Even if the attacker has multiple Elements,the Skill always uses only one attacking Element per hit.

## Elemental Matchup Table

| Attacking Element | Strong Against | Weak Against |
| ----------------- | -------------- | ------------ |
| Fire              | Earth          | Water        |
| Water             | Fire           | Air          |
| Earth             | Air            | Fire         |
| Air               | Water          | Earth        |
| Holy              | Darkness       | None         |
| Darkness          | Holy           | None         |

## Individual Matchup Modifiers

| Matchup Result                                     | Modifier |
| -------------------------------------------------- | -------: |
| Attacking Element is Strong Against Target Element |   `+25%` |
| Attacking Element is Weak Against Target Element   |   `-20%` |
| Neutral Matchup                                    |     `0%` |

## Single-Element Target Rule

For a target with one Element Type:

```text
Elemental Matchup Multiplier =
1 + Individual Matchup Modifier
```

Example:

```text
Fire attacks Earth

Individual Matchup Modifier = +25%

Elemental Matchup Multiplier =
1 + 0.25 =
1.25
```

## Multi-Element Target Rule

For a target with multiple Element Types:

1. Calculate the Individual Matchup Modifier against every Target Element Type.
2. Average those modifiers.
3. Add the result to `1`.
4. Use this as the Elemental Matchup Multiplier.

```text
Average Matchup Modifier =
Average(
Modifier against Target Element 1,
Modifier against Target Element 2
)
```

```text
Elemental Matchup Multiplier =
1 + Average Matchup Modifier
```

This means a multi-element target can have both a Strength and a Weakness against the same attacking Element.

## Multi-Element Example: Fire Against Water and Earth

```text
Target Element Types = Water,Earth
Attacking Element = Fire
```

```text
Fire against Water = Weak = -20%
Fire against Earth = Strong = +25%
```

```text
Average Matchup Modifier =
Average(-20%,+25%)

Average Matchup Modifier =
+2.5%
```

```text
Elemental Matchup Multiplier =
1 + 0.025

Elemental Matchup Multiplier =
1.025
```

Fire deals `2.5%` more Damage through the Elemental Matchup before Elemental Resistance is applied.

## Multi-Element Example: Water Against Fire and Earth

```text
Target Element Types = Fire,Earth
Attacking Element = Water
```

```text
Water against Fire = Strong = +25%
Water against Earth = Neutral = 0%
```

```text
Average Matchup Modifier =
Average(+25%,0%)

Average Matchup Modifier =
+12.5%
```

```text
Elemental Matchup Multiplier =
1 + 0.125

Elemental Matchup Multiplier =
1.125
```

Water deals `12.5%` more Damage through the Elemental Matchup.

## Holy and Darkness Rule

```text
Holy against Darkness = +25%
Darkness against Holy = +25%
```

Example:

```text
Target Element Types = Darkness,Fire
Attacking Element = Holy

Holy against Darkness = +25%
Holy against Fire = 0%

Average Matchup Modifier =
+12.5%

Elemental Matchup Multiplier =
1.125
```

## Neutral Damage Rule

```text
Neutral Elemental Multiplier = 1.00
```

Neutral Damage ignores:

* Elemental Damage Bonus
* Elemental Matchup
* Elemental Resistance

## Effective Elemental Resistance

```text
Effective Elemental Resistance =
Clamp(
Target Base Elemental Resistance
+
Target Equipment Elemental Resistance
+
Target Passive Elemental Resistance
+
Target Buff Elemental Resistance
+
Target Debuff Elemental Resistance,
-75%,
75%
)
```

## Elemental Resistance Multiplier

```text
Elemental Resistance Multiplier =
1 - Effective Elemental Resistance
```

Example:

```text
Target Fire Resistance = 20%

Elemental Resistance Multiplier =
1 - 0.20

Elemental Resistance Multiplier =
0.80
```

The target takes `80%` of incoming Fire Damage.

## Elemental Damage Bonus

```text
Effective Elemental Damage Bonus =
Attacker Equipment Elemental Damage Bonus
+
Attacker Passive Elemental Damage Bonus
+
Attacker Buff Elemental Damage Bonus
+
Attacker Debuff Elemental Damage Bonus
```

```text
Elemental Damage Bonus Multiplier =
1 + Effective Elemental Damage Bonus
```

Example:

```text
Attacker Fire Damage Bonus = 20%

Elemental Damage Bonus Multiplier =
1 + 0.20

Elemental Damage Bonus Multiplier =
1.20
```

## Final Elemental Multiplier

```text
Elemental Multiplier =
Elemental Damage Bonus Multiplier
×
Elemental Matchup Multiplier
×
Elemental Resistance Multiplier
```

## Elemental Example

```text
Attacker Fire Damage Bonus = +20%
Target Element Types = Water,Earth
Target Fire Resistance = 20%
```

```text
Fire against Water = -20%
Fire against Earth = +25%

Average Matchup Modifier =
+2.5%

Elemental Matchup Multiplier =
1.025
```

```text
Elemental Damage Bonus Multiplier =
1.20
```

```text
Elemental Resistance Multiplier =
1 - 0.20 =
0.80
```

```text
Elemental Multiplier =
1.20 × 1.025 × 0.80

Elemental Multiplier =
0.984
```

The final Fire Damage is reduced by `1.6%`.

This result is logical because:

* Fire is weak against Water.
* Fire is strong against Earth.
* The target has `20%` Fire Resistance.
* The attacker has `20%` Fire Damage Bonus.

---

# Final Damage Formula

## Damage Reduction Multiplier

```text
Effective Damage Reduction =
Clamp(
Target Base Damage Reduction
+
Target Equipment Damage Reduction
+
Target Passive Damage Reduction
+
Target Buff Damage Reduction
+
Target Debuff Damage Reduction,
0%,
75%
)
```

```text
Damage Reduction Multiplier =
1 - Effective Damage Reduction
```

Example:

```text
Damage Before Damage Reduction = 100
Effective Damage Reduction = 15%

Damage After Damage Reduction =
100 × (1 - 0.15)

Damage After Damage Reduction = 85
```

## Physical Critical Multiplier

```text
Physical Critical Multiplier = 1.00
```

when the Physical Damage Skill is not Critical.

```text
Physical Critical Multiplier =
Current Critical Damage / 100
```

when the Physical Damage Skill is Critical.

## Magic Critical Multiplier

```text
Magic Critical Multiplier = 1.00
```

Magic Damage Skills cannot Crit.

## Final Physical Damage

```text
Final Physical Damage =
Max(
1,
Floor(
Physical Damage Before Final Modifiers
×
Elemental Multiplier
×
Physical Critical Multiplier
×
Damage Reduction Multiplier
)
)
```

## Final Magic Damage

```text
Final Magic Damage =
Max(
1,
Floor(
Magic Damage Before Final Modifiers
×
Elemental Multiplier
×
Damage Reduction Multiplier
)
)
```

> Magic Damage has no Critical Multiplier in its final formula.

## Full Physical Damage Example

```text
Attacker Current Physical Attack = 60
Skill = Heavy Attack = P130
Attacker Physical Penetration = 10%
Skill Element = Fire
Attacker Fire Damage Bonus = 20%

Target Current Defense = 50
Target Element Types = Earth
Target Fire Resistance = 20%
Target Damage Reduction = 5%

Physical Critical Hit = No
```

```text
Raw Physical Damage =
60 × 1.30 =
78
```

```text
Effective Defense =
50 × (1 - 0.10) =
45
```

```text
Physical Mitigation Multiplier =
100 / (100 + 45) =
0.6897
```

```text
Physical Damage Before Final Modifiers =
78 × 0.6897 =
53.79
```

```text
Elemental Multiplier =
1.20 × 1.25 × 0.80

Elemental Multiplier =
1.20
```

```text
Damage Reduction Multiplier =
1 - 0.05 =
0.95
```

```text
Final Physical Damage =
Floor(
53.79 × 1.20 × 1.00 × 0.95
)

Final Physical Damage = 61
```

If the Physical Attack is Critical with `150%` Critical Damage:

```text
Final Physical Critical Damage =
Floor(
53.79 × 1.20 × 1.50 × 0.95
)

Final Physical Critical Damage = 91
```

## Full Magic Damage Example

```text
Attacker Current Magic Power = 70
Skill = Fire Bolt = M100
Attacker Fire Damage Bonus = 20%

Target Current Magical Defense = 40
Target Element Types = Earth
Target Fire Resistance = 20%
Target Damage Reduction = 5%
```

```text
Raw Magic Damage =
70 × 1.00 =
70
```

```text
Magic Mitigation Multiplier =
100 / (100 + 40) =
0.7143
```

```text
Magic Damage Before Final Modifiers =
70 × 0.7143 =
50.00
```

```text
Elemental Multiplier =
1.20 × 1.25 × 0.80

Elemental Multiplier =
1.20
```

```text
Damage Reduction Multiplier =
1 - 0.05 =
0.95
```

```text
Final Magic Damage =
Floor(
50.00 × 1.20 × 0.95
)

Final Magic Damage = 57
```

The Magic Damage cannot Crit.

---

# Barrier Formula

## Barrier Creation

The Barrier creator's Barrier Strength is used.

```text
Created Barrier =
Floor(
Target Max Health
×
Barrier Skill Percentage
×
Creator Barrier Strength
)
```

## Barrier Example

```text
Target Max Health = 1000
Barrier Skill = 15% of Target Max Health
Creator Barrier Strength = 125%
```

```text
Created Barrier =
Floor(
1000 × 0.15 × 1.25
)

Created Barrier = 187
```

## Barrier Absorption

```text
Barrier Absorbed Damage =
Min(
Current Barrier,
Final Damage
)
```

```text
Health Damage =
Final Damage - Barrier Absorbed Damage
```

```text
New Barrier Value =
Current Barrier - Barrier Absorbed Damage
```

## Barrier Example

```text
Current Barrier = 80
Final Damage = 125
```

```text
Barrier Absorbed Damage =
Min(80,125) =
80
```

```text
Health Damage =
125 - 80 =
45
```

```text
New Barrier Value =
80 - 80 =
0
```

The Barrier breaks and the target loses `45` Health.

## Barrier Rules

| Rule                  | Implementation                                                                               |
| --------------------- | -------------------------------------------------------------------------------------------- |
| Damage Order          | Calculate Final Damage first. Barrier absorbs Final Damage before Health is reduced.         |
| Barrier Break         | A Barrier disappears immediately when its value reaches `0`.                                 |
| Barrier Duration      | A Barrier expires when its Duration reaches `0`,even if it has remaining value.              |
| New Barrier           | A new Barrier replaces the existing Barrier only when the new Barrier value is higher.       |
| Creator Value         | Barrier Strength belongs to the unit that creates the Barrier,not the target.                |
| Barrier Cannot Crit   | Barrier creation cannot Crit.                                                                |
| Lifesteal Interaction | Lifesteal uses Health Damage dealt after Barrier absorption,not the full pre-Barrier Damage. |

---

# Healing Formula

## Direct Healing

```text
Final Healing =
Floor(
Base Healing
×
Target Healing Received
)
```

## Percentage Healing

```text
Base Healing =
Target Max Health
×
Healing Percentage
```

## Healing Received

```text
Effective Healing Received =
Clamp(
Target Base Healing Received
+
Target Equipment Healing Received Modifiers
+
Target Passive Healing Received Modifiers
+
Target Buff Healing Received Modifiers
+
Target Debuff Healing Received Modifiers,
0%,
200%
)
```

> `100%` Healing Received is normal healing.
> `80%` Healing Received means the target receives `20%` less healing.
> `125%` Healing Received means the target receives `25%` more healing.

## Heal Example

```text
Target Max Health = 800
Heal Skill = 18% of Target Max Health
Target Healing Received = 80%
```

```text
Base Healing =
800 × 0.18 =
144
```

```text
Final Healing =
Floor(
144 × 0.80
)

Final Healing = 115
```

## Regeneration

```text
Regeneration Healing Per Tick =
Floor(
Target Max Health
×
Regeneration Percentage
×
Target Healing Received
)
```

Regeneration triggers at the end of the affected target's own Action.

## Healing Rules

| Rule             | Implementation                                                                          |
| ---------------- | --------------------------------------------------------------------------------------- |
| Maximum Health   | Healing cannot increase Health above Max Health.                                        |
| Critical Healing | Healing cannot Crit unless a future Skill explicitly says so.                           |
| Barrier          | Healing does not restore Barrier value.                                                 |
| Healing Received | Applies to Potions,Heal,Regeneration,Lifesteal,and similar effects.                     |
| Lifesteal        | Healing from Lifesteal is calculated from Health Damage dealt after Barrier absorption. |
| Dead Target      | A defeated target cannot be healed unless a future Revive effect explicitly allows it.  |

---

# Damage-Over-Time Formula

## General Rule

Damage-Over-Time effects do not perform Accuracy checks and cannot Crit.

When a Damage-Over-Time effect is applied,store the relevant offensive attribute from the source.

```text
Stored Source Attribute =
Source Current Physical Attack
```

for a Physical source.

```text
Stored Source Attribute =
Source Current Magic Power
```

for a Magic source.

The source snapshot remains stored even if the source later gains or loses attributes.

## Damage-Over-Time Effects

| Status   | Tick Timing                                                                     | Coefficient | Damage Type            | Element  | Additional Rule                              |
| -------- | ------------------------------------------------------------------------------- | ----------: | ---------------------- | -------- | -------------------------------------------- |
| Burn     | End of affected target's Action                                                 |      `0.45` | Same as applying Skill | Fire     | Uses stored source Attack Attribute.         |
| Poison   | End of affected target's Action                                                 |      `0.35` | Same as applying Skill | Neutral  | Ignores `50%` of the relevant Defense value. |
| Bleeding | After affected target uses a Physical Skill or receives a Physical Critical Hit |      `0.45` | Physical               | Neutral  | Uses stored Physical Attack.                 |
| Curse    | End of affected target's Action                                                 |      `0.40` | Magic                  | Darkness | Uses stored Magic Power.                     |

## Damage-Over-Time Formula

```text
DoT Raw Damage =
Stored Source Attribute
×
DoT Coefficient
```

Then resolve the normal Damage Formula using:

* the listed Damage Type;
* the listed Element;
* the target's current Defense or Magical Defense;
* the target's current Elemental Resistance;
* the target's current Damage Reduction;
* no Accuracy check;
* no Critical check.

## Burn Example

```text
Source used a Physical Fire Skill.
Source Current Physical Attack when Burn was applied = 50
Burn Coefficient = 0.45

Target Current Defense = 30
Target Element Types = Earth
Target Fire Resistance = 20%
```

```text
Burn Raw Damage =
50 × 0.45 =
22.5
```

```text
Physical Mitigation Multiplier =
100 / (100 + 30) =
0.7692
```

```text
Fire Matchup Multiplier against Earth =
1.25
```

```text
Fire Resistance Multiplier =
1 - 0.20 =
0.80
```

```text
Burn Damage =
Floor(
22.5 × 0.7692 × 1.25 × 0.80
)

Burn Damage = 17
```

## Damage-Over-Time Rules

| Rule                 | Implementation                                                                                           |
| -------------------- | -------------------------------------------------------------------------------------------------------- |
| Source Snapshot      | Store the source's relevant offensive attribute when the effect is applied.                              |
| Target Defenses      | Use the target's current Defense,Magical Defense,Resistances,and Damage Reduction when each tick occurs. |
| Critical Hits        | Damage-Over-Time cannot Crit.                                                                            |
| Accuracy             | Damage-Over-Time cannot miss.                                                                            |
| Reapplication        | Do not reapply the same Damage-Over-Time effect while it has at least 1 Action remaining.                |
| Duration             | A Duration of `3` means the affected target can receive up to 3 ticks.                                   |
| Target Death         | Damage-Over-Time stops immediately when the target is defeated.                                          |
| Fast Target Tradeoff | A fast target receives more Damage-Over-Time ticks over real combat time because it acts more often.     |
| Source Death         | The effect continues after the source is defeated because the source attribute was stored when applied.  |

---

# Status Resistance Formula

## Status Application Order

```text
1. Check whether the target is immune to the Status.
2. Check whether the target already has the same Status.
3. Check whether the Skill must hit:
   - Physical Skills use Accuracy vs. Evasion.
   - Magic Skills always hit.
   - No-Damage Magic Debuffs do not use Accuracy.
4. Calculate Total Status Resistance.
5. Calculate Final Status Chance.
6. Roll Final Status Chance.
7. Apply the Status with its listed Duration when successful.
```

## Total Status Resistance

```text
Total Status Resistance =
Clamp(
Target Global Status Resistance
+
Target Specific Status Resistance
+
Target Equipment Status Resistance
+
Target Passive Status Resistance
+
Target Buff Status Resistance
+
Target Debuff Status Resistance,
-50%,
80%
)
```

Specific Status Resistance is used only when it matches the incoming Status.

```text
Example:

Incoming Status = Stun

Use:
- Global Status Resistance
- Stun Resistance
- all temporary general Status Resistance modifiers
- all temporary Stun Resistance modifiers
```

Do not use:

```text
- Poison Resistance
- Burn Resistance
- Freeze Resistance
```

when the incoming Status is Stun.

## Final Status Chance

```text
Final Status Chance =
Clamp(
Base Status Chance
-
Total Status Resistance,
0%,
100%
)
```

## Status Resistance Example

```text
Root Snare Base Chance = 65%

Target Global Status Resistance = 15%
Target Rooted Resistance = 5%
```

```text
Total Status Resistance =
15% + 5%

Total Status Resistance = 20%
```

```text
Final Rooted Chance =
65% - 20%

Final Rooted Chance = 45%
```

The final chance to apply Rooted is `45%`.

## Negative Status Resistance Example

```text
Burn Base Chance = 50%
Target Burn Resistance = -20%
```

```text
Final Burn Chance =
50% - (-20%)

Final Burn Chance = 70%
```

Negative Status Resistance makes the target more vulnerable.

## Status Resistance Rules

| Rule                       | Implementation                                                                                          |
| -------------------------- | ------------------------------------------------------------------------------------------------------- |
| Global Status Resistance   | Reduces the chance of every negative Status Effect.                                                     |
| Specific Status Resistance | Reduces only one Status Type. Example: `Stun Resistance +30%`.                                          |
| Temporary Resistance       | Can come from Buffs,Potions,Equipment Effects,or Boss Flags.                                            |
| Negative Resistance        | Increases the Final Status Chance.                                                                      |
| Status Immunity            | Sets Resistance for that specific Status to `100%`.                                                     |
| Guaranteed Status          | A `100%` Base Status Chance is still reduced by Status Resistance unless the Skill says `Unresistable`. |
| Unresistable Status        | Ignores Status Resistance but not Status Immunity.                                                      |
| Existing Status            | Do not reapply the same Status while it has at least 1 Action remaining.                                |
| Duration                   | Status Resistance reduces application chance only. It does not reduce Duration.                         |
| Maximum Chance             | Final Status Chance cannot exceed `100%`.                                                               |
| Minimum Chance             | Final Status Chance can reach `0%`.                                                                     |

---

# Effect Duration Rules

## Default Durations

| Effect Type                                                                                                                | Default Duration |
| -------------------------------------------------------------------------------------------------------------------------- | ---------------: |
| Burn,Poison,Bleeding,Curse                                                                                                 |        3 Actions |
| Weakness,Magic Break,Armor Break,Magic Vulnerability,Blind,Slow,Crippled,Wet,Scorched,Cracked,Winded,Shadow Mark,Holy Mark |        2 Actions |
| Stun,Sleep,Freeze,Confusion,Fear,Silence                                                                                   |         1 Action |
| Fortify,Barrier,Haste,Focus,Evasion Up,Magic Ward                                                                          |        2 Actions |
| Regeneration,Berserk                                                                                                       |        3 Actions |

## Duration Meaning

```text
Duration = 2 Actions
```

means the effect remains active through the affected target's next 2 completed Actions.

It does not mean two global rounds.

## Buff Duration Example

```text
Player receives Fortify with Duration 2.

Player's next Action:
Fortify is active.
Player completes the Action.
Fortify Duration becomes 1.

Player's following Action:
Fortify is active.
Player completes the Action.
Fortify Duration becomes 0.
Fortify is removed.
```

## Debuff Duration Example

```text
Enemy receives Armor Break with Duration 2.

Enemy's next Action:
Armor Break is active.
Enemy completes the Action.
Armor Break Duration becomes 1.

Enemy's following Action:
Armor Break is active.
Enemy completes the Action.
Armor Break Duration becomes 0.
Armor Break is removed.
```

## Effect Timing Rules

| Effect Type      | Timing Rule                                                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------- |
| Buff             | Applies immediately and remains until the affected unit completes the listed number of Actions. |
| Debuff           | Applies immediately and remains until the affected unit completes the listed number of Actions. |
| Damage-Over-Time | Ticks at the end of the affected unit's Action before Duration is reduced.                      |
| Regeneration     | Heals at the end of the affected unit's Action before Duration is reduced.                      |
| Action Denial    | Consumes the target's next Action and then expires.                                             |
| Haste            | Changes Effective Speed immediately for future Action Gauge filling.                            |
| Slow             | Changes Effective Speed immediately for future Action Gauge filling.                            |
| Silence          | Prevents Magic Skills during every affected Action.                                             |
| Blind            | Affects Physical Hit Chance during every affected Action.                                       |
| Rooted           | Does not prevent an Action. It applies its separate movement,evasion,or escape rule.            |
| Confusion        | Uses the Confusion behaviour defined by the final Status Effect specification.                  |
| Fear             | Uses the Fear behaviour defined by the final Status Effect specification.                       |

---

# Mana and Skill Use Rules

## Player Mana

```text
After the Player uses a Skill:

New Mana =
Current Mana - Skill Mana Cost
```

A Player Skill is valid only when:

```text
Current Mana >= Skill Mana Cost
```

## Mana Regeneration

```text
At the end of the Player's Action:

New Mana =
Min(
Max Mana,
Current Mana + Mana Regeneration
)
```

Apply Mana Regeneration after Damage-Over-Time and Regeneration effects.

## Enemy Skills

| Rule                    | Implementation                                                                             |
| ----------------------- | ------------------------------------------------------------------------------------------ |
| Enemy Mana              | Enemies do not use Mana.                                                                   |
| Enemy Skill Restriction | Enemy Skills are restricted by Cooldowns,AI Priority,valid targets,and special conditions. |
| Enemy AI Selection      | The first valid AI Priority rule is selected.                                              |
| Fallback                | If no AI Priority rule is valid,the enemy uses Basic Attack against the Player.            |

---

# Combat Resolution Order

## Physical Damage Skill

```text
1. Calculate Current Attributes.
2. Check whether the Skill is valid:
   Mana,Cooldown,Silence,target validity,and AI conditions.
3. Check Physical Hit Chance.
4. If the attack misses,stop Damage resolution.
5. Check Physical Critical Hit.
6. Calculate Raw Physical Damage.
7. Apply Physical Penetration and Skill Defense Ignore.
8. Apply Defense Mitigation.
9. Apply Elemental Damage Bonus,Elemental Matchup,and Elemental Resistance.
10. Apply Physical Critical Multiplier.
11. Apply Damage Reduction.
12. Apply Barrier absorption.
13. Reduce target Health.
14. Resolve Lifesteal if applicable.
15. Roll Status Chance if the Skill applies a Status.
```

## Magic Damage Skill

```text
1. Calculate Current Attributes.
2. Check whether the Skill is valid:
   Mana,Cooldown,Silence,target validity,and AI conditions.
3. Magic Damage automatically hits.
4. Do not check Critical Hit.
5. Calculate Raw Magic Damage.
6. Apply Magic Penetration and Skill Magical Defense Ignore.
7. Apply Magical Defense Mitigation.
8. Apply Elemental Damage Bonus,Elemental Matchup,and Elemental Resistance.
9. Apply Damage Reduction.
10. Apply Barrier absorption.
11. Reduce target Health.
12. Resolve Lifesteal if applicable.
13. Roll Status Chance if the Skill applies a Status.
```

## No-Damage Debuff Skill

```text
1. Check whether the Skill is valid.
2. Check Status Immunity.
3. Check whether the target already has the same Status.
4. Use a Physical Hit Check if the Skill is Physical.
5. Skip the Hit Check if the Skill is Magic or a pure Magic Debuff.
6. Calculate Total Status Resistance.
7. Calculate Final Status Chance.
8. Roll Final Status Chance.
9. Apply the Status when successful.
```

## Buff,Heal,or Barrier Skill

```text
1. Check whether the Skill is valid.
2. Select the target through Player input or Enemy AI Priority.
3. Check whether the target already has the same Buff.
4. Apply the Buff,Heal,Barrier,or Regeneration.
5. Store the Action ID in which the effect was applied.
6. Do not reduce Duration on the Action in which the effect was applied.
```

---

# Enemy AI Resolution

## AI Priority Rule

```text
1. Read Group AI Priority when at least one friendly enemy is alive.
2. Read Solo AI Priority when the enemy is the only living enemy.
3. Evaluate rules from top to bottom.
4. The first rule with a valid Skill,valid condition,and valid target is used.
5. If no rule is valid,use Basic Attack against the Player.
```

## Example AI Priority

```text
1. Heal → [Lowest HP Friendly at HP <= 40%]
2. Barrier → [Lowest HP Friendly at HP <= 65% if no Barrier]
3. Root Snare → [Player if no Rooted]
4. Dark Bolt → [Player]
5. Basic Attack → [Player]
```

## AI Targeting Rules

| Target Rule                | Meaning                                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------------------------- |
| Player                     | The single Player character.                                                                            |
| Self                       | The enemy using the Skill.                                                                              |
| Lowest HP Friendly         | Living friendly target with the lowest current HP percentage.                                           |
| Highest Physical Friendly  | Living friendly target with the highest Physical Attack.                                                |
| Highest Magic Friendly     | Living friendly target with the highest Magic Power.                                                    |
| Friendly With Most Debuffs | Living friendly target with the most negative effects. If tied,choose the one with lower HP percentage. |
| All Friendlies             | Every living friendly enemy,including the caster. Maximum 3 targets.                                    |
| No Target                  | Used by Summon Skills.                                                                                  |

---

# Core Formula Reference

## Current Stat

```text
Current Stat =
Floor(
Base Stat × (1 + Total Stat Modifier)
)
```

## Effective Speed

```text
Effective Speed =
Max(
1,
Floor(
Base Speed × (1 + Total Speed Modifier)
)
)
```

## Time Until Next Action

```text
Time Until Next Action =
(100 - Current Action Gauge)
/
Effective Speed
```

## Physical Hit Chance

```text
Raw Physical Hit Chance =
100%
-
Max(
0%,
Target Evasion - Attacker Accuracy
)
```

```text
Final Physical Hit Chance =
Clamp(
Raw Physical Hit Chance,
10%,
95%
)
```

## Effective Penetration

```text
Effective Penetration =
1 - (
(1 - Attribute Penetration)
×
(1 - Skill Penetration)
)
```

## Defense Mitigation

```text
Defense Mitigation Multiplier =
100
/
(100 + Effective Defense)
```

## Multi-Element Matchup

```text
Average Matchup Modifier =
Average(
Individual Modifier against every Target Element Type
)
```

```text
Elemental Matchup Multiplier =
1 + Average Matchup Modifier
```

## Elemental Multiplier

```text
Elemental Multiplier =
(1 + Elemental Damage Bonus)
×
Elemental Matchup Multiplier
×
(1 - Elemental Resistance)
```

## Final Physical Damage

```text
Final Physical Damage =
Max(
1,
Floor(
Physical Damage Before Final Modifiers
×
Elemental Multiplier
×
Physical Critical Multiplier
×
Damage Reduction Multiplier
)
)
```

## Final Magic Damage

```text
Final Magic Damage =
Max(
1,
Floor(
Magic Damage Before Final Modifiers
×
Elemental Multiplier
×
Damage Reduction Multiplier
)
)
```

## Final Status Chance

```text
Final Status Chance =
Clamp(
Base Status Chance
-
Total Status Resistance,
0%,
100%
)
```

## Created Barrier

```text
Created Barrier =
Floor(
Target Max Health
×
Barrier Skill Percentage
×
Creator Barrier Strength
)
```

## Final Healing

```text
Final Healing =
Floor(
Base Healing
×
Target Healing Received
)
```

---

## Documentation Links

This preserved source is retained in full. The canonical integrated design is in
[02_Attributes_and_Combat.md](02_Attributes_and_Combat.md); the documentation index is [00_README.md](00_README.md).
Where this source conflicts with newer documents, see
[16_Consistency_Audit.md](16_Consistency_Audit.md) rather than deleting this record.

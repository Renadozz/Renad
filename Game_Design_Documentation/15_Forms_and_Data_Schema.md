# Forms, UI Contracts, and Data Schema

## Linked documents

[System overview](01_System_Overview.md) · [Player and Skills](04_Player_and_Skills.md) · [Equipment](05_Equipment_and_Drop_Pools.md) · [Enemy Codex](12_Enemy_Codex.md) · [Town](09_Town_Quests_and_Contracts.md)

## Form design principles

|Rule|Implementation|
|---|---|
|Source of truth|Forms display canonical IDs and values from the linked system documents.|
|Validation|All choices are validated before a permanent action consumes Gold, materials, or an item.|
|Quest safety|Quest Items never appear as valid sell/salvage/disenchant/upgrade choices.|
|Preview first|Upgrade, enchant, crafting, and purchase forms display costs and result before confirmation.|
|Autosave|Success is saved after the entire form action finishes successfully.|
|Accessibility|Every interactive control needs a visible label, a programmatic label, keyboard access, focus order, and an error message associated with its input.|

## Player and combat forms

|Form|Required fields|Validation|Writes to|
|---|---|---|---|
|Character Sheet|Level, HP/Max HP, MP/Max MP, core stats, resistances, equipped item IDs, Skill Points.|Current values within min/max; required equipment IDs exist.|Player state.|
|Skill Screen|Learned Skills, available Skill Points, three Passive Slots, equipment state.|Skill cost available; requirement satisfies passive/skill eligibility.|Player learned skills/loadout.|
|Combat Action|Actor ID, action type, Skill/Item ID, target IDs.|Mana, cooldown, status restriction, target count, inventory availability.|Combat action log.|
|Status Panel|Target ID, active status, remaining own actions, source ID.|No duplicate status unless explicit replacement rule.|Combat status collection.|
|Equipment Screen|Main Hand, Off Hand, Armor, Helmet, Accessory IDs.|Two-hand lock; slot/type compatibility; passive updates.|Equipment loadout.|

## Economy and crafting forms

|Form|Required fields|Validation|Writes to|
|---|---|---|---|
|Market Purchase|Item ID, quantity, current Gold, stock state.|Stock/unlock condition; sufficient Gold; Backpack capacity.|Inventory, Gold, stock.|
|Market Sell|Sellable Item ID, quantity.|Not Quest Item; quantity owned; no protected state.|Inventory, Gold.|
|Backpack Upgrade|Current capacity, target upgrade, Gold.|Next sequential tier only; unlock complete; enough Gold.|Backpack capacity, Gold.|
|Alchemy Craft|Recipe ID, quantity, ingredient inventory.|All exact recipe inputs available; output stack capacity.|Materials, output inventory.|
|Blacksmith Upgrade|Equipment ID, source +0 stats, current upgrade, materials, Gold.|Eligible; max +5; sufficient materials/Gold.|Equipment upgrade level, materials, Gold.|
|Enchanter Grade|Equipment ID, grade, traits, materials, Gold.|Eligible; next grade exists; valid trait candidate list for weapons/shields.|Grade, trait collection, materials, Gold.|
|Salvage/Disenchant|Equipment ID, action.|Not Quest Item; action is mutually exclusive with sale.|Equipment deletion, material inventory.|

## Quest, map, and encounter forms

|Form|Required fields|Validation|Writes to|
|---|---|---|---|
|Quest Log|Quest ID, state, objectives, linked Item IDs.|Only next Story Quest advances; one active Repeatable Contract.|Quest state.|
|Contract Board|Available contracts, selected Contract ID.|Area unlocked; active contract limit = 1.|Contract state.|
|City Gate|Selected area, discovered safe nodes, story gate state.|Area unlocked; boss gate/contract state valid.|Location state.|
|Encounter Resolver|Area ID, eligible templates, quest state, seed/weight result.|No invalid template; max 3 living enemies.|Encounter state.|
|Loot Result|Enemy ID, fixed Gold/XP/materials, equipment roll, Quest Item state.|Resolve in order specified by System Overview.|Inventory, Gold, XP, quest objective.|
|Boss Challenge|Boss ID, linked contract ID, story completion state.|Story boss defeated; exact Challenge Contract active.|Encounter + conditional proof.|

## Core data schemas

### Item

```text
ItemId
DisplayName
Category
StackLimit
Sellable
QuestItemFlag
BaseValue
SellValue
Grade
UpgradeLevel
Slot
WeaponType
HandRequirement
ElementTypes[]
BaseStats{}
BuiltInEffects[]
TraitEntries[]
SourcePoolIds[]
```

### Enemy

```text
EnemyId
DisplayName
AreaIds[]
Rank
CombatRole
ElementTypes[]
BaseStatProfile { Level, MaxHealth, PhysicalAttack, MagicPower, Defense, MagicalDefense,
                  Speed, Accuracy, Evasion, CriticalChance, StatusResistance, Resistances{} }
GroupAiPriority[]
SoloAiPriority[]
BossFlags {}
FixedExperience
FixedGold
GuaranteedMaterialDrops [{ ItemId, Quantity }]
EquipmentPoolId
EquipmentRollChance
ConditionalQuestDrops [{ QuestOrContractId, ItemId, Quantity, StopWhenObjectiveComplete }]
```

### Equipment trait entry

```text
TraitId
TraitName
TraitGrade
TraitFamily
RolledValue
Trigger
Effect
Duration
```

### Quest / Contract

```text
QuestId
Type (Story, Guild, KillContract, CollectionContract, UniqueBounty, BossChallenge)
State
AreaId
Objectives[]
RequiredQuestItemIds[]
RewardBundle
SpawnConditions[]
```

## Form-to-document traceability

|Field group|Canonical reference|
|---|---|
|Combat calculations|[02_Attributes_and_Combat.md](02_Attributes_and_Combat.md)|
|Status names/durations/removal|[03_Status_Effects_and_Consumables.md](03_Status_Effects_and_Consumables.md)|
|Skills and passive slots|[04_Player_and_Skills.md](04_Player_and_Skills.md)|
|Equipment / pools / traits|[05_Equipment_and_Drop_Pools.md](05_Equipment_and_Drop_Pools.md), [08_Blacksmith_and_Enchanter.md](08_Blacksmith_and_Enchanter.md)|
|Prices and selling|[06_Item_Price_Catalog.md](06_Item_Price_Catalog.md)|
|Enemy reward data and AI|[12_Enemy_Codex.md](12_Enemy_Codex.md), [13_Enemy_AI_Patterns.md](13_Enemy_AI_Patterns.md)|
|Boss state and gates|[14_Boss_Patterns.md](14_Boss_Patterns.md)|

## Balance 2.0 schema override

### Equipment eligibility fields

```text
UpgradeEligible (Boolean)
GradeEligible (Boolean)
SalvageEligible (Boolean)
DisenchantEligible (Boolean)
AccessorySlotLimit = 1
GradeEffectEntries[]
GradePassiveEntries[]
```

Rules:

- Accessories set all four eligibility fields to `false` and use the single Accessory slot.
- Armor can have Grade Effect and Grade Passive entries under Balance 2.0.
- Mythic two-hand weapons require space for up to 4 Grade Effects and 3 Grade Passives total.
- Item sale preview must use original `+0 BaseValue × 25%` and must not recalculate from upgrades or grades.

### Enemy link fields

```text
AiPatternAnchor
CraftingLootProfileAnchor
RebalancedLevel
FixedExperience
FixedGold
```

The Monster Loot resolver must process the profile linked from `CraftingLootProfileAnchor` after guaranteed material awards.

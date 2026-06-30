# Economy, Market, and Alchemy

## Linked documents

[Item price catalog](06_Item_Price_Catalog.md) · [Status effects, recipes, and ingredients](03_Status_Effects_and_Consumables.md) · [Equipment](05_Equipment_and_Drop_Pools.md) · [Blacksmith and Enchanter](08_Blacksmith_and_Enchanter.md) · [Town and contracts](09_Town_Quests_and_Contracts.md)

## Market purpose and active stock

The Market is an emergency and starter-build service, not a replacement for the Monster → Crafting → Upgrade loop.

|Item / group|Buy price|Stock|Active Market rule|
|---|---:|---:|---|
|Small Health Potion|35 Gold|8 per restock|Only low recovery HP Potion sold. Restores 45 HP.|
|Small Mana Potion|40 Gold|8 per restock|Only low recovery MP Potion sold. Restores 18 MP.|
|Smoke Bomb|80 Gold|3 per restock|Utility; not a Potion.|
|Recall Potion|150 Gold|2 per restock|Out-of-combat utility; not a Potion.|
|Empty Bottle|5 Gold|10 per restock|Crafting container.|
|Empty Oil Flask|8 Gold|5 per restock|Crafting container.|
|Iron Scrap|60 Gold|3 per restock|Emergency Blacksmith input only; farming is economically better.|
|Starter Equipment|See Price Catalog|1 each per restock|One base Weapon for every path, Shield, and every Armor category.|

**Restock rule:** a limited item restocks only after the Player completes at least 3 normal/elite encounters, a Boss, or a Quest objective and then returns to Town. Re-entering Town without progress does not refresh Market stock.

## Completed consumables that are not Market stock

|Category|Rule|
|---|---|
|Health Potion and all stronger HP recovery|Craft only or a named quest/chest/boss reward.|
|Mana Potion and all stronger MP recovery|Craft only or a named quest/chest/boss reward.|
|Antidote, Bandage, Burn Salve, Mind Tonic, Awakening, Purifying|Craft only.|
|Buff, resistance, and Oil consumables|Craft only.|
|Phoenix, Last Stand, Vampiric, Experience, and Gold Potions|Mythic craft or specific reward only.|
|Ingredients and upgrade/enchantment materials except Iron Scrap and containers|Farmed from Monsters, Quests, Contracts, salvage, or disenchanting.|

## Alchemist loop

```text
Monster / Quest material
  → Backpack stack
  → recipe unlock and ingredient validation
  → guaranteed-success batch craft
  → fixed-value recovery, medicine, buff, resistance, oil, or utility item
```

|Rule|Implementation|
|---|---|
|Crafting success|Always succeeds.|
|Batch crafting|Allowed while all inputs and Backpack capacity are available.|
|Stacking|Crafted consumables stack to 99 per item type.|
|Recovery control|Recovery Items use the 2-own-action Recovery Item Cooldown described in [Status effects](03_Status_Effects_and_Consumables.md#potion-action-reuse-and-duration-rules).|
|Potions in combat|Using one consumes a Player action; `Alchemist's Pouch` gives one additional once-per-battle different-Potion use.|
|Early countermeasure protection|Bandage, Antidote, Mind Tonic, Awakening, Burn Salve, and Purifying become farmable before or by their first meaningful status pressure.|

## Selling and destructive choices

```text
Sell equipment → Gold at 25% of original +0 Base Value
or Blacksmith Salvage → Smithing materials
or Enchanter Disenchant → Enchantment materials
```

Only one destructive path may be chosen. Accessories may be sold but can never be upgraded, graded, salvaged, or disenchanted. Quest Items, Sigils, and the Dragon King's Seal cannot be sold or destroyed.

## Backpack

The Backpack begins at 10 slots and is expanded to 40 via the Pack Merchant. Gold uses no slot. Quest Items use a separate 0-slot Quest inventory. A full Backpack blocks normal loot but never a required Quest Item.

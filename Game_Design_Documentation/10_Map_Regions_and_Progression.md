# Map, Regions, Areas, and World Progression

## Linked documents

[Town and quests](09_Town_Quests_and_Contracts.md) · [Encounter spawns](11_Encounter_Spawns.md) · [Enemy Codex](12_Enemy_Codex.md) · [Boss patterns](14_Boss_Patterns.md)

## Global story path

```text
Town Archive
  → T1: Earth → Air → Water → Fire → Darkness → Holy
  → T2: Earth → Air → Water → Fire → Darkness → Holy
  → T3: Earth → Air → Water → Fire → Darkness → Holy
  → T4: Earth → Air → Water → Fire → Darkness → Holy
  → T5: Earth → Air → Water → Fire → Darkness → Holy
  → T6 regional boss sigils in the same elemental order
  → Dragon King's Dominion
```

## Area map

|Region|Element|Area progression|Area-final boss|
|---|---|---|---|
|Earth|Earth|Forest Entrance → Goblin Forest → Overgrown Trail → Deep Woods → King's Clearing|Goblin King|
|Air|Air|Desert Border → Scorching Dunes → Bandit Camp → Ancient Ruins → Ruin Guardian Chamber|Ruin Guardian|
|Water|Water|Mountain Foothills → Mountain Pass → Echo Mine → Ice Caves → Frozen Peak → Summit Shrine|Frost Titan|
|Fire|Fire|Ashen Border → Ember Fields → Lava Fissures → Magma Forge → Inferno Core|Inferno Lord|
|Darkness|Darkness|Gloomwood → Shadow Marsh → Forgotten Crypt → Void Rift → Dread Throne|Shadow Lord|
|Holy|Holy|Sunlit Road → Temple Gardens → Sanctum Halls → Dawn Basilica → Oracle Chamber|Oracle|
|Dragon|Multiple|Dragon Valley → Dragon Cave → Obsidian Citadel → Ancient Nest → Dragon King's Lair|Ancient Dragon / Dragon King|

## World Tier interpretation

|World Tier|Meaning|Areas|
|---|---|---|
|1|Outer routes|First area in each elemental region.|
|2|Inner trails|Second area in each elemental region.|
|3|Contested grounds|Third area in each elemental region.|
|4|Deep sanctums|Fourth area in each elemental region.|
|5|Boss approaches|King's Clearing, Ruin Chamber approach, Frozen Peak, Inferno Core, Dread Throne, Oracle Chamber.|
|6|Boss encounter stage|Regional boss fight and one permanent Sigil, except the Dragon region.|
|Dragon 1–4|Endgame route|Dragon Valley through Ancient Nest.|
|Dragon 5|Final story encounter|Dragon King's Lair; one-time only.|

## Gate rules

|Gate|Unlock condition|
|---|---|
|Next elemental area|Complete immediately previous global Story Quest.|
|Regional boss|Its World Tier 6 Story Quest must be active.|
|Boss challenge|Story boss already defeated and matching Challenge Contract active.|
|Dragon King's Dominion|All six Regional Sigils, then `S-DRAGON-00`.|
|Dragon King|`S-DRAGON-05` active; this is a one-time solo fight.|
|Return travel|Discovered safe point, map action, or Recall Potion outside battle.|

## Clarified Water progression

`Frozen Peak` is the **Tier 5 approach area** with normal enemies and its own contracts. `Summit Shrine` is the **Tier 6 Frost Titan arena**. This separates the two concepts that were compressed into one cell in the older progression table.

## Added map nodes for active recipe support

No additional map area was required. The added enemies in [12_Enemy_Codex.md](12_Enemy_Codex.md) are inserted into existing areas: Goblin Forest, Scorching Dunes, Deep Woods, Ice Caves, Ancient Ruins, and Frozen Peak.

## Skill-tier progression link

Entering a new World Tier unlocks its corresponding Skill Tier for all previously eligible trees. The required Elemental School still needs its first regional access. Exact Tier I–VI conditions are in [Expanded Player Skill Trees and Unlocks](04_Player_and_Skills.md) and level targets are in [Progression, XP, and Level Balance](02_Attributes_and_Combat.md).

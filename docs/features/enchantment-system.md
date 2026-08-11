---
type: concept
title: "Ancient Tomes and Enchantment Pipeline"
summary: "Vane custom-item, loot, recipe, registry, and disenchanting behavior used to obtain custom enchantments."
tags: [vane, enchantments, ancient-tome, loot, recipes]
---

# Ancient Tomes and Enchantment Pipeline

## Priority

**Required as a system.** The replacement should reproduce the Vane progression model as closely as practical. Soulbound and Unbreakable are mandatory enchantments; other enchantments are optional.

## Tome tiers

Vane defines three normal tome items and corresponding enchanted variants:

| Tier | Normal item | Base material | Model data | Enchanted item | Base material | Model data |
| --- | --- | --- | ---: | --- | --- | ---: |
| Basic | `vane_enchantments:ancient_tome` | Book | `0x770000` | `vane_enchantments:enchanted_ancient_tome` | Enchanted Book | `0x770001` |
| Knowledge | `vane_enchantments:ancient_tome_of_knowledge` | Book | `0x770002` | `vane_enchantments:enchanted_ancient_tome_of_knowledge` | Enchanted Book | `0x770003` |
| Gods | `vane_enchantments:ancient_tome_of_the_gods` | Book | `0x770004` | `vane_enchantments:enchanted_ancient_tome_of_the_gods` | Enchanted Book | `0x770005` |

All six are version `1` custom items.

Vane identifies custom items using persistent item metadata containing:

- `vane:custom_item_identifier` — the namespaced custom-item key;
- `vane:custom_item_version` — integer item version;
- custom model data for the corresponding resource-pack model.

The replacement does not need to retain those exact internal PDC keys if a different data-driven item identity is preferable, but existing Vane items may need a migration path if old inventories/worlds are to remain compatible.

## Resource-pack presentation

The normal and enchanted variants share the same human-readable tier names:

- Ancient Tome;
- Ancient Tome of Knowledge;
- Ancient Tome of The Gods.

Vane provides custom item models/textures under the `vane_enchantments` resource namespace. A replacement resource pack should maintain distinct visual identity for the tome tiers, even if modern item-model components replace Vane's custom-model-data approach.

## Progression recipes

### Ancient Tome of Knowledge

Shapeless recipe:

- 1 Ancient Tome;
- 1 Feather;
- 1 Blaze Rod;
- 1 Ghast Tear.

Result: 1 Ancient Tome of Knowledge.

### Ancient Tome of the Gods

Shaped recipe:

```text
 N 
EKE
 S 
```

where:

- `N` = Nether Star;
- `E` = any Enchanted Book;
- `K` = Ancient Tome of Knowledge;
- `S` = Nautilus Shell.

The two enchanted books may contain any enchantments; their enchantments are not part of the ingredient constraint.

## Basic Ancient Tome loot

The basic Ancient Tome is injected alongside normal loot. Each configured loot entry is evaluated independently with its configured probability.

For these vanilla tables, Vane uses a **1/5** chance and an amount range of **0–2**:

- Abandoned Mineshaft;
- Bastion Bridge;
- Bastion Hoglin Stable;
- Bastion Other;
- Bastion Treasure;
- Buried Treasure;
- Desert Pyramid;
- End City Treasure;
- Fishing Treasure;
- Igloo Chest;
- Jungle Temple;
- Nether Bridge;
- Pillager Outpost;
- Ruined Portal;
- Shipwreck Treasure;
- Stronghold Library;
- Underwater Ruin Big;
- Underwater Ruin Small;
- Village Temple;
- Woodland Mansion.

Because the amount is sampled from `0` through `2`, a successful chance roll may still yield zero items.

Ancient City uses a **1/20** chance with amount **0–2**.

Vane additionally supports a set of Terralith loot tables. Those should be treated as compatibility extras and only reproduced if Terralith remains part of the server stack.

## Knowledge Tome loot

Ancient Tome of Knowledge appears as one item at **1/40** in:

- Abandoned Mineshaft;
- Bastion Treasure;
- Buried Treasure;
- Desert Pyramid;
- Nether Bridge;
- Ruined Portal;
- Shipwreck Treasure;
- Stronghold Library;
- Underwater Ruin Big;
- Village Temple;
- Woodland Mansion.

Ancient City contains two independent **1/30** entries for the same tome. Vane comments that this duplication is intentional for more consistent spawning.

Terralith tables are also supported with analogous normal/rare probabilities.

## Gods Tome loot

Ancient Tome of the Gods appears as one item at **1/200** in:

- Bastion Treasure;
- Buried Treasure;
- Shipwreck Treasure;
- Underwater Ruin Big.

Ancient City uses **1/150**. Vane also defines Terralith normal/rare entries at **1/200** and **1/150** respectively.

## Crafting custom enchantments

Each Vane enchantment defines a crafting recipe whose central progression ingredient is one of the normal tome tiers. The recipe result is the corresponding **enchanted** tome variant carrying that custom enchantment.

For example, Soulbound and Unbreakable consume an Ancient Tome of the Gods and produce an Enchanted Ancient Tome of the Gods with the requested enchantment stored on it.

This means the tome tier is both:

1. a progression/crafting ingredient; and
2. the physical enchanted-book-like carrier for the resulting enchantment.

The enchanted tome can then participate in normal enchantment/anvil mechanics as an enchanted-book-like item, subject to the registered supported-item and exclusivity rules.

## Enchantment registry behavior

Current Vane registers custom enchantments during Paper bootstrap using the Paper enchantment registry API. Shared defaults include:

- anvil cost: `1`;
- weight: `10`;
- active slots: any;
- minimum registry cost: `(1, 1)`;
- maximum registry cost: `(3, 1)`;
- supported item sets and maximum levels defined per enchantment;
- exclusivity defined through registry sets where needed.

The replacement may instead use Minecraft's data-driven enchantment registry if the target version exposes all needed fields and effects. Event-driven behavior such as Soulbound still requires server-side logic even if the enchantment definition itself is data-driven.

## Grindstone behavior

When an enchanted tome is placed through grindstone processing and the result contains no enchantments, Vane converts it back to the matching normal tome rather than leaving an unenchanted enchanted-book custom item:

- Enchanted Ancient Tome → Ancient Tome;
- Enchanted Ancient Tome of Knowledge → Ancient Tome of Knowledge;
- Enchanted Ancient Tome of the Gods → Ancient Tome of the Gods.

This is a useful compatibility requirement because it preserves the underlying progression item after disenchanting.

## Replacement acceptance criteria

Required:

- three recognizable tome progression tiers;
- basic tomes obtainable through exploration loot;
- Knowledge and Gods tiers craftable from lower tiers using Vane-like recipes;
- custom-enchantment recipes output an enchanted carrier for the requested enchantment;
- Soulbound and Unbreakable recipes/loot integrate into this system;
- disenchanting a carrier should return the corresponding normal tome when no enchantments remain.

Preferred:

- reproduce Vane's loot-table coverage and probabilities;
- preserve old Vane custom items through conversion/migration;
- preserve resource-pack appearance or an equivalent visual design;
- allow individual recipes and loot injections to be configured or disabled independently.

## Source references

- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/items/Tomes.java`
- `vane-core/src/main/java/org/oddlama/vane/core/item/CustomItem.java`
- `vane-core/src/main/java/org/oddlama/vane/core/item/CustomItemHelper.java`
- `vane-core/src/main/java/org/oddlama/vane/core/LootTable.java`
- `vane-core/src/main/java/org/oddlama/vane/core/config/loot/LootDefinition.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/CustomEnchantmentRegistry.java`
- `vane-enchantments/src/main/resources/lang-en.yml`

---
type: concept
title: "Unbreakable"
summary: "Required Vane enchantment that permanently prevents durability loss."
tags: [vane, enchantment, unbreakable, required]
---

# Unbreakable

## Priority

**Required.** This behavior must be retained by the replacement.

## Registry properties

Vane registers `vane_enchantments:unbreakable` as:

- maximum level: **I**;
- rarity: rare;
- treasure enchantment;
- custom items allowed;
- supported items: Paper's `ENCHANTABLE_DURABILITY` item tag;
- active in any equipment slot;
- explicitly mutually exclusive with vanilla **Unbreaking** and **Mending**.

## Crafting recipe

Unbreakable consumes an Ancient Tome of the Gods and produces an Enchanted Ancient Tome of the Gods carrying Unbreakable.

```text
WAW
NBN
TST
```

where:

- `W` = Wither Rose;
- `A` = Enchanted Golden Apple;
- `N` = Netherite Ingot;
- `B` = Ancient Tome of the Gods;
- `T` = Totem of Undying;
- `S` = Nether Star.

## Loot

Vane injects an Unbreakable Enchanted Ancient Tome of the Gods into:

- Abandoned Mineshaft: **1/120** chance, amount one;
- Bastion Treasure: **1/30** chance, amount one.

## Durability behavior

Vane listens to `PlayerItemDamageEvent` at the lowest priority. When the damaged item carries Unbreakable, it:

1. sets the item's native `unbreakable` item-meta property to `true`;
2. hides the vanilla unbreakable tooltip flag;
3. sets the event damage to zero;
4. cancels the damage event.

The native unbreakable property is written lazily on the first attempted durability loss. Once set, Minecraft itself prevents subsequent durability processing, reducing repeated event work.

Observable behavior: an Unbreakable item does not lose durability through normal player item-damage events.

## Replacement acceptance criteria

Required:

- supported items must never lose durability while carrying Unbreakable;
- enchantment level is I;
- Unbreakable must not coexist with Mending or Unbreaking through normal supported enchanting/anvil mechanics;
- the enchantment must be obtainable through the Ancient Tome system using the Vane-like recipe.

Preferred:

- use the native item unbreakable component/property where possible rather than continuously repairing damage after the fact;
- keep the native unbreakable marker hidden so the custom enchantment remains the player-facing explanation;
- reproduce the Vane loot injections.

## Source references

- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/Unbreakable.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/registry/UnbreakableRegistry.java`

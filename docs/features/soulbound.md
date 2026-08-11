---
type: concept
title: "Soulbound"
summary: "Required Vane enchantment that preserves items on death and guards against accidental drops."
tags: [vane, enchantment, soulbound, required]
---

# Soulbound

## Priority

**Required.** This behavior must be retained by the replacement.

## Registry properties

Vane registers `vane_enchantments:soulbound` as:

- maximum level: **I**;
- rarity: rare;
- treasure enchantment;
- custom items allowed;
- supported items: Paper's `ENCHANTABLE_DURABILITY` item tag;
- active in any equipment slot;
- no explicit exclusivity list.

Its display formatting is dark gray rather than the default rare-enchantment gold used by Vane's common registry wrapper.

## Crafting recipe

Soulbound consumes an Ancient Tome of the Gods and produces an Enchanted Ancient Tome of the Gods carrying Soulbound.

```text
CQC
OBE
RGT
```

where:

- `C` = Chain (two positions);
- `Q` = Writable Book;
- `O` = Bone;
- `B` = Ancient Tome of the Gods;
- `E` = Ender Eye;
- `R` = an Enchanted Book with **Curse of Binding I**;
- `G` = Ghast Tear;
- `T` = Totem of Undying.

The Curse of Binding requirement is an exact enchantment ingredient constraint in Vane's recipe definition.

## Loot

A Soulbound Enchanted Ancient Tome of the Gods has an independent **1/15** chance to be added to Bastion Treasure loot, amount one.

## Death behavior

On `PlayerDeathEvent` at monitor priority, Vane scans the event's normal drop list. Every stack carrying Soulbound is:

1. added to Paper's `itemsToKeep` collection; and
2. removed from the normal death-drop list.

Therefore Soulbound items remain with the player after death independently of the rest of the inventory's normal drop behavior.

The replacement should preserve the actual item stack and metadata rather than recreating an approximation after respawn.

## Accidental-drop protection

Vane additionally prevents a single accidental Q/drop-key action from throwing a Soulbound item away.

The default confirmation window is **2,000 ms** and is stored on the item metadata using a persistent cooldown key.

The intended interaction is:

1. first drop attempt is blocked and the player sees an action-bar warning;
2. a subsequent explicit drop through the inventory UI can arm/confirm the drop within the configured window;
3. when the confirmation state permits it, the item is actually allowed to drop and Vane clears the temporary marker.

Vane's language strings describe this as:

- Soulbound items can only be dropped using the mouse;
- drop again to confirm;
- notification when a Soulbound item is successfully dropped.

### Full-inventory edge case

Minecraft can force an item to be dropped when closing a crafting/inventory interaction with no room available. If that item is Soulbound, Vane tries to protect it by finding the first non-Soulbound item in the player's inventory, placing the Soulbound stack into that slot, and dropping the non-Soulbound stack instead.

If every available inventory stack is Soulbound, Vane cannot prevent the forced drop and lets it proceed.

Soulbound items may still be intentionally stored in containers; the protection is specifically against item-drop behavior, not inventory transfer in general.

## Replacement acceptance criteria

Required:

- Soulbound level I must be applicable to durability-enchantable items;
- Soulbound items must remain with their owner on death;
- normal container/storage interactions must remain possible;
- the enchantment must be obtainable through the Ancient Tome system using the Vane-like recipe.

Strongly preferred:

- protect against accidental drop-key loss;
- retain a deliberate way to drop a Soulbound item using a confirmation interaction;
- handle full-inventory forced-drop situations without losing the Soulbound item whenever another stack can be displaced instead.

## Source references

- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/Soulbound.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/registry/SouldboundRegistry.java`
- `vane-core/src/main/java/org/oddlama/vane/core/data/CooldownData.java`
- `vane-enchantments/src/main/resources/lang-en.yml`

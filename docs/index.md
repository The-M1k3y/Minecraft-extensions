---
okf_version: "0.2"
---

# Minecraft Extensions Knowledge Base

This directory is an Open Knowledge Format (OKF) v0.2 knowledge bundle for the replacement of selected Vane functionality.

## Source baseline

Behavior documented here is derived from the Vane repository at commit `c5a79260950023cfddd640d86e68006331583fcb` (2026-06-28), unless a document says otherwise.

The goal is to describe observable behavior and data contracts independently of the eventual implementation. A replacement may use a data pack, resource pack, Paper plugin, or a combination of them, provided the required behavior is preserved closely enough for this server.

## Requirements and feature references

- [Scope and priorities](scope.md) - Selected replacement scope, priorities, and architecture boundaries.
- [Creeper protection](features/creeper-protection.md) - Protected explosions and Vane's optional staged world-rebuild behavior.
- [Ancient Tomes and enchantment pipeline](features/enchantment-system.md) - Tome tiers, loot, recipes, custom items, registry behavior, and grindstone conversion.
- [Soulbound](features/soulbound.md) - Required keep-on-death and guarded-drop enchantment behavior.
- [Unbreakable](features/unbreakable.md) - Required durability prevention and enchantment exclusivity behavior.
- [Other Vane enchantments](features/other-enchantments.md) - Lower-priority enchantment mechanics retained for future compatibility work.
- [Anvil repair-cost limiter](features/anvil-cost-limiter.md) - Removal of the normal anvil cost ceiling and configurable cost cap.

## Bundle history

- [Change log](log.md) - Chronological updates to this knowledge bundle.

## Documentation conventions

Requirements marked **required** are part of the selected replacement scope. Items marked **nice to have** are useful compatibility targets but may be omitted. Source notes describe Vane's behavior rather than prescribing a particular replacement technology.

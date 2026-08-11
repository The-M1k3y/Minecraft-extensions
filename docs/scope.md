---
type: concept
title: "Replacement Scope and Priorities"
summary: "Selected Vane behavior to preserve and the expected replacement boundaries."
tags: [vane, scope, requirements]
---

# Replacement Scope and Priorities

## Required behavior

The initial replacement must cover:

1. **Permission management** — only basic permission groups are required. Region management, claims, and similar features are out of scope; a dedicated permission plugin such as LuckPerms is expected to provide this capability rather than custom code in this repository.
2. **Creeper protection** — prevent permanent creeper damage to the world. Vane's optional staged world rebuild is the behavioral reference.
3. **Custom enchantment pipeline** — preserve the general Vane progression through Ancient Tomes, loot acquisition, crafting recipes, enchanted tome variants, and application of custom enchantments as closely as practical.
4. **Soulbound** — required custom enchantment.
5. **Unbreakable** — required custom enchantment.
6. **Anvil repair-cost limiter** — remove or cap the effective anvil cost limit similarly to Vane.

## Nice-to-have behavior

The remaining Vane custom enchantments are lower-priority compatibility targets. Their source behavior is summarized in [Other Vane enchantments](features/other-enchantments.md) so they can be implemented later without repeating source analysis.

## Architecture principle

Prefer the least invasive platform that can implement a feature correctly:

- **Data pack** for loot tables, recipes, tags, predicates, advancements/functions, and data-driven registry content where supported by the target Minecraft/Paper version.
- **Resource pack** for custom item presentation and client-visible names/models/textures.
- **Paper plugin** for event-driven mechanics, inventory/death handling, anvil APIs, registry bootstrap behavior that cannot be expressed in a data pack, or compatibility glue between components.

A single logical feature may span all three layers.

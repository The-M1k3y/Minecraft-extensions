---
type: concept
title: "Anvil Repair-Cost Limiter"
summary: "Vane behavior for removing the hard anvil cost ceiling and capping the charged repair cost."
tags: [vane, anvil, repair-cost, required]
---

# Anvil Repair-Cost Limiter

## Priority

**Required.** The replacement must allow anvil operations that vanilla would reject for excessive cost and should reproduce Vane's configured cost cap.

## Vane behavior

Vane's `RepairCostLimiter` handles `PrepareAnvilEvent` at `LOWEST` priority.

For every prepared anvil operation it:

1. sets the anvil view's maximum repair cost to `999999`;
2. reads the calculated repair cost;
3. if that cost exceeds the configured maximum, replaces it with the configured maximum.

The default configured maximum repair cost is **39 levels**.

The configuration description explicitly notes that setting the cap below 40 removes the normal "Too Expensive" restriction altogether. Costs above 40 remain technically craftable when configured that way even if the vanilla client can still display "Too Expensive" and may not display the actual required level count correctly.

## Replacement acceptance criteria

Required:

- otherwise-valid anvil combinations must not become impossible solely because vanilla's normal maximum-cost threshold is exceeded;
- default charged cost should be capped at **39 levels**;
- the cap should be configurable.

Preferred:

- do not alter recipe validity, enchantment compatibility, material requirements, or prior-work calculations except as necessary to remove/cap the final cost limit;
- preserve compatibility with custom enchantments and enchanted Ancient Tomes.

## Source reference

- `vane-trifles/src/main/java/org/oddlama/vane/trifles/RepairCostLimiter.java`

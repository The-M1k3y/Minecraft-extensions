---
type: concept
title: "Creeper Protection"
summary: "Vane hazard-protection behavior for creeper explosions and optional world rebuilding."
tags: [vane, creeper, explosion, world-rebuild]
---

# Creeper Protection

## Priority

**Required.** The replacement must prevent creeper explosions from causing permanent world damage.

## Vane behavior

Vane implements creeper protection inside `vane-admin`'s `HazardProtection` listener.

The relevant configuration defaults are:

- hazard protection enabled;
- creeper explosion protection enabled;
- an optional `world_rebuild` subsystem controls whether protected explosions are cancelled outright or allowed to visually destroy blocks and then rebuild them.

When a creeper produces an `EntityExplodeEvent`, Vane handles it at `HIGHEST` priority after previously cancelled events have been ignored.

### Without world rebuild

If creeper explosions are disabled and world rebuild is not enabled, Vane cancels the explosion event. This prevents the normal explosion from affecting blocks.

### With world rebuild

If world rebuild is enabled, Vane does not simply cancel the visual destruction. Instead it:

1. snapshots every block state from the explosion's affected-block list;
2. replaces those blocks with air without drops or physics;
3. clears the explosion event's block list so vanilla does not process those blocks again;
4. waits for the configured initial delay;
5. restores the saved block states one by one, without physics;
6. plays each restored block's placement sound.

The default rebuild timing is:

- initial delay: **2,000 ms**;
- minimum interval between restored blocks: **50 ms** (one server tick at normal tick rate);
- delay falloff: **0.175**.

For the `n`th restoration step the effective delay is approximately:

`max(min_delay, initial_delay × exp(-n × delay_falloff))`.

Blocks are ordered relative to a point above the horizontal center of the affected area. The implementation restores the blocks furthest from that top-center reference first, resulting in a deterministic-looking staged rebuild rather than arbitrary restoration.

If a block position is no longer air when Vane restores its saved state, the replacement block is broken naturally before the saved state is forced back into place.

Pending rebuilds are completed immediately when the module is disabled.

## Hanging entities

Vane separately cancels `HangingBreakByEntityEvent` when the remover is a protected creeper. This is important because protecting the block list alone does not guarantee paintings/item frames survive an explosion.

## Replacement acceptance criteria

At minimum:

- creeper explosions must not permanently remove or alter protected blocks;
- hanging entities should not be destroyed by protected creeper explosions;
- entity damage and player damage do **not** need to be suppressed merely because block damage is protected, unless separately configured by the replacement.

Preferred compatibility:

- preserve the visible explosion followed by delayed staged rebuilding;
- preserve block states, including stateful blocks, as reliably as practical;
- avoid duplicate block drops while simulating destruction;
- handle conflicting player/world edits during a pending rebuild predictably.

## Source references

- `vane-admin/src/main/java/org/oddlama/vane/admin/HazardProtection.java`
- `vane-admin/src/main/java/org/oddlama/vane/admin/WorldRebuild.java`

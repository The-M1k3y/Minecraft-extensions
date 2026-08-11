# Minecraft Extensions

Replacement components for selected Vane functionality on a PaperMC server.

## Repository layout

- `datapacks/` — server-side data packs for behavior that can be implemented with vanilla data-driven features.
- `resource-packs/` — client resource packs for custom item models, textures, names, and related assets.
- `plugins/` — Paper plugins for behavior that requires server APIs or event handling.
- `docs/` — an Open Knowledge Format (OKF) v0.2 knowledge bundle documenting source behavior, replacement requirements, and implementation decisions.

Each implementation should live in its own subdirectory below the appropriate top-level component directory. Cross-component behavior should be documented in `docs/` before implementation so the data pack, resource-pack, and plugin pieces share the same behavioral contract.

## Current scope

The initial documentation captures the Vane behavior selected for replacement, with emphasis on creeper protection, the Ancient Tome/custom-enchantment system, Soulbound, Unbreakable, and the anvil repair-cost limiter. Other Vane enchantments are documented as lower-priority reference behavior.

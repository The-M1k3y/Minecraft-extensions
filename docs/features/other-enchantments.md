---
type: concept
title: "Other Vane Enchantments"
description: "Reference behavior for lower-priority Vane enchantments that may be replicated later."
tags: [vane, enchantments, optional]
---

# Other Vane Enchantments

These enchantments are **nice to have** rather than required for the initial replacement. The summaries below preserve the source behavior needed for later implementation planning.

## Angel

- Key: `vane_enchantments:angel`
- Maximum level: V
- Rarity: very rare
- Treasure enchantment
- Supported item: Elytra
- Exclusive with Wings
- Recipe tier: Ancient Tome of the Gods
- Default configured flying speeds by level: `0.7`, `1.1`, `1.4`, `1.7`, `2.0` (Vane describes these as blocks per second)
- Default acceleration factor: `0.1`

While the player is sneaking and gliding with Angel on the chest item, Vane continuously accelerates the player toward their look direction using an exponential moving-average style velocity adjustment. The contribution is reduced when the current velocity points away from the look direction. Firework particles are spawned behind the player.

The crafting recipe uses Phantom Membranes, Dragon's Breath, Pufferfish Buckets, a Firework Rocket, and an Ancient Tome of the Gods. It can also appear as an enchanted Gods tome in several exploration loot tables at 1/250.

## Grappling Hook

- Key: `vane_enchantments:grappling_hook`
- Maximum level: III
- Rarity: uncommon
- Treasure enchantment
- Supported item: Fishing Rod
- Recipe tier: Ancient Tome of Knowledge
- Default ideal grapple distance: 16 blocks
- Strength by level: `1.6`, `2.1`, `2.7`

When reeling a fishing hook that is anchored in a block, Vane adds velocity toward the hook. The pull is strongest around the configured ideal distance, fall distance is reset, and a small upward velocity component is always added. If the hook is below the player, the downward pull is suppressed so the player does not simply scrape along the ground.

The recipe is a vertical Tripwire Hook, Lead, and Ancient Tome of Knowledge.

## Hell Bent

- Key: `vane_enchantments:hell_bent`
- Maximum level: I
- Rarity: common
- Treasure enchantment
- Supported items: helmets
- Recipe tier: Ancient Tome of Knowledge

If a player wearing a Hell Bent helmet takes `FLY_INTO_WALL` damage while gliding, Vane cancels that damage entirely.

The recipe is Music Disc Pigstep above an Ancient Tome of Knowledge above a Turtle Helmet. Enchanted Knowledge tomes can also appear in Bastion loot at 1/50.

## Leafchopper

- Key: `vane_enchantments:leafchopper`
- Maximum level: I
- Rarity: common
- Treasure enchantment
- Supported items: tools
- Recipe tier: Ancient Tome of Knowledge

Left-clicking non-persistent leaf blocks with a Leafchopper tool breaks the leaves immediately and naturally, without additional durability cost from the custom action. Persistent/player-placed leaves are ignored.

The recipe surrounds an Ancient Tome of Knowledge with four Shears in a cross pattern.

## Lightning

- Key: `vane_enchantments:lightning`
- Maximum level: I
- Rarity: rare
- Treasure enchantment
- Supported items: weapons
- **Disabled by default in Vane**
- Recipe tier: Ancient Tome of Knowledge

During rain or thunderstorms, attacking an entity outdoors with a Lightning weapon causes an actual lightning strike at the target and adds a configurable amount of direct damage; the default bonus is 4 damage points. A configuration option can restrict activation to thunderstorms only.

When lightning-protection mode is enabled, a player holding a Lightning weapon is immune to lightning damage.

The recipe uses Lightning Rods, Totems of Undying, a Beacon, and an Ancient Tome of Knowledge.

## Rake

- Key: `vane_enchantments:rake`
- Maximum level: IV
- Rarity: common
- Treasure enchantment
- Supported items: tools
- Recipe tier: Ancient Tome of Knowledge

When a player right-clicks existing farmland with a Rake-enchanted tool, Vane finds an additional tillable block within the level-dependent search behavior and tills it. Each extra tilling action consumes one durability point and swings the player's arm.

The recipe surrounds an Ancient Tome of Knowledge with four Golden Hoes in a cross pattern.

## Seeding

- Key: `vane_enchantments:seeding`
- Maximum level: IV
- Rarity: common
- Treasure enchantment
- Supported items: tools
- Recipe tier: Ancient Tome of Knowledge

Right-clicking a supported planted crop with a Seeding tool causes Vane to find another suitable farmland position within the level-dependent search behavior and plant the same crop there, provided the player has the required seed/item. Each successful extra planting consumes one durability point and swings the player's arm.

The recipe places Pumpkin Seeds, Carrot, Wheat Seeds, Nether Wart, Beetroot Seeds, Potato, and Melon Seeds around an Ancient Tome of Knowledge.

## Takeoff

- Key: `vane_enchantments:take_off`
- Maximum level: III
- Rarity: uncommon
- Treasure enchantment
- Supported item: Elytra
- Recipe tier: Ancient Tome of the Gods
- Boost strength by level: `0.2`, `0.4`, `0.6`

When a player begins Elytra gliding and is **not** sneaking, Vane immediately applies a level-dependent boost. The Elytra takes a small random durability cost of 1–2 points and firework particles are spawned.

The recipe uses Phantom Membranes, Pistons, a Slime Block, and an Ancient Tome of the Gods. Enchanted Gods tomes with Takeoff also appear in a broad set of exploration loot tables at 1/150.

## Wings

- Key: `vane_enchantments:wings`
- Maximum level: IV
- Rarity: rare
- Treasure enchantment
- Supported item: Elytra
- Recipe tier: Ancient Tome of Knowledge
- Boost cooldowns by level: 7,000 ms; 5,000 ms; 3,500 ms; 2,800 ms
- Boost strengths by level: `0.4`, `0.47`, `0.54`, `0.6`

While gliding, beginning to sneak triggers a level-dependent Elytra boost if the Elytra cooldown has expired. Vane applies the configured cooldown to the Elytra, damages it by a small random amount of 1–2 durability points, and emits firework particles.

The recipe uses Phantom Membranes, Dispensers, Firework Rockets, and an Ancient Tome of Knowledge. Enchanted Knowledge tomes with Wings appear in several exploration loot tables at 1/110 and in Bastion Treasure at 1/10.

## Notes for future replication

Most of these mechanics require Paper event handling even if the enchantment definitions, recipes, and loot distribution can be data-driven. The likely split is:

- data pack: enchantment definitions where supported, recipes, loot-table modifications;
- resource pack: names and optional visual assets;
- Paper plugin: movement, damage, farming, interaction, durability, and cooldown behavior.

## Source references

- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/Angel.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/GrapplingHook.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/HellBent.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/Leafchopper.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/Lightning.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/Rake.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/Seeding.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/TakeOff.java`
- `vane-enchantments/src/main/java/org/oddlama/vane/enchantments/enchantments/Wings.java`
- corresponding registry classes in `vane-enchantments/.../enchantments/registry/`

---
okf_version: "0.2"
title: "Minecraft Extensions Knowledge Base"
summary: "Behavioral reference and replacement requirements for selected Vane features."
---

# Minecraft Extensions Knowledge Base

This directory is an Open Knowledge Format (OKF) v0.2 knowledge bundle for the replacement of selected Vane functionality.

## Source baseline

Behavior documented here is derived from the Vane repository at commit `c5a79260950023cfddd640d86e68006331583fcb` (2026-06-28), unless a document says otherwise.

The goal is to describe observable behavior and data contracts independently of the eventual implementation. A replacement may use a data pack, resource pack, Paper plugin, or a combination of them, provided the required behavior is preserved closely enough for this server.

## Contents

- [Scope and priorities](scope.md)
- [Creeper protection](features/creeper-protection.md)
- [Ancient Tomes and enchantment pipeline](features/enchantment-system.md)
- [Soulbound](features/soulbound.md)
- [Unbreakable](features/unbreakable.md)
- [Other Vane enchantments](features/other-enchantments.md)
- [Anvil repair-cost limiter](features/anvil-cost-limiter.md)
- [Change log](log.md)

## Documentation conventions

Requirements marked **required** are part of the selected replacement scope. Items marked **nice to have** are useful compatibility targets but may be omitted. Source notes describe Vane's behavior rather than prescribing a particular replacement technology.

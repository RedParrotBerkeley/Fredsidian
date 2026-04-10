# Fredsidian Privacy Model

## Principle

Memory access should be scoped by context, not assumed globally safe.

## Access Tiers

### Tier 1: Assistant Operational Memory
High-trust internal memory used for continuity.

### Tier 2: Scoped Obsidian Folders
Allowed for assistant consultation when relevant.

### Tier 3: Sensitive/Private Vault Areas
Excluded by default unless explicitly authorized.

## Shared Context Rule

Shared or group contexts should not automatically expose:
- personal history
- private notes
- internal paths
- sensitive operational details

## Default Safe Behavior

- retrieve less before retrieving more
- summarize rather than dump
- prefer abstractions over raw sensitive text
- require explicit permission for broad private-note access

## Secret Handling

Secrets should not be stored in standard notes unless absolutely necessary.
If exposed:
- rotate
- invalidate
- audit
- document

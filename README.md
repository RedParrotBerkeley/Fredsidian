# Fredsidian

**Fredsidian** is a memory architecture for AI assistants that combines a **trusted operational memory core** with a broader **Obsidian-style markdown knowledge graph**.

The idea is simple: an assistant should not have to choose between brittle chat history and an unbounded note vault.

Fredsidian separates the two jobs:
- a small, explicit memory layer for operational truth
- a larger linked markdown graph for projects, research, decisions, and long-term context

That makes it useful for builders working on:
- AI personal assistants
- local-first memory systems
- markdown-based agent memory
- retrieval systems for long-running assistants
- Obsidian-integrated agent workflows

## Why this exists

Most assistant memory approaches collapse very different needs into one bucket.

That creates predictable problems:
- important operating rules get buried in noisy context
- long-term notes are treated as equally trustworthy as hard operational facts
- assistants lose continuity or become overconfident
- personal knowledge vaults get mixed with assistant state too early and too broadly

Fredsidian is an attempt to solve that cleanly.

Instead of treating memory as one flat store, it treats assistant memory as **two different systems with different trust levels and retrieval rules**.

## Core idea

Fredsidian uses a **two-tier memory model**.

### 1. Core operational memory
This is the high-trust layer.

Use it for:
- assistant operating rules
- durable user preferences
- important recurring tasks
- safety boundaries
- short curated memory
- daily operational logs

Examples:
- `MEMORY.md`
- `memory/YYYY-MM-DD.md`

This layer should stay:
- small
- explicit
- durable
- easy to audit

### 2. Obsidian-style graph memory
This is the broader context layer.

Use it for:
- project notes
- research
- decision records
- people and entity notes
- linked plans
- long-form context
- reusable references

This layer should be:
- rich
- linked
- searchable
- scoped
- retrieval-aware

## Design principles

- operational truth should stay small and trusted
- broader context should be rich, linked, and markdown-native
- retrieval should be scoped, evidence-based, and privacy-aware
- assistant memory and PKM are related, but not identical
- read-mostly is the safest starting point
- write-back should be explicit, not magical

## Retrieval model

When an assistant needs context, Fredsidian recommends this order:

1. Check core memory first for operational truth
2. Check graph memory second for broader context
3. Separate:
   - facts
   - hypotheses
   - next checks
4. return the smallest useful synthesis, ideally with source references

This prevents broad personal context from overriding explicit assistant instructions or durable operating facts.

## Write policy

### Core memory writes
Appropriate for:
- explicit “remember this” requests
- stable preferences
- operationally important facts
- daily logs

### Graph memory writes
Appropriate for:
- research notes
- project summaries
- planning docs
- decision logs
- structured references
- reusable knowledge artifacts

### Guardrails
- do not silently rewrite large parts of a vault
- do not assume all notes are equally trusted
- do not expose private vault content in shared contexts
- require approval before broad or high-impact write-back

## Recommended v1 scope

Fredsidian v1 should be:
- read-mostly
- local-first
- markdown-native
- explicit about privacy boundaries
- useful without requiring vector databases or plugin sprawl

Fredsidian v1 should **not** try to:
- replace all assistant memory
- auto-ingest an entire vault without boundaries
- silently rewrite knowledge systems
- pretend broad recall is the same thing as trusted operational continuity

## Project structure

```text
fredsidian/
  README.md
  docs/
    architecture.md
    note-schema.md
    retrieval-policy.md
    privacy-model.md
    roadmap.md
  examples/
    vault-structure.md
    sample-notes/
      project-note.md
      person-note.md
      decision-note.md
      research-note.md
      daily-note.md
```

## Who this is for

Fredsidian is aimed at people building assistants that need to operate over time without turning memory into a blob.

Especially if you care about:
- trust boundaries
- long-term continuity
- local-first systems
- markdown-native workflows
- Obsidian-compatible knowledge graphs
- operational reliability over flashy demos

## Status

Fredsidian is currently a **design/spec project**, not a packaged implementation release.

That is intentional.

The goal right now is to make the architecture sharp enough that implementation choices later stay clean.

## Keywords

Relevant discovery terms this project addresses:
- Obsidian memory for AI
- Obsidian-style assistant memory
- markdown memory for agents
- local-first AI memory
- AI assistant memory architecture
- knowledge graph memory for assistants
- second-brain workflows for AI systems


## Portfolio snapshot

- **Problem:** Assistant memory systems often blend high-trust operational rules with noisy long-form notes.
- **Core capability:** Two-tier memory architecture separating trusted operational memory from markdown graph context.
- **Primary stack:** Markdown-first architecture with AI assistant memory patterns.
- **Status:** Active design and implementation exploration.


## Related projects

- [agent-black-box](https://github.com/mikepatraw/agent-black-box) — run replay, diff, and incident tooling for agents.\n- [rx-guard](https://github.com/mikepatraw/rx-guard) — healthcare-focused agent workflow project.\n- [WatchClaw](https://github.com/mikepatraw/WatchClaw) — security-minded OpenClaw scanner.

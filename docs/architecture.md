# Fredsidian Architecture

## Purpose

Fredsidian is a hybrid assistant memory architecture that combines:
- small, trusted assistant operational memory
- larger, linked Obsidian knowledge memory

The architecture is designed to improve recall, continuity, and project context without collapsing all memory concerns into one system.

## Architectural Goals

- preserve a trusted assistant memory core
- use Obsidian as a linked second brain
- support gradual adoption
- separate operational truth from broader knowledge context
- minimize privacy leakage and uncontrolled writes
- keep the system inspectable and human-readable

## Memory Layers

### Layer A: Operational Memory

Operational memory stores assistant-critical continuity.

Examples:
- user preferences
- agent behavior rules
- recurring instructions
- messaging constraints
- important short durable facts
- daily event logs

Properties:
- low volume
- high trust
- highly curated
- should be safe to consult first

### Layer B: Knowledge Graph Memory

Knowledge graph memory stores broader context that benefits from linking and long-term accumulation.

Examples:
- projects
- meeting notes
- decision history
- research notes
- people and organization pages
- plans and frameworks
- reference material

Properties:
- higher volume
- linked structure
- more exploratory retrieval
- not every note is equally trustworthy or current

## Retrieval Flow

1. Query operational memory first
2. If insufficient, search relevant Obsidian folders
3. Retrieve matching notes/pages
4. Separate retrieved content into:
   - verified facts
   - contextual references
   - hypotheses or stale material
5. Return a concise synthesis
6. Cite source files when useful

## Write Flow

### Writes to operational memory
Best for:
- explicit remember-this requests
- high-confidence user preferences
- assistant behavior constraints
- notable events from the day

### Writes to Obsidian
Best for:
- project pages
- decision logs
- long-form research summaries
- reusable references
- structured drafts

## Trust Model

Not all memory is equally trusted.

### Highest trust
- assistant rules and curated operational memory
- recent verified logs

### Medium trust
- maintained project notes
- structured decision records

### Lower trust until verified
- old research notes
- brainstorm pages
- stale meeting notes
- speculative notes without timestamps or provenance

## Privacy Model

Fredsidian should support scoped access.

Recommended scopes:
- always-readable assistant folders
- optional project folders
- private folders excluded by default
- shared-context restrictions so personal memory is not surfaced in group contexts

## Modes of Adoption

### V1
- read-mostly
- filesystem-based
- scoped folders
- no full-vault automatic writes

### V2
- optional write-back to assistant-specific Obsidian folders
- templates for consistent note creation

### V3
- structured local API integration
- semantic indexing / ranking
- stronger provenance and retrieval metadata

## Failure Modes to Avoid

- replacing all assistant memory too early
- broad uncontrolled note editing
- leaking private vault content into shared spaces
- treating every old note as current truth
- building a graph without note discipline

## Design Summary

Fredsidian works best when:
- core assistant memory stays small and trusted
- Obsidian becomes the linked second brain
- retrieval is scoped and evidence-aware
- writing remains deliberate and reviewable

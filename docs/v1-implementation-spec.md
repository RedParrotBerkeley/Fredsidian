# Fredsidian V1 Implementation Spec

## Objective

Ship a minimal, credible, buildable V1 of Fredsidian.

V1 should prove that a hybrid assistant memory system can:
- preserve a trusted operational memory core
- consult an Obsidian-style markdown knowledge graph
- retrieve relevant context safely
- support future growth without forcing premature complexity

V1 is a **read-mostly architecture**.

## Non-Goals

V1 does **not** attempt to:
- replace all assistant memory with Obsidian
- edit the entire vault autonomously
- require embeddings or a vector database
- depend on a plugin-heavy Obsidian stack
- promise perfect semantic retrieval

## User Story

A user has:
- an AI assistant with its own operational memory
- an Obsidian vault containing projects, research, people, and decisions

They want the assistant to:
- remember assistant-specific operational facts reliably
- consult relevant Obsidian notes when more context is needed
- avoid mixing private vault content into the wrong context
- return concise, trustworthy syntheses rather than raw note dumps

## V1 System Components

### 1. Operational Memory Store
A small trusted memory layer for assistant continuity.

Inputs:
- curated long-term assistant memory
- daily assistant logs
- explicit remember-this events

Responsibilities:
- hold assistant behavior rules
- hold user preferences and durable assistant facts
- provide first-pass retrieval for operational truth

### 2. Obsidian Vault Reader
A scoped markdown file reader over selected vault folders.

Inputs:
- configured folder allowlist
- user query

Responsibilities:
- discover relevant notes
- read note contents
- expose metadata such as path, title, dates, and note type when present

### 3. Retrieval Orchestrator
A deterministic retrieval controller.

Responsibilities:
- query operational memory first
- decide when Obsidian context is needed
- search allowed folders only
- rank results using simple transparent heuristics
- assemble a minimal context pack

### 4. Synthesis Layer
Builds the final answer from retrieved memory.

Responsibilities:
- separate verified facts from inferred context
- summarize rather than dump
- cite file paths or note sources when useful
- state uncertainty clearly

### 5. Optional Writeback Hooks (Limited)
V1 allows only narrow writeback patterns, ideally off by default.

Allowed writeback targets:
- assistant daily log
- assistant-specific draft folders
- explicitly approved structured notes

## Folder Scope Model

V1 requires explicit folder allowlisting.

### Recommended default allowed folders
- `Assistant/`
- `Projects/`
- `People/`
- `Decisions/`
- `Research/`
- `Reference/`
- `Daily/`

### Recommended default blocked folders
- personal/private journals
- finance folders
- credentials or secrets folders
- archival dump folders with poor signal

## Retrieval Flow

### Step 1: Operational Memory Check
Search assistant memory for:
- explicit preferences
- instructions
- recent durable facts
- assistant-specific continuity

### Step 2: Obsidian Scope Decision
If operational memory is insufficient, determine whether the question likely needs:
- project context
- older decisions
- linked research
- people or relationship context

If yes, search Obsidian allowlisted folders.

### Step 3: Note Search
V1 search should be simple and inspectable.

Recommended heuristic ranking:
1. exact title/path matches
2. frontmatter type matches
3. recent updates/dates
4. frequency of query term matches
5. presence of linked entities

### Step 4: Context Pack Assembly
Build a small context bundle with:
- note title
- file path
- top summary lines or relevant sections
- date/update metadata when available
- confidence notes

### Step 5: Synthesis
Return:
- verified facts
- likely relevant context
- next checks if needed

## Output Contract

When Fredsidian retrieval is used, final responses should prefer:
- concise synthesis
- small bullets
- source citations when the information matters
- explicit uncertainty language when relevant

Suggested structure:
- Answer
- Relevant context
- Risks / uncertainty
- Next check

## Note Parsing Rules

V1 should support plain markdown first.

### Must support
- headings
- paragraphs
- bullet lists
- wiki-links
- YAML frontmatter when present

### Nice to support, but not required for v1
- backlinks graph analysis
- embedded blocks
- canvas files
- advanced plugin metadata

## Minimal Frontmatter Convention

V1 should recognize these fields when present:
- `type`
- `date`
- `updated`
- `status`
- `tags`

But frontmatter should not be mandatory for all notes.

## Note Type Handling

If `type` exists, V1 should recognize at least:
- `project`
- `person`
- `decision`
- `research`
- `daily`
- `draft`

## Trust Model

Not all retrieved notes are equally trustworthy.

### Highest trust
- assistant memory
- structured decision notes
- updated project notes

### Medium trust
- structured research notes
- recent daily notes

### Lower trust
- old brainstorms
- undated scratch notes
- stale or conflicting pages

The synthesizer must not present lower-trust material as verified fact without labeling it.

## Privacy and Context Controls

### Main/private session behavior
May retrieve from approved private folders when relevant.

### Shared/group session behavior
Must not automatically retrieve broad private memory.
Should only retrieve explicitly relevant, scoped, non-sensitive context.

### Hard rules
- never expose secrets from notes
- never dump raw private note text in shared contexts
- never assume whole-vault access is acceptable

## Writeback Policy

V1 is read-mostly.

### Allowed by default
- assistant daily operational logs
- local drafts created for review

### Allowed only with explicit approval
- creating or updating project notes
- decision logs
- structured research summaries in the vault

### Not allowed by default
- broad note rewrites
- deleting or renaming vault structures
- bulk metadata modification

## Recommended Repository Layout for V1 Build

```text
fredsidian/
  README.md
  docs/
    architecture.md
    note-schema.md
    retrieval-policy.md
    privacy-model.md
    roadmap.md
    v1-implementation-spec.md
  examples/
    vault-structure.md
    sample-notes/
  src/
    fredsidian/
      config.py
      models.py
      memory_core.py
      vault_reader.py
      search.py
      retrieval.py
      synthesize.py
      policies.py
```

## Suggested Internal Module Responsibilities

### `config.py`
- folder allowlists
- blocked paths
- mode flags

### `models.py`
- note metadata model
- retrieval result model
- memory item model

### `memory_core.py`
- operational memory loading
- daily memory loading
- core memory lookup

### `vault_reader.py`
- markdown file enumeration
- frontmatter parsing
- content extraction

### `search.py`
- lexical matching
- path/title matching
- recency scoring

### `retrieval.py`
- orchestration logic
- context pack assembly

### `synthesize.py`
- response shaping
- fact/context/uncertainty separation

### `policies.py`
- shared-context restrictions
- writeback rules
- privacy filters

## Acceptance Criteria for V1

Fredsidian V1 is successful if it can:

1. retrieve assistant operational memory reliably
2. search a scoped Obsidian folder set
3. recognize core note types when present
4. return concise, source-aware summaries
5. avoid leaking private note content in shared contexts
6. operate without embeddings or external APIs
7. remain understandable enough for another builder to implement quickly

## Suggested Build Order

1. implement note and config models
2. implement operational memory loader
3. implement vault reader
4. implement simple search and ranking
5. implement retrieval orchestration
6. implement synthesis contract
7. implement privacy/context policy filters
8. add limited optional writeback hooks last

## Risks

- weak note quality reduces retrieval quality
- over-scoped vault access increases privacy risk
- trying to mimic full semantic search too early adds complexity without enough value
- users may expect “Obsidian graph magic” before retrieval discipline exists

## Design Decision Summary

Fredsidian V1 should feel:
- small
- clear
- safe
- buildable
- useful

It should prove the architecture, not pretend the hardest parts are already solved.

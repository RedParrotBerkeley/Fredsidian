# Fredsidian Note Schema

## Philosophy

The note schema should support:
- fast retrieval
- clear ownership of facts
- easy linking
- low-friction writing
- human readability without special tooling

Markdown first. Frontmatter where useful, not everywhere just because we can.

## Core Note Types

### 1. Project Note

Purpose:
- hold the current state of a project
- summarize goals, status, risks, and next actions

Suggested path:
- `Projects/<project-name>.md`

Suggested fields:
```yaml
---
type: project
status: active
owner: Mike
updated: 2026-04-09
tags:
  - project
  - active
---
```

Suggested sections:
- Summary
- Current status
- Goals
- Open questions
- Risks
- Next actions
- Related notes

### 2. Person Note

Purpose:
- preserve useful context about a person, collaborator, client, or entity

Suggested path:
- `People/<name>.md`

Suggested fields:
```yaml
---
type: person
updated: 2026-04-09
tags:
  - person
---
```

Suggested sections:
- Who they are
- Relationship/context
- Important preferences
- Active threads
- Related projects

### 3. Decision Note

Purpose:
- record a meaningful decision with rationale and tradeoffs

Suggested path:
- `Decisions/YYYY-MM-DD-<decision-name>.md`

Suggested fields:
```yaml
---
type: decision
date: 2026-04-09
status: accepted
tags:
  - decision
---
```

Suggested sections:
- Decision
- Context
- Alternatives considered
- Why this was chosen
- Risks
- Follow-up checks

### 4. Research Note

Purpose:
- store synthesis from research work
- preserve sources and confidence

Suggested path:
- `Research/<topic>.md`

Suggested fields:
```yaml
---
type: research
updated: 2026-04-09
tags:
  - research
---
```

Suggested sections:
- Question
- Summary
- Key findings
- Source notes
- Confidence / caveats
- Next checks

### 5. Daily Note

Purpose:
- log the day’s events, decisions, and open loops

Suggested path:
- `Daily/YYYY-MM-DD.md`

Suggested fields:
```yaml
---
type: daily
date: 2026-04-09
tags:
  - daily
---
```

Suggested sections:
- What happened
- Important decisions
- Follow-ups
- Linked projects
- Linked people

### 6. Assistant Draft Note

Purpose:
- store assistant-prepared drafts for later review

Suggested path:
- `Assistant/Drafts/<draft-name>.md`

Suggested fields:
```yaml
---
type: draft
status: draft
updated: 2026-04-09
tags:
  - assistant
  - draft
---
```

Suggested sections:
- Purpose
- Draft
- Notes
- Approval status

## Linking Rules

Use explicit wiki-links where possible:
- `[[Project Name]]`
- `[[Person Name]]`
- `[[2026-04-09-project-decision]]`

Best practices:
- link people to projects
- link decisions to projects
- link daily notes to both
- link research to the decision or project it informs

## Minimal Required Metadata

Required for most durable notes:
- `type`
- `updated` or `date`

Optional metadata should stay optional unless retrieval quality proves otherwise.

## Naming Conventions

- stable names for project and person pages
- dated names for decisions and daily notes
- concise, readable titles
- avoid clever naming that hurts retrieval

## Retrieval Hints

Notes become easier to retrieve when they contain:
- one-line summary near the top
- explicit current status
- timestamps
- related links
- clearly labeled open questions

## Anti-Patterns

Avoid:
- giant undifferentiated notes
- missing dates on time-sensitive material
- storing all thoughts in daily notes only
- weak titles like `ideas.md` or `stuff.md`
- mixing facts, guesses, and decisions without labels

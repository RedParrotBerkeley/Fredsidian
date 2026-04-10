# Fredsidian Retrieval Policy

## Goal

Retrieve the smallest trustworthy set of context that materially improves the answer.

## Retrieval Order

1. Core assistant memory
2. Relevant Obsidian scoped folders
3. Specific linked notes
4. Daily logs only if needed for chronology

## Retrieval Rules

- prefer recent, maintained notes
- prefer structured notes over raw dumps
- prefer project/decision notes over old brainstorms
- distinguish fact from hypothesis
- do not surface private context in shared channels

## Response Rules

When retrieved content matters, present:
- what is verified
- what is inferred
- what should be checked next

## Citation Preference

When useful, cite:
- file path
- section title
- date

## Writeback Trigger Rules

Write back only when one of these is true:
- user explicitly asked to remember something
- a durable decision was made
- a project state materially changed
- a summary was created that will be useful later

## Shared Context Restrictions

In shared/group contexts:
- do not load broad personal long-term memory by default
- only retrieve scoped notes relevant to the request
- do not disclose private paths, secrets, or sensitive context

# CLAUDE.md — nucu-docs LLM Wiki

This repository is the knowledge base for **Makoto-kun**, the AI teaching
assistant for the NUCU program (Nagoya University × CU Boulder). It follows
the LLM Wiki pattern: humans curate sources, the LLM (you) compiles and
maintains the wiki. Wiki pages are embedded into a pgvector store and served
to students through a Discord RAG bot, so every page you write is also a
retrieval document. Write accordingly (see "Writing for retrieval" below).

## Directory structure

```
mk3/                   ← repo root
├── CLAUDE.md          ← this file (schema; humans edit, you follow)
├── raw/               ← immutable source material (you READ, never edit)
│   ├── curriculum/    ← lesson plans, teaching material
│   ├── automation/    ← n8n, RAG, AI-automation reference material
│   └── program/       ← NUCU program info, logistics, policies
└── wiki/              ← compiled knowledge (you OWN this directory)
    ├── concepts/      ← one page per concept (e.g. rag.md, embeddings.md)
    ├── entities/      ← tools, orgs, people (e.g. n8n.md, railway.md)
    ├── sources/       ← one summary page per raw source
    ├── index.md       ← global table of contents
    └── log.md         ← append-only operation log
```

## Layer rules

1. **raw/ is immutable.** Never edit, rename, move, or delete anything under
   `raw/`. Not even typos. If a source seems wrong, note the issue on its
   `wiki/sources/` page instead.
2. **wiki/ is yours.** Create, update, merge, and split pages freely. Humans
   rarely edit this directory; assume every page was written by you and can
   be rewritten by you.
3. **CLAUDE.md is human-owned.** Propose changes in conversation; do not edit
   this file unless explicitly asked.

## Page format

Every wiki page starts with YAML frontmatter:

```yaml
---
type: concept          # concept | entity | source | index
title: Vector embeddings
sources:
  - raw/automation/2026-05-12-embeddings-intro.txt
  - raw/automation/2026-06-02-openai-embeddings.txt
updated: 2026-07-06
tags: [rag, curriculum-module-2]
---
```

- `type` and `sources` are mandatory. `sources` lists every raw file that
  informed the page — this is how the downstream bot attributes answers.
- Update `updated` on every meaningful edit.
- File names: lowercase, hyphenated, no dates for concept/entity pages
  (`vector-embeddings.md`), dated for source pages
  (`2026-05-12-embeddings-intro.md`).

## Writing for retrieval

Wiki pages are chunked and embedded, then retrieved in isolation. Therefore:

- **Self-contained pages.** Each page must make sense without following any
  links. Define terms briefly on first use, even if another page covers them.
- **Length target: 300–800 words.** Longer than that, split into linked pages.
  Shorter than ~100 words, merge into a related page.
- **Front-load the summary.** First paragraph = a 2–3 sentence answer to
  "what is this and why does it matter?" This paragraph does the heaviest
  lifting in retrieval.
- **Plain, clear English.** The audience is NUCU students, many of whom are
  non-native English speakers. Short sentences. Concrete examples over
  abstractions. Expand acronyms on first use.
- **Cross-reference with wikilinks** (`[[vector-embeddings]]`) so the wiki is
  browsable in Obsidian, but never rely on a link to carry essential meaning.

## Workflows

### Ingest (default operation)

Trigger phrase: "New files have been added to raw/, ingest them."

1. Diff `raw/` against the `sources` frontmatter across `wiki/` (or against
   `log.md`) to find unprocessed files.
2. For each new source:
   a. Read it fully.
   b. Create its `wiki/sources/` summary page (key claims, context, why it
      was added).
   c. Create or update the relevant `wiki/concepts/` and `wiki/entities/`
      pages. Prefer updating an existing page over creating a near-duplicate.
   d. Add cross-links in both directions.
   e. If the new source contradicts an existing page, keep both claims on the
      page under a "Conflicting information" note — do not silently overwrite.
3. Update `index.md` (grouped by type, alphabetical within groups).
4. Append one line per source to `log.md`:
   `2026-07-06 ingested raw/automation/foo.txt → updated [[rag]], [[n8n]]`

### Query

Trigger phrase: "Based on the wiki, ..." — answer from `wiki/` pages only,
citing page names. If the wiki cannot answer, say so and suggest which kind
of source would fill the gap. Do not answer from general knowledge without
flagging that you are doing so.

### Lint

Trigger phrase: "Run a lint pass."

Check and fix: broken wikilinks, pages missing from `index.md`, `sources`
entries pointing at nonexistent raw files, concepts mentioned on 3+ pages
that lack their own page, pages over 800 words (propose splits), stale
`updated` dates on pages you modify. Report contradictions; do not resolve
them without asking.

## Conventions that downstream systems depend on

The n8n workflow "Wiki to Vector Store Loader" ingests `wiki/**/*.md` from
this repo into Postgres/pgvector and stores each file's repo path as
`source` metadata.
Because of that:

- Never place non-knowledge files (scratch notes, TODOs) under `wiki/` —
  everything there gets embedded. `log.md` and `index.md` are the two
  exceptions the loader may skip; keep their names stable.
- Renaming a wiki file changes its retrieval identity. Prefer editing in
  place; when a rename is truly needed, note it in `log.md`.
- Frontmatter is embedded along with the body, which is fine — but keep it
  minimal so it doesn't dilute the page's semantic content.

## Tone

You are maintaining teaching material. Accuracy over completeness, clarity
over cleverness. When uncertain, say so on the page rather than guessing.

# nucu-docs

This repo is the knowledge base behind **Makoto-kun 3.0**, the AI teaching
assistant for the NUCU program (Nagoya University × CU Boulder). If you're a
student in the program, everything Makoto-kun knows when it answers your
questions on Discord — about lectures, the trip itinerary, program policies,
site visits, and more — comes from the files in here.

## How it works: three layers

```
raw/  →  Claude Code (compile step)  →  wiki/  →  Discord bot
```

1. **`raw/`** — the source material. Lecture transcripts, program guides,
   itineraries: whatever gets added here is treated as ground truth and is
   never edited or cleaned up in place.
2. **Claude Code (the compile step)** — an AI agent (that's this tool) reads
   new files in `raw/` and turns them into wiki pages: one summary page per
   source, plus concept/entity pages that pull related ideas together and
   link to each other. This is the "compiling" step — raw material in,
   structured knowledge out.
3. **`wiki/`** — the compiled knowledge base. Short, self-contained Markdown
   pages, organized as concepts (ideas like RAG or the Meiji Restoration),
   entities (people, places, organizations like Nagoya University or
   Station Ai), and sources (one page per raw file). This is what actually
   answers your questions.

## From wiki to Discord

The `wiki/` pages don't answer questions by themselves — they need to get
into a place Makoto-kun can search. That happens through an n8n workflow
called **"Wiki to Vector Store Loader"**:

1. The workflow reads every `wiki/**/*.md` file in this repo.
2. Each page is split into chunks and converted into an **embedding** — a
   numeric vector that captures its meaning — using a process called
   Retrieval-Augmented Generation (RAG). See [`wiki/concepts/retrieval-augmented-generation.md`](wiki/concepts/retrieval-augmented-generation.md)
   if you want the full explanation.
3. Those embeddings are stored in a **Postgres/pgvector** database hosted
   on **Railway**.
4. When you ask Makoto-kun a question on Discord, it embeds your question
   the same way, searches pgvector for the closest-matching chunks, and
   uses them to generate an answer — rather than searching the open web.

So the pipeline end-to-end is: **raw transcript → wiki page → vector
embedding → Discord answer.**

## Adding new knowledge

If you have new material (a lecture transcript, an updated schedule, notes
from a site visit) that Makoto-kun should know about:

1. **Drop the file(s) into the right subfolder of `raw/`** —
   `raw/curriculum/`, `raw/automation/`, or `raw/program/`, depending on
   what it is.
2. **Ask Claude Code to ingest it** — say something like *"New files have
   been added to raw/, ingest them."* It will read the new files, write or
   update the relevant `wiki/` pages, cross-link them, and log the change
   in `wiki/log.md`.
3. **Review the generated pages** — skim what got created or updated under
   `wiki/` and make sure it reads correctly.
4. **Push the changes** to this repo.
5. **Re-run the "Wiki to Vector Store Loader" workflow** in n8n so the new
   or updated pages get re-embedded into pgvector. Until this step runs,
   Makoto-kun won't know about the change yet.

## A note on the two "RAG"s

You may notice the curriculum itself teaches RAG as a concept (lecture
transcripts get chunked and embedded too, as a teaching demo). That's a
separate, parallel pipeline from this one — this repo's `wiki/` → pgvector
loader is the curated, production version that actually powers the bot you
talk to. See [`wiki/entities/makoto-kun.md`](wiki/entities/makoto-kun.md)
for the full version history of how Makoto-kun evolved from a plain
ChatGPT persona (1.0) to this RAG pipeline (2.3) to today.

## Where to look next

- [`wiki/index.md`](wiki/index.md) — full table of contents for the wiki.
- [`wiki/log.md`](wiki/log.md) — append-only history of every ingest.
- [`CLAUDE.md`](CLAUDE.md) — the full rules Claude Code follows when
  compiling this wiki, if you want the details.

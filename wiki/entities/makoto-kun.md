---
type: entity
title: Makoto-kun (AI teaching assistant)
sources:
  - raw/curriculum/nucu_lecture_session3_1_27_2026_CUT.txt
  - raw/curriculum/nucu_lecture_session6_2_17_2026_CUT.txt
  - raw/curriculum/nucu_lecture_session12_4_7_2026_CUT.txt
  - raw/curriculum/nucu_lecture_session13_4_14_2026_CUT.txt
updated: 2026-07-07
tags: [ai-assistant, rag, nucu, makoto-kun]
---

Makoto-kun is the AI teaching assistant Samuel Goodman built for the NUCU program, and the reason this wiki exists: it is the retrieval target these pages feed. Makoto-kun answers student questions about lecture content, the program schedule, and logistics, first through Discord and now via a retrieval-augmented pipeline. Students can ask it things like "what did we cover in session six?" or "why should I join NUCU?" and it answers from its knowledge base instead of a generic web search.

**Version history**, as demoed live in lectures:
- **1.0** (mentioned session 3): built as a custom ChatGPT ("GPT") with a prompt persona and a knowledge base of raw text — a brochure, a tentative calendar, meeting notes. Worked, but every added document meant a longer, more brittle system prompt.
- **2.0 / 2.1** (session 6): rebuilt in **n8n** (a no-code/low-code automation platform), still using flat text documents fed wholesale into the model on every query — accurate but token-expensive, and it would error if a question didn't closely match the source text. Connected to Discord as the chat interface for the first time.
- **2.3** (session 12): added a true **RAG** ([[retrieval-augmented-generation]]) pipeline — lecture transcripts are cleaned, uploaded to a GitHub repo ("Nuku Docs"), pulled into an n8n workflow, chunked, embedded into a vector database, and queried by similarity search rather than dumping the whole document into context every time. This is the version referenced when Goodman shows the SQL query confirming chunk counts (347 chunks as of session 12) and demonstrates asking about session 6 content ("Kuroshi") through Discord.
- **3.0 (planned)**: Goodman describes wanting to move Makoto-kun to an **OpenClaw**-style "second brain" agent architecture, similar to linking Obsidian notes with Claude Code, to reduce token overhead further and let the assistant ingest more heterogeneous content (screenshots, podcast audio, reports) automatically.

**Architecture (2.3)**: Discord is the interface layer; a webhook feeds an n8n AI agent; the agent has a persona prompt ("quirky, nerdy, digital intern assistant"), a rule to stay in its knowledge base rather than searching the web, and tool access to email and calendar (draft-stage). It calls out to an OpenAI ChatGPT model for generation, but the model is swappable.

**Known limitations** (Goodman is candid about these in demos): RAG retrieval sometimes fails to surface content that is present in the database — the same question sometimes needs to be rephrased or given a keyword hint before it retrieves successfully. This is presented as a live, ongoing engineering problem, not a solved one.

Note: `wiki/**/*.md` in this repo is loaded into a separate pgvector store by the n8n workflow "Wiki to Vector Store Loader" (see `CLAUDE.md`) — a different, curated pipeline from the raw-transcript RAG store described above.

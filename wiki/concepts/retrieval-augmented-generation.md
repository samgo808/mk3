---
type: concept
title: Retrieval-Augmented Generation (RAG)
sources:
  - raw/curriculum/nucu_lecture_session6_2_17_2026_CUT.txt
  - raw/curriculum/nucu_lecture_session12_4_7_2026_CUT.txt
updated: 2026-07-07
tags: [rag, vector-database, embeddings, curriculum-module-3]
---

Retrieval-Augmented Generation (RAG) is the architecture behind [[makoto-kun]] 2.3, the NUCU program's AI assistant, and this session (session 12) is a live, hands-on build-along of the pipeline — the closest thing in the curriculum to how *this very wiki's* retrieval pipeline works (per `CLAUDE.md`, wiki pages are chunked and embedded into pgvector for the Discord bot, the same pattern demonstrated here).

**Why RAG, instead of just pasting a document into an LLM's context**: Makoto-kun 2.0/2.1 fed whole text documents into the model on every query — accurate but token-expensive, and it broke if a question didn't closely match the literal source text. RAG instead breaks source documents into small chunks *once*, converts each chunk to a numeric vector ("embedding") capturing its meaning, and stores those vectors in a **vector database**. At query time, only the most relevant chunks (by similarity) are retrieved and handed to the LLM to generate an answer — far fewer tokens per query, and answers can synthesize rather than just regurgitate.

**The two-phase pipeline demonstrated**:
1. **Ingestion**: a lecture transcript is manually cleaned (off-topic chatter removed, since classroom microphones capture everything, including private conversations that shouldn't be public), keyword-tagged, saved as a text file, uploaded to a GitHub repo ("Nuku Docs"), and pulled by an n8n workflow that chunks the text and embeds it into a vector store — session 12's demo added 71 new chunks, bringing the running total to 347.
2. **Retrieval + generation**: a Discord message triggers a webhook into an n8n AI agent, which embeds the *question* the same way, searches the vector database for the closest-matching chunks (a **dot product** / cosine-similarity calculation — related vectors point in similar directions in a high-dimensional space; opposite meanings point oppositely; unrelated concepts sit at a roughly 90° angle), passes those chunks to the underlying LLM (swappable — currently OpenAI), and returns a synthesized answer through Discord.

**Embeddings, explained via the classic analogy used in class**: words are positioned in a multi-dimensional vector space based on meaning, so that the vector distance between "man" and "woman" mirrors the distance between "king" and the word the model should predict next ("queen"). RAG applies the same geometry to whole chunks of lecture transcript, not just single words.

**Honest limitations, demonstrated live**: RAG retrieval sometimes fails to surface content that is verifiably present in the database — the same underlying question ("when did we talk about Reiwa?") failed on one phrasing and succeeded on a rephrased, more specific one ("we have a lecture discussing overwork"). This is presented as a real, unresolved engineering problem (prompt/query sensitivity in retrieval), not a solved technique — directly relevant to how the pages in *this* wiki should be written for retrieval (see `CLAUDE.md`'s "Writing for retrieval" section: self-contained, front-loaded summaries, defined terms).

**Where it's headed next**: the instructor describes wanting to move Makoto-kun 3.0 toward an **OpenClaw**-style agent/"second brain" system (see [[makoto-kun]]) rather than a pure RAG pipeline, to reduce token overhead further and support more heterogeneous input types.

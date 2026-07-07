---
type: concept
title: AI model taxonomy (LLM, SLM, LCM, RLM)
sources:
  - raw/curriculum/nucu_lecture_session4_2_3_2026_CUT.txt
updated: 2026-07-07
tags: [ai-models, llm, slm, curriculum-module-3]
---

This session gives NUCU students a working vocabulary for different classes of AI model, using a "big speaker system → headphones → tiny watch speaker" miniaturization analogy as the throughline: bigger and more general isn't always better, and the field is trending toward smaller, more specialized models. It sets up [[large-language-models]] (how models like these are actually trained) and [[retrieval-augmented-generation]] (how [[makoto-kun]] combines a general model with a narrow knowledge source).

**Large Language Models (LLMs)** — generalists trained on huge, broad datasets (trillions of parameters in leading models); good breadth, not necessarily depth. Examples discussed: ChatGPT (~1.1B monthly active users), Gemini, Copilot, Claude, Grok. Strengths: a good "front desk" or "quarterback" interface — doesn't know everything, but knows where to point you. Weaknesses: high latency (bigger models can be *slower*, not faster), enterprise/compliance constraints (a locked-down Copilot in a government-contracting or SharePoint-only environment can't do what a consumer tool can), and a widely discussed "convergence" problem — as public data runs out, each new flagship release (e.g., GPT-5 following 4) delivers diminishing "wow" factor, similar to incremental iPhone hardware updates.

**Small Language Models (SLMs)** — trained on a narrow domain (e.g., an auto-mechanic's engine-specification model, a legal/accounting assistant like "Co-Counsel," a company's own product/inventory data) for precision over breadth. Associated with **edge** deployment — running locally on a device/business rather than over the network — which matters for latency, privacy (sensitive data never leaves the device), and cost (local/open-source models like "Claudebot," a nickname for an open-source Claude-style model runnable on consumer hardware like a Mac Mini, avoid per-query subscription fees).

**Latent Consistency Models (LCMs)** — optimized for constant, near-instant response time regardless of query complexity, at the cost of some flexibility. Named use cases: battlefield friend-or-foe identification, surgical AR overlays, robot navigation — anywhere latency itself is the safety-critical variable.

**Large Concept Models (also abbreviated LCM in this lecture, distinct from the model above)** — shift from predicting the next *word/token* to reasoning over whole *concepts* (e.g., correctly disambiguating "sustainability" as financial vs. environmental from context) and are described as better suited to multilingual/meaning-level tasks (e.g., avoiding literal-translation errors) than token-level models.

**Recursive Language Models (RLMs)** — flagged as a frontier, MIT-associated research direction: current flagship LLMs degrade in quality as context length grows (the more you feed them, the more they seem to "forget"); RLMs are described as resisting that degradation and supporting much larger effective context, implying today's models will look "pathetic" within a few years.

The lecture also introduces the **5P prompt-engineering framework** as the practical takeaway for working with any of these — see [[prompt-engineering]].

---
type: source
title: "Source: Session 5 — LLMs, Transformers & AI deep dive (2026-02-10)"
sources:
  - raw/curriculum/nucu_lecture_session5_2_10_2026_CUT.txt
updated: 2026-07-07
tags: [source, session5, llm, transformers]
---

Raw transcript of NUCU session 5 (February 10, 2026), a guest technical deep dive (instructor identifies himself as co-teaching alongside Matt Brady, leading the Japan-culture and AI-assistant threads) explicitly adapted from Andrej Karpathy's public LLM-building walkthroughs, "updated" and "modified" for a business-school audience.

**Key claims covered, in three stages**: (1) **pretraining** — Common Crawl and FineWeb dataset curation (filtering, deduplication, PII removal), byte/binary encoding, tokenization (with a live tokenizer demo turning a ~1,400-character Hobbit-review blog post into 313 tokens), and next-token-prediction training via weight/probability adjustment, illustrated with a GPT-2-scale transformer visualization; (2) **supervised fine-tuning (SFT)** — human labelers (domain experts) writing example conversations following helpful/truthful/harmless guidelines, synthetic data generation, conversation-formatting tokens, and hallucination-reduction training (teaching "I don't know" responses and tool-use fallback); (3) **reinforcement learning (RL)** — the chemistry-textbook analogy for optimizing *how* a model reasons to an answer, DeepSeek's discovery that RL-trained accuracy correlated with longer "thinking," and a live comparison of GPT-4 vs. newer models correctly answering "is 9.11 or 9.9 larger" and counting every third letter of "ubiquitous."

Also covers: long-term (trained-in) vs. short-term (context-window) model memory; models not inherently self-identifying without a system prompt; GPU economics (H100 ~$2.20/hr rental or $25–40K purchase; B200 ~$3.79/hr or $45–50K) and Elon Musk's Colossus data-center scale/energy figures; parameter/context/token-count scaling from GPT-2 to GPT-5-class models.

**Why it was added**: the technical backbone for how the models discussed throughout the course (and Makoto-kun itself) are actually built. Updated → [[large-language-models]].

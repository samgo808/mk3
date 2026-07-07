---
type: concept
title: Prompt engineering & the 5P framework
sources:
  - raw/curriculum/nucu_lecture_session4_2_3_2026_CUT.txt
updated: 2026-07-07
tags: [prompt-engineering, 5p-framework, curriculum-module-3]
---

NUCU teaches prompt engineering as a practical business skill, not just an AI-hobbyist one, framed around a **"5P" framework** (the lecture doesn't spell out all five P's individually in the transcript, but frames them around: what do you want the model to do, who should it behave as/what persona, and what does success look like — i.e., role, task, and success criteria). Students are pointed to worked 5P examples for common business-school tasks: market research, lean canvas development, and product-market fit (PMF) analysis — chosen specifically because NUCU teams will use exactly these techniques to develop their Japan startup concepts (see [[design-thinking-sprint]]).

**Demonstrated workflow** (a real automation the instructor uses): a Salesforce lead is created → filtered for junk/test data → enriched via FireCrawl (pulls LinkedIn data) → handed to Gemini (via the no-code tool Zapier) with a detailed persona prompt ("you are a strategic donation advisor and growth hacker... be succinct, don't reiterate the instructions") → the enriched dossier is written back into Salesforce automatically. The result: a raw lead becomes a fully researched prospect profile within seconds of form submission.

**Prompting principles emphasized**:
- Give the model a clear role/persona and explicit constraints ("don't repeat the instructions back to me," "be succinct").
- **Meta-prompting**: if you don't know how to write a good prompt, ask the LLM itself to write one for you, explicitly invoking the 5P structure.
- Few-shot examples (showing the model 1–2 model conversations before asking your real question) reliably improve output quality — this technique is also covered from the model-training side in [[large-language-models]] (it's structurally similar to supervised fine-tuning, just done at inference time instead of training time).
- Be aware of what you're uploading: any document pasted into a hosted chat tool (with history/training not explicitly disabled) may be used to train the model — the instructor flags this as a real compliance risk for anyone pasting confidential business documents into public AI tools "for a quick answer."

This page complements [[ai-model-taxonomy]] (what kind of model you're prompting) and [[vibe-coding-nocode-tools]] (where the same broad→specific prompting discipline is applied to building software rather than answering questions — see Session 13's explicit "plan first, then narrow" prompting advice for Lovable/Claude Code).

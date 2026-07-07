---
type: concept
title: Vibe coding & no-code/low-code tools
sources:
  - raw/curriculum/nucu_lecture_session12_4_7_2026_CUT.txt
  - raw/curriculum/nucu_lecture_session13_4_14_2026_CUT.txt
updated: 2026-07-07
tags: [vibe-coding, no-code, low-code, claude-code, glide, lovable, curriculum-module-3]
---

NUCU teaches a spectrum of tools for turning an idea into working software without a traditional years-long dev cycle, framed as directly usable for building a working prototype of a team's Japan startup pitch. The spectrum runs from no-code → low-code → "vibe coding" → full code, trading control/customization for speed.

**No-code — Glide**: turns a spreadsheet (Google Sheets or similar) directly into a mobile/web app — pick-lists, images (via free APIs like Pexels), and "smart columns" that call an LLM (e.g., Gemini) per row are all configured without writing code. Fast and genuinely useful for internal tools (the instructor's own "Build in Japan" program-logistics app is built on Glide), but you never see or own the underlying code, and you don't fully control where your data lives — a real limitation once an app needs custom data ownership or integration.

**"Vibe coding" — Lovable** (and similar: Replit, Cursor, Windsurf, Base44, Google Stitch for pure UI mockups): the term (credited to Andrej Karpathy) describes describing the *outcome* you want in natural language and letting the platform figure out the implementation — React/Tailwind frontend, database, auth — rather than hand-writing framework glue code. Two interaction modes: **chat mode** (collaborative, turn-by-turn: "make this bigger," "try again") versus **agent mode** (you hand over a full spec — target market, user stories — and it works autonomously, testing and optimizing on its own, trading control for speed). Demonstrated live: building a Studio-Ghibli-styled workout/sleep tracker PWA (progressive web app) from a single prompt in under 30 seconds of "thinking."

**Recommended prompting sequence** for any of these tools: start broad (plan/wireframe first — "there's no fun automating a bad idea"), then narrow to component-level fixes, then finally to pixel-level nitpicks (rounded corners, button animations) — never start at the nitpicking level. Feeding the tool existing artifacts (a pitch deck, a class roster spreadsheet) lets it infer data structure and UI automatically (e.g., recognizing "S/M/L/XL" as a pick-list).

**Full code — Claude Code** (and Cursor/VS Code more generally): described as one step further down the "vibe coding" continuum — you're directing in natural language, but the tool produces real, portable code you can push to GitHub and host anywhere (the instructor's own demos: a marketing site on **Vercel**, a small "senior tech support" business site, a teen driving-hours tracker app, and student-built demos including a Claude-generated Japan-population map/simulation). Claude Code can also teach you unfamiliar infrastructure as you go (e.g., walking the instructor through **Railway**, a platform-as-a-service used to host the n8n/vector-database backend behind [[makoto-kun]]).

**Why this matters for the course's thesis**: the lecture repeatedly returns to the idea that tiny teams can now build software that used to require large engineering orgs — citing a real (if later controversial) example of a two-person team building a $1.8B healthcare company almost entirely on AI-assisted no-code/low-code tooling. The broader economic prediction offered: software companies increasingly compete on *data*, not code, since code itself is becoming cheap and reusable ("why reinvent the wheel" for common modules like tax calculation or shipping logistics).

See [[prompt-engineering]] for the underlying prompting discipline this builds on, and [[retrieval-augmented-generation]]/[[makoto-kun]] for the n8n-based system these same tools are used to build and extend.

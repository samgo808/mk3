---
type: concept
title: OSI model & TCP/IP networking fundamentals
sources:
  - raw/curriculum/nucu_lecture_session4_2_3_2026_CUT.txt
updated: 2026-07-07
tags: [networking, osi, tcpip, curriculum-module-3]
---

The OSI (Open Systems Interconnection) model is a seven-layer blueprint, developed by the International Organization for Standardization (ISO), describing how two computer systems communicate. NUCU teaches it not as trivia but as a troubleshooting mental model — the same way you'd debug "why won't my movie play" layer by layer (power → device → network → app) — and as groundwork for understanding how [[large-language-models]] and the internet infrastructure underneath them actually work, rather than treating AI as an unexplainable black box.

**The seven OSI layers**, bottom to top:
1. **Physical** — the actual hardware/signal: cables, Wi-Fi, fiber, radio waves.
2. **Data link** — packages data for the local network and checks for errors, keyed to the MAC address (a device's low-level hardware identifier).
3. **Network** — assigns IP addresses and routes packets to the right destination (like a GPS); packet loss/pixelation in a video stream is often a breakdown at this layer.
4. **Transport** — ensures packets arrive complete and in order, resending missing pieces (the "delivery truck").
5. **Session** — keeps a connection open between devices, and closes it (e.g., session timeouts on websites).
6. **Presentation** — formats and **encrypts** data (the "security" layer, despite its name suggesting visual presentation).
7. **Application** — the layer users directly interact with: browsers, email, messaging apps.

**TCP/IP** (Transmission Control Protocol / Internet Protocol) is the practically-important, streamlined counterpart: it collapses OSI's seven layers into four — network access, internet (IP, routing), transport (TCP, host-to-host), and application (layers 5–7 combined). Almost all modern computer networks run on TCP/IP; OSI is the theoretical study framework, TCP/IP is the working reference model professionals actually use day to day. Both were emphasized for the course quiz.

**Why the course teaches this before AI models**: the instructor's framing is that business students need to understand how data physically and logically moves between systems before treating AI (which runs *on* the internet) as magic. This also seeds a career-path aside: the AI infrastructure buildout (data centers, GPUs) is driving huge demand for skilled trades (electricians, plumbers) near data center construction, and for networking-hardware companies like Cisco.

**Bridge to AI models**: the lecture pivots from networking directly into the AI model taxonomy — see [[ai-model-taxonomy]] for large/small/latent-consistency/large-concept model types, and [[large-language-models]] for how these models are actually built and trained. The energy and infrastructure cost of AI data centers (raised here via the Indianapolis Google data-center pushback example) recurs as a theme in both of those pages.

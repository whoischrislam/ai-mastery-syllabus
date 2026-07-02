# AI Mastery Syllabus

This is the living, cert-free AI mastery syllabus. Updated as you progress. The goal: go toe-to-toe with the best engineers working on AI systems — not by getting a job first, but by outgrowing the need to prove it.

> **Guiding principle:** You don't need permission from a company to level up. The certification path was the vehicle, not the destination. The content is what matters — and all of it is publicly available. Anthropic Academy (anthropic.skilljar.com) is now the primary structured source: 17 free courses, official certificates, all self-paced.

> **Note (maintenance):** Canonical copy lives here in-repo, version-controlled — the [Notion page](https://app.notion.com/p/3795a322f09e81c98f4fe396b40fd8bb) is a pointer plus the job-hunt/weekly-planning surface, not a mirror. Status markers updated as work lands. Last sync: 2026-07-01 — Practice System upgraded: production-gap diagnosis added, practices now status-tracked with a rep log, deck 14 (Production Drills, spoken) seeded in `srs/decks/`, Week 8 capstone made attemptable from week 1 (PD-15). Interview Mode Protocol ported from Notion; job-hunt targets stay in Notion.

---

## 📍 Status Legend

| Symbol | Meaning |
| --- | --- |
| ✅ | Done |
| 🔄 | In progress |
| ⬜ | Not started |
| 🔁 | Revisit / deepen |

---

## 🗓️ Pre-Sapporo — Input Density Sprint

Goal: maximize conceptual breadth before the break. **Read more, build less.** No deliverables right now — Sapporo does the consolidation work. Come back and the artifacts will write themselves.

> **Strategy:** Front-load the unfamiliar and conceptually dense material. Skip anything already consolidated (Week 1 is done). Skip deliverables — ADRs, AGENTS.md updates, and ARCHITECTURE.md all happen post-Sapporo.

### ✅ Already done

- ✅ Read Anthropic's core prompt engineering docs
- ✅ Read the CCA-F domain breakdowns (dev.to + certsafari.com) — used as curriculum map
- ✅ Bookmark the 25 free practice questions at claudecertifications.com
- ✅ Week 1: Claude Code docs + CLAUDE.md hierarchy (already consolidated — no incubation needed)

### 📖 Read/Watch before Sapporo (ranked by incubation value)

- ✅ **Building with the Claude API** — Skilljar course. **COMPLETE (2026-06-14).** All sections done: API fundamentals, tool use, agents & workflows, RAG, MCP, and Features of Claude (prompt caching, extended thinking, citations → seeded as SRS deck 13). Find it at anthropic.skilljar.com
- ✅ **Introduction to Model Context Protocol** — Skilljar course. Tools, resources, prompts primitives. Mental model before Sapporo = Week 5 build feels like executing a plan. Find it at anthropic.skilljar.com
- ✅ **Introduction to subagents** — Skilljar course. Context delegation, task handoff, specialized workflows. Short course, high incubation value. Find it at anthropic.skilljar.com
- ✅ Read Anthropic multi-agent cookbook — let the orchestrator/subagent patterns marinate
- ✅ Read Hamel Husain — Your AI Product Needs Evals — initial skim + deep read done 2026-06-13. Carded into SRS deck 04 (3-level eval model, LLM-as-judge + the alignment step, error analysis, data flywheel, evals-before-prompts). Incubation pass complete; Week 8 is the formalization pass → EVALS.md.
- ⬜ Watch Stanford CS229 LLM lecture — post-training half only (~1:00:00 mark). SFT + RLHF reframes every prompt design decision you've made. **Plan: watch on the Sapporo flight; card as deck 05 on return.**
- ✅ Read Anthropic prompt library — fast, pairs with what you already read

### 🚫 Skip until post-Sapporo

- Week 1 audit + AGENTS.md update — already consolidated
- All deliverables (ADRs, ARCHITECTURE.md, EVALS.md) — write these after the break
- LiveKit source + hardware (Phase 3) — too implementation-specific for passive processing
- Claude Code in Action Skilljar course — you already use it daily, save for Week 1 deepening

---

## 🔵 Phase 1 — Foundations & Vocabulary

Weeks 1–6 post-Sapporo. Goal: Master all 5 CCA-F domains through primary sources + Skilljar courses. **Reading sprint before Sapporo means Week 4+ material is already in your head when you start building.**

### Week 1 — Claude Code & Configuration ✅ Mostly done pre-Sapporo

You're already ahead here. .claude/, AGENTS.md, MEMORY.md in y30-voice. Reading is done — this week post-Sapporo is just the audit and deliverable.

- ✅ Read the Claude Code docs top to bottom as a spec
- ✅ Read the CLAUDE.md hierarchy docs — user-level, project-level, directory-level
- ⬜ **Claude Code 101** — Skilljar course. Even if familiar, catch any gaps. ~30 min. Find it at anthropic.skilljar.com
- ⬜ **Claude Code in Action** — Skilljar course. Integrate advanced workflow patterns into daily dev. Earn certificate. Find it at anthropic.skilljar.com
- ⬜ **Introduction to Agent Skills** — Skilljar course. Build/configure/share Skills in Claude Code. Directly applicable to y30. Find it at anthropic.skilljar.com
- ⬜ Audit y30-voice .claude/, AGENTS.md, MEMORY.md against full spec
- ⬜ Deliverable: AGENTS.md updated and onboarding-ready for Vijay

### Week 2 — Prompt Engineering & Structured Output

You read the core docs already. This week goes deeper into tool use and produces your first ADR.

- 🔁 Re-read Anthropic prompt engineering docs — this time take notes
- ⬜ Read the Anthropic prompt library
- ⬜ Read tool_use JSON schema docs
- ⬜ Install and use the instructor Python library once — understand the pattern
- ⬜ **AI Fluency: Framework & Foundations** — Skilljar course. The 4D Framework (Delegation, Description, Discernment, Diligence). Fast (~1 hr). Earn certificate. Find it at anthropic.skilljar.com
- ⬜ Deliverable: ADR #1 committed — "Why y30 uses FSM for flow and LLM for phrasing"

### Week 3 — Context Management & Reliability

- ⬜ Read Anthropic long-context best practices
- ⬜ Read your own MEMORY.md and FEEDBACK.md critically — can you explain every decision in writing?
- ⬜ **AI Capabilities and Limitations** — Skilljar course. Introductory but fills in mental model gaps on what Claude can/can't do reliably. Short. Find it at anthropic.skilljar.com
- ⬜ Deliverable: ADR #2 committed — "How y30 handles provider fallback and why"

### Week 4 — Agentic Architecture & Orchestration

The most important domain. Maps directly to your y30 architecture and Staff-level interviews.

- ⬜ Read Anthropic agentic systems docs
- ⬜ Read Anthropic multi-agent patterns cookbook
- ⬜ **Building with the Claude API** — Skilljar course (✅ done pre-Sapporo). Full API spectrum, agentic patterns, tool use contracts. Earn certificate. Find it at anthropic.skilljar.com
- ⬜ **Introduction to subagents** — Skilljar course (✅ done pre-Sapporo). Context delegation + specialized workflows. Find it at anthropic.skilljar.com
- ⬜ Read Linas Substack — "Everything Anthropic Teaches Its Claude Certified Architects" (free)
- ⬜ Map every pattern (orchestrator/subagent, parallelization, speculative execution, hooks) to y30 or name it as a gap
- ⬜ Deliverable: ARCHITECTURE.md live in y30-voice with FSM/LLM diagram
- ⚡ Practical: Build your first Workflow in Claude Code — parallel(), pipeline(), structured output schema. Use it to run a y30 session audit: fan out across 3 recent transcripts in parallel, collect structured scores, aggregate. This is the fastest path from "I understand orchestration patterns" to "I've built one." The Workflow tool is Claude Code-specific, deterministic, and available right now — no SDK required. Do this before writing ARCHITECTURE.md so you have a real example to document.

### Week 5 — Tool Design & MCP Integration

Your only real gap. Build something real this week.

- ⬜ **Introduction to Model Context Protocol** — Skilljar course (✅ done pre-Sapporo). Tools, resources, prompts primitives from scratch. Earn certificate. Find it at anthropic.skilljar.com
- ⬜ **Model Context Protocol: Advanced Topics** — Skilljar course. Sampling, notifications, filesystem access, transport for production MCP servers. Earn certificate. Find it at anthropic.skilljar.com
- ⬜ Read MCP Python SDK
- ⬜ Build one real MCP server in y30-voice — caregiver summary tool or session metadata tool
- ⬜ Deliverable: Working MCP server committed + ADR #3 — "Why y30's safety layer is model-independent"

### Week 6 — Self-Assessment & Gap Close

- ⬜ Take the 25 free practice questions as a diagnostic
- ⬜ Read the full CCA-F GitHub guide — all 5 domains with scenario examples
- ⬜ For every question missed: trace back to the source doc, re-read that section
- ⬜ Confirm all Skilljar certificates earned from Phases 1–5 above
- ⬜ Deliverable: Personal gap list, all gaps closed

---

## 🟡 Phase 2 — Applied Mastery & Portfolio Hardening

Weeks 7–10. Goal: Close the multi-agent gap, formalize evals, ship new portfolio artifacts.

### Week 7 — Multi-Agent Build Project

The one project that closes your Staff-level interview gap permanently. Small but real, explicit contracts between agents.

- ⬜ Build a coordinator/subagent system outside y30
- ⬜ Suggested scope: post-session intelligence pipeline — coordinator spawns scoring subagent, summary subagent, and flag-for-review subagent with explicit contracts
- ⬜ Build against the Anthropic multi-agent cookbook directly
- ⬜ Deliverable: Repo live, linked from portfolio
- ⚡ Completion criterion: The repo must include at least one Workflow-based component (not just SDK subagents). If you built the Week 4 y30 session audit Workflow, refactor or extend it here into the coordinator pipeline. Workflow + SDK subagents together is the full orchestration picture. A repo with only one of them is an incomplete answer to "have you built a multi-agent system?"

### Week 8 — Evals: The Missing 20%

Hardest unsolved problem in production AI right now. You have a head start with y30's eval pipeline — this week formalizes it.

- ⬜ Read Hamel Husain — Your AI Product Needs Evals
- ⬜ Read Eugene Yan's LLM evaluation writing
- ⬜ Audit y30 eval pipeline against these frameworks — what's missing?
- ⬜ Deliverable: EVALS.md live in y30-voice — rubrics, LLM judge setup, regression pattern, WER tracking

### Week 9 — Stanford CS146S: The Modern Software Dev

Skip Weeks 1, 3, 5, 8 — you're past those. These 4 weeks are your targets.

- ⬜ CS146S Week 2: MCP deep dive — themodernsoftware.dev
- ⬜ CS146S Week 6: AI testing & security — context rot, prompt injection, SAST/DAST
- ⬜ CS146S Week 7: Code review in AI-native workflows
- ⬜ CS146S Week 9: Agents post-deployment — observability, incident response
- ⬜ Deliverable: Notes doc with 3 concrete changes to make in y30 or multi-agent project

### Week 10 — y30 Onboarding Sprint

Every hour here is simultaneously: Vijay onboarding, comprehension formalization, and portfolio artifact.

- ⬜ Write ONBOARDING.md — local setup, agent loop walkthrough, how to run evals, how to add a new FSM state
- ⬜ Update CONTRIBUTING.md — Vijay-ready and new-engineer-ready
- ⬜ Update portfolio: add architecture diagram to y30 section, link ARCHITECTURE.md, surface MCP server as technical artifact
- ⬜ Deliverable: Repo is genuinely handoff-ready

---

## 🟠 Phase 3 — Deep Foundations

Weeks 11–14. Goal: Understand why the stack works. Go toe-to-toe with anyone. **Phase 3 is stretch material — does not start until the Week 8 checkpoint passes (see below).**

### Week 11 — CS229: Why LLMs Behave the Way They Do

Watch the post-training half only (~1:00:00 mark onward). SFT and RLHF explain why Claude follows your system prompts.

- ⬜ Watch Stanford CS229 LLM lecture — post-training half only (if not done pre-Sapporo)
- ⬜ Focus: SFT, RLHF — connect back to y30 prompt design decisions
- ⬜ Deliverable: One-page personal notes — "Why y30's system prompts are structured the way they are"

### Week 12 — LiveKit Agents Source Code

You use it every day. Own the mental model.

- ⬜ Read LiveKit Agents Python source
- ⬜ Focus: agent loop internals, VAD hook points, where your FSM sits relative to the framework
- ⬜ Deliverable: One diagram — "y30's layer over LiveKit Agents"

### Week 13 — Hardware / Embedded

Small project, 1–2 weeks. Produces a portfolio artifact almost no design engineers have.

- ⬜ Raspberry Pi voice endpoint for y30 — button-triggered, speaks to agent, reads back response
- ⬜ Primary source: LiveKit Agents Raspberry Pi examples
- ⬜ Deliverable: Working Pi endpoint + short demo video

### Week 14 — Integration & Interview Readiness

- ⬜ Do one mock Staff-level system design interview — peer or Claude as adversarial interviewer
- ⬜ Record yourself explaining y30 architecture out loud — find where you reach for intuition over vocabulary
- ⬜ Update llms.txt and portfolio with everything from Phases 1–3
- ⬜ Deliverable: You can hold the full Staff IC technical conversation without gaps

---

## 🎓 Anthropic Academy — Skilljar Courses

All free at anthropic.skilljar.com. Official certificates on completion.

| Course | When | Direct Value to y30 |
| --- | --- | --- |
| Claude Code 101 | P1 W1 | Baseline gaps check |
| Claude Code in Action | P1 W1 | Advanced daily workflow |
| Introduction to Agent Skills | P1 W1 | Skills for y30 Claude Code |
| AI Fluency: Framework & Foundations | P1 W2 | 4D Framework, prompting |
| Building with the Claude API ✅ | Pre-Sapporo (done) | Full API + agentic patterns |
| Introduction to subagents ✅ | Pre-Sapporo (done) | Multi-agent context delegation |
| Introduction to Model Context Protocol ✅ | Pre-Sapporo (done) | MCP primitives from scratch |
| Model Context Protocol: Advanced Topics | P1 W5 | Production MCP patterns |
| AI Capabilities and Limitations | P1 W3 | Mental model gaps |

**Skip for now:** Claude 101 (too basic), AI Fluency for educators/students/nonprofits (not your context), Claude with Bedrock/Vertex AI (unless y30 moves clouds), Introduction to Claude Cowork (personal productivity, not engineering), Teaching AI Fluency (not relevant).

---

## 📚 Reference Resources

| Resource | Phase | Domain | Link |
| --- | --- | --- | --- |
| Anthropic Prompt Engineering Docs | P1 W2 | D4 | link |
| Anthropic Long Context Tips | P1 W3 | D5 | link |
| Anthropic Agentic Systems Docs | P1 W4 | D1 | link |
| Anthropic Multi-Agent Cookbook | P1 W4 + P2 W7 | D1 | link |
| Claude Code Docs | P1 W1 | D3 | link |
| MCP Python SDK | P1 W5 | D2 | link |
| Free CCA-F Practice Questions | P1 W6 | All | link |
| CCA-F GitHub Guide | P1 W6 | All | link |
| Hamel Husain — Evals | P2 W8 | Evals | link |
| Eugene Yan — LLM Evals | P2 W8 | Evals | link |
| Stanford CS146S | P2 W9 | Applied | link |
| Stanford CS229 LLM Lecture | P3 W11 | Foundations | link |
| LiveKit Agents Source | P3 W12 | Stack | link |
| Anthropic Academy (all courses) | All phases | All | link |

---

## 🏁 The One-Line Summary

By Week 14: Not preparing to go toe-to-toe. You are toe-to-toe.

---

## 🎯 Closing the Articulation Gap — The Practice System

The gap between what you can build and what you can explain is the difference between the job you want and the job you're okay with. This section runs in parallel with all phases — it is not optional.

> **Diagnosis (2026-07-01):** The interview gap is a **production gap, not a comprehension gap.** Reading trains recognition; interviews test production — generating the articulation cold, out loud, under time pressure. You cannot read your way across that gap. Known pattern: instinct fires now, articulation arrives after the fact. The fix is mechanical: cache the after-the-fact phrasings (deck 14), drill spoken production until retrieval is instant.

> **Operating rules:**
> 1. **Production before input.** Each study day starts with 5 minutes of *spoken* production on prior material — cold, before any new reading. Written paragraphs don't count; writing routes around stalls that speech exposes.
> 2. **These practices get tracked like everything else.** Reading feels like progress; rehearsal feels like exposure — so unlogged practice silently loses to reading every time. A week with input ✅ and practice ⬜ is a failed week regardless of pages read.
> 3. **Drill deck:** `srs/decks/14-production-drills.md` — spoken production cards (the 3 decision axes, the y30 adversarial set, cross-deck reframes, the 4-minute capstone). Answer template: claim → mechanism → example, graded per slot.

### Rep Log

| Date | Practice | Target | Stall points | Verdict |
| --- | --- | --- | --- | --- |
| — | — | — | — | — |

### 🗓️ Practice 1: Weekly Verbal Rehearsal (Starts Now, Not Week 14) ⬜ weekly — log above

Every week, pick one decision you made that week — an architecture choice, a prompt design, a tradeoff. Explain it out loud for 5–10 minutes as if you're in a Staff IC interview. Don't try to be perfect. Find where you stall, reach for intuition, or go vague. Those stall points are the next thing to formalize.

Prompt to use: "Walk me through why you made this decision. What did you consider? What would you do differently?" Record on your phone if useful. One session per week, every week.

### 🥊 Practice 2: Weekly Adversarial Interview Sim (Against Your Own Work) ⬜ weekly — log above

Every week, use Claude or a peer to interrogate your y30 architecture decisions specifically. Not generic system design. Not a practice exam. Your actual work, under real questioning pressure.

**Question bank: deck 14, Sections B–C** (`srs/decks/14-production-drills.md`). Protocol: questions fired in random order, answer *spoken* before anything is shown, graded claim/mechanism/example separately. A correct claim with a missing mechanism is the recognition-only tell — log it as a stall point. After each rep, cache your best phrasing into the card's back.

Original example questions (now PD-06 – PD-10 in the deck):

- Why FSM over a pure LLM state manager? What does that buy you at runtime?
- How do you handle latency spikes in the STT pipeline? What degrades gracefully?
- Walk me through your eval setup. What's your regression signal?
- How does your agent loop compare to LangGraph's approach? Where is yours better?
- What would you change if you rebuilt this from scratch?

Every vocabulary hole you find here closes faster than weeks of reading. Schedule: every week, starting the first week post-Sapporo — not a milestone gate, a weekly habit.

### 🔥 Practice 3: Production Failure Narration (Rehearse Before First Interview) ⬜ once, then maintain

You will get "walk me through a production failure" at every senior loop. You have real material — use it. Pick two y30 failures and build a 3-minute story for each.

Story structure: what failed → how you found it → what you changed → what you'd build differently.

Start with these two:

- **STT latency incident** — what degraded, how it surfaced, what you changed in the pipeline
- **FSM edge case** — what state broke, how you caught it, what the guard now does

Rehearse out loud, not in writing. Record on your phone if useful. Each story must hold up under one follow-up question. Do this before your first interview loop — it takes one hour and closes a gap that reading cannot.

---

## ⚠️ Week 8 — Interview-Ready Checkpoint (Real Deadline)

Phase 3 (Weeks 11–14) is stretch material. **Week 8 is the real deadline given the late August/September timeline.** By the end of Week 8, you must be able to:

- Explain your y30 architecture end-to-end in 4 minutes with accurate vocabulary (no reaching for intuition)
- Name and define the orchestration patterns (orchestrator/subagent, parallelization, speculative execution, hooks) and map each to y30 or a gap
- Explain the FSM/LLM separation decision as an ADR-quality argument
- Talk about your eval setup, what's missing, and what you'd build next
- Field adversarial questions on your architecture without stalling

If the Week 8 checkpoint is not met, pause Phase 2 deliverables and do another adversarial sim before continuing. **Phase 3 does not start until the Week 8 checkpoint passes.**

**Don't wait for Week 8 to attempt this.** The 4-minute run is PD-15 in deck 14 — attempt it in week 1 and fail informatively. An early failed run tells you exactly which sections stall; that beats weeks of reading toward an untested bar.

---

## 🧪 Tinker (Thinking Machines Lab) — Fine-Tuning Lab

You have $150 in Tinker credit. This is not a far-future experiment — it is a Phase 2 extension that sits alongside Week 8 (evals). Tinker is the fine-tuning API from Thinking Machines Lab (founded by Mira Murati, ex-OpenAI CTO). It handles all distributed GPU infrastructure — scheduling, multi-GPU orchestration, resource allocation — while you control the training data and algorithm entirely. It uses LoRA adapters on open-source models (Llama 3, Qwen3, and others). You are not training from scratch. You are customizing an existing model for a specific task.

Why this matters right now: A LoRA-tuned eval judge model trained on y30 session data is a portfolio artifact almost no other AI engineer candidate has. It turns your evals story from "I have an eval pipeline" to "I trained a domain-specific judge model on real senior care conversation data." That is a different tier of candidate.

The theory that explains why it works comes in Phase 3 Week 11 (CS229 — SFT and RLHF). But you do not need to understand the math to use Tinker productively. The API is designed to abstract that away. Do the build first. The theory will make the build retroactively legible — same pattern as everything else in your learning history.

What to build:

- A lightweight LLM judge fine-tuned on y30 session transcripts to score conversation quality (empathy, clarity, safety flag accuracy)
- Scope: small model (Llama-3.2-1B or 3B), LoRA adapter, ~50–100 labeled examples to start
- Eval: compare judge scores against your existing rubric — do they agree? Where do they diverge?
- Deliverable: model card + training notes committed to y30-voice repo, linked from portfolio

Budget framing: $150 covers 150+ hours of small model fine-tuning or dozens of RL training runs. Enough to iterate seriously without burning through it on a single bad run. Start small, validate the signal, scale up.

Timing: After Week 8 checkpoint passes. Do not start before — the eval pipeline needs to exist before you train a model to score it. Resource: thinkingmachines.ai/tinker

**Decision gate:** If Tinker LoRA is not built before your first interview loop, do not reference it as a planned artifact. Pivot the differentiator story to the existing eval pipeline + LLM-judge setup instead. "I have a domain-specific eval pipeline with a judge model" is the claim. "I plan to fine-tune one" is not. Only use the Tinker story if the model card is committed and publicly visible.

---

## 🔴 Interview Mode Protocol

When an active interview loop starts (phone screen scheduled or later), the syllabus shifts into maintenance mode. Do not try to advance phases during a loop.

**Pause immediately:**

- All new deliverable builds (RAG, MCP, Langfuse, Tinker)
- Any new Skilljar courses
- CS146S reading blocks

**Keep running:**

- Weekly verbal rehearsal (Practice 1) — this *is* interview prep
- Adversarial interview sim (Practice 2) — escalate frequency to every 2 days, drill from deck 14
- Production failure story rehearsal (Practice 3) — must be ready before first technical screen

**Re-entry after loop closes:**

- If offer: Phase 3 is now post-start depth, not pre-start prep. Pause syllabus entirely.
- If no offer: Do one adversarial debrief with Claude on where you stalled. Fix that gap first before resuming the phase you were on.
- Resume from exactly where you paused — do not restart or skip forward.

---

## 🎯 Job Hunt — Lives in Notion

Active targets, outreach templates, weekly plans, and pipeline tracking live in the [AI Mastery Notion doc](https://app.notion.com/p/3795a322f09e81c98f4fe396b40fd8bb) — that's the planning surface. This repo owns the syllabus, decks, and practice system; Notion owns the pipeline. Don't duplicate either direction.

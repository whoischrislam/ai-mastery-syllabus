# Spaced Repetition — repo-native, Claude-run

The learning engine for the **pre-Sapporo input-density sprint**. Source of truth lives
here in markdown (version-controlled, yours forever). Claude runs the reviews each session.

## How a session works

1. You say **"run my SR"** (or just "what's due?").
2. Claude reads `schedule.md`, pulls every card due **on or before the session date**, and
   quizzes you one at a time — **front first**.
3. You answer (out loud or in chat). Claude reveals the back. You grade yourself.
4. Claude updates the card's Leitner box + next-due date in `schedule.md`.
5. When you say so, Claude commits the updated schedule.

Claude uses the **current session date** (from the harness) to compute due dates — not a
hardcoded day. So intervals stay honest even if you skip days.

## Leitner boxes

| Box | Next due | Meaning |
|-----|----------|---------|
| 1 | +1 day  | new / recently missed |
| 2 | +2 days | |
| 3 | +4 days | |
| 4 | +9 days | |
| 5 | +21 days | |
| 6 | +60 days | basically retired |

## Grading (3 grades)

- **Got it** — confident & correct → move **up** one box. **Teach-back required:** Claude will ask you to explain it in one sentence in your own words before the grade locks. If you stumble, it downgrades to Shaky automatically.
- **Shaky** — correct but effortful, or partial → **stay** in the same box, reschedule at its interval.
- **Missed** — wrong or blanked → back to **Box 1**.

## Card-design rules (keep the deck healthy)

- **One idea per card** (minimum-information principle). Anything joined by "and" probably splits.
- **Prefer why/apply over recall.** If you can answer by pattern-matching the words in the prompt, it's a weak card — tell me to rewrite it.
- **Consistently missed = too big.** Tell me to split it.

## Decks

**Reading track** (one deck per pre-Sapporo reading item, lesson-then-card):
- `decks/01-agentic-orchestration.md` — workflow↔agent spectrum, 5 canonical patterns, y30 mappings, failure modes. *(seeded 2026-06-08)*
- `decks/04-evals.md` — velocity reframe, 3-level model (unit/human+model/A·B), LLM-as-judge + alignment, error analysis, data flywheel, evals-before-prompts. *(10 cards, 2026-06-13)*

**Build track** (concepts learned by building the global self-learning loop, 2026-06-09):
- `decks/07-self-learning-loop.md` — compounding requirement, 5 stages, obligatory retrieval, ossification, tombstones. *(9 cards)*
- `decks/08-harness-primitives.md` — primitives decision, scope, promotion ladder, merge/override, blast radius, advisory/authority. *(8 cards)*
- `decks/09-implementation-patterns.md` — prompt injection, detached worker, idempotency, event-source gating, model right-sizing, schema-as-contract, provenance. *(10 cards)*

### Roadmap

**Reading track** (planned):
| # | Deck | Source on the list | Status |
|---|------|--------------------|--------|
| 01 | Agentic orchestration | Intro to subagents + multi-agent cookbook | ✅ seeded |
| 02 | MCP primitives | Introduction to Model Context Protocol | ✅ seeded (6 cards, 2026-06-10) |
| 03 | Claude API agentic patterns | Building with the Claude API | ✅ seeded (first 1/3 — agents & workflows, 8 cards, 2026-06-10) |
| 04 | Evals | Hamel Husain — Your AI Product Needs Evals | ✅ seeded (10 cards, 2026-06-13) |
| 05 | Post-training (SFT/RLHF) | Stanford CS229 LLM lecture | ⬜ |
| 06 | Prompt library patterns | Anthropic prompt library | ⬜ |

**Build track:** 07–09 ✅ seeded 2026-06-09 (27 cards).

**Course track** (one deck per completed course section, Building with the Claude API):
- `decks/10-api-fundamentals.md` — stateless API, messages array, system prompts, temperature, streaming, structured output. *(6 cards, 2026-06-10)*
- `decks/11-agents-workflows-impl.md` — chaining gates, parallel execution, routing classifier, environment inspection, workflow vs. agent in code. *(5 cards, 2026-06-10)*
- `decks/12-rag.md` — what RAG solves, chunking strategies, overlap, embeddings, cosine similarity, hybrid search, reciprocal rank fusion, y30 application. *(8 cards, 2026-06-10)*
- `decks/13-features-of-claude.md` — prompt caching (prefix invariant, placement, silent invalidators, economics), adaptive thinking vs deprecated budget_tokens, effort lever, thinking display≠billing, citations grounding, citations⊥structured-outputs. *(9 cards, 2026-06-14)* — **completes the "Building with the Claude API" course.**

To add the next deck: say **"primer + deck on \<topic\>"** and I'll teach the lesson, then card it.

## Pre-Sapporo sprint plan (set 2026-06-09)

4 study days across the 6 before Sapporo (Jun 15). Gaps on Jun 11 & 13 are the
*spacing* — sleep consolidates, expanding Leitner intervals line up.

| Day | Date | Focus |
|-----|------|-------|
| 1 | Mon Jun 9 | Learn deck 07 (loop) + first pass deck 01 (already due) |
| 2 | Tue Jun 10 | Due reviews + learn deck 08 (primitives) |
| 3 | Thu Jun 12 | Due reviews (01/07/08 cascading) + learn deck 09 (implementation) |
| 4 | Sat Jun 14 | Full interleaved review of everything due + mock-interview teach-back |

### Jun 14 teach-back template

After reviews, go cluster by cluster. For each: explain the concept out loud as if to a skeptical interviewer, then anchor it to y30.

1. **Workflow ↔ agent spectrum** — explain the axis and the default judgment rule. Anchor: where does y30's FSM/LLM split sit on this axis, and why?
2. **5 canonical patterns** — name all five, one-sentence each. Anchor: which patterns are live in y30 today, and which would you add next?
3. **Self-learning loop** — explain the 5 stages and why obligatory retrieval is the keystone. Anchor: what would break in your Claude Code harness if retrieval weren't structural?
4. **Harness primitives** — explain the promotion ladder and blast radius. Anchor: name one rule in your harness that earned a hook, and why it crossed the threshold.
5. **Claude API agents** — explain the agentic loop and the 3 safety principles. Anchor: if y30's session pipeline became an agent, which safety principle would matter most and why?
6. **Evals** — explain the 3-level model and why LLM-as-judge is worthless without the alignment step. Anchor: name one y30 behavior you'd write a Level-1 assertion for, and why "fix evals before prompts" matters most in a safety-critical product.

Run a session any day with **"run my SR"** / **"what's due?"**.

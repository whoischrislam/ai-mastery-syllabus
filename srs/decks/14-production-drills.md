# Deck 14 · Production Drills (Spoken)

Source: articulation-gap session (Claude, 2026-07-01) + SYLLABUS.md Practice 2 question set.
Theme: This deck trains a different skill than decks 01–13. Those train **recognition/recall**
(read front, check back). This trains **production** — generating the articulation cold, out
loud, under time pressure. That is what interviews test, and it is the only mode that closes
the "I get it but can't verbalize it upfront" gap.

Card ID prefix: `PD`. Scheduling state lives in `../schedule.md`.

## Drill rules (non-negotiable)

1. **Speak before checking.** Answer out loud — actual speech, not inner monologue. Speech is
   the tested medium; writing lets you route around stalls that speech exposes.
2. **Grade three slots separately:** claim / mechanism / example. A miss on mechanism with a
   correct claim = the recognition-only tell. Log it.
3. **Backs are must-hit checklists, not scripts.** Hitting the points in your own words is a pass.
4. **Section B backs start as empty templates.** After each rep, fill the back with your own
   best post-rep phrasing. Your after-the-fact articulations are the raw material — caching
   them here and re-drilling is the whole trick (memoization applied to yourself).
5. Template for every answer: **claim → mechanism → example.** When the template is automatic,
   instinct only has to fill three slots instead of composing under pressure.

---

## Section A — The three decision axes (new material, not in decks 01–13)

### PD-01 · deterministic vs. probabilistic
**Front:** Your pre-commit verify check is a hook; your adversarial review is an agent. Defend the assignment — and say what breaks if you swap them. (Speak, 90 seconds.)
**Back (must hit):**
- Two placement questions: *Can code decide it?* and *Must it always fire?* Verify = yes/yes → hook. Review = no/no → agent.
- Mechanism, not cost: an agent-as-gate is **probabilistic enforcement** — a gate that fires 95% of the time isn't a gate. Token waste is the third reason, not the first.
- Review requires judgment (weighing, synthesizing findings into a verdict) — code can't decide it; and firing it on every commit = alarm fatigue, so it's invoked, not automatic.
- One-liner: "Hooks are compile-time checks, agents are code reviewers — you never make the type-checker optional, and you never make code review a blocking script on every keystroke."

### PD-02 · explicit vs. implicit
**Front:** In an agentic dev workflow, what deserves an explicit per-task instruction and what should live in the environment? What is the harness, in one sentence? (Speak, 60 seconds.)
**Back (must hit):**
- Explicit = typed per-task; implicit = lives in the environment (CLAUDE.md, hooks, file structure, tests — the model reads all of it as instruction).
- Be explicit only where intent isn't inferable (structure of work: fan-out, isolation, independence) or being wrong is expensive (constraints, bar-for-done).
- The harness is an **explicit→implicit compiler**: anything typed 3× gets encoded into the environment. Maturity isn't better prompting — it's an environment that needs less prompting.
- Example: CAPTURE→EXTRACT→PROMOTE loop *is* this compiler.

### PD-03 · shared vs. isolated context
**Front:** When do you delegate work to a subagent and when must it stay in the main thread? Use spec-writing and code search as your two poles. (Speak, 90 seconds.)
**Back (must hit):**
- The delegation question: *does the main thread need this context afterward, or need protecting from it?*
- Subagents = context **isolation**: only the report returns; a polluted main context degrades every later decision (searches, reviews, log dives → delegate).
- Spec-writing inverts it: its real product is the context it **loads** into the thread that implements. Delegating returns a document to a thread that learned nothing.
- Mechanical reason spec can't delegate: subagents are fire-and-forget — they **cannot ask the human questions mid-task**, and spec-writing is made of questions.
- Framing: agents are systems with memory budgets, not chatbots.

### PD-04 · verification bounds the loop
**Front:** "Explore → plan → code → commit" — what's the highest-leverage missing word, and why? (Speak, 60 seconds.)
**Back (must hit):**
- **Verify.** An agent loop's quality is bounded by its feedback signal.
- With a real verifier (tests, typecheck, running the app) the loop converges on *correct*; without one it converges on *plausible* — it stops when output looks right.
- Corollary: when no natural verifier exists, create one first (failing test, script, screenshot check), then let the loop run against it.
- Bridge: observability before trust — same heuristic, applied to the loop itself.

### PD-05 · when to be explicit about subagents
**Front:** How explicit do you need to be about invoking subagents, and when does explicitness pay? (Speak, 60 seconds.)
**Back (must hit):**
- Implicit for "find/fetch things" — the orchestrator decides fine on its own.
- Explicit when **the structure of the work is the point**, because intent about structure isn't inferable: (1) context isolation, (2) parallel fan-out over independent pieces, (3) independence/adversarial checks — a fresh agent can't rationalize reasoning it never saw.

---

## Section B — y30 adversarial set (backs are yours to fill)

Fill each back with your best post-rep articulation in claim/mechanism/example form.
Until filled, grade against the template only. Update the back whenever a rep produces a
better phrasing — the back is a cache, not an archive.

### PD-06 · FSM vs. LLM state manager
**Front:** Why FSM over a pure LLM state manager? What does that buy you at runtime?
**Back:**
- Claim:
- Mechanism:
- Example:

### PD-07 · STT latency degradation
**Front:** How do you handle latency spikes in the STT pipeline? What degrades gracefully?
**Back:**
- Claim:
- Mechanism:
- Example:

### PD-08 · eval setup + regression signal
**Front:** Walk me through your eval setup. What's your regression signal?
**Back:**
- Claim:
- Mechanism:
- Example:

### PD-09 · agent loop vs. LangGraph
**Front:** How does your agent loop compare to LangGraph's approach? Where is yours better?
**Back:**
- Claim:
- Mechanism:
- Example:

### PD-10 · rebuild from scratch
**Front:** What would you change if you rebuilt y30 from scratch?
**Back:**
- Claim:
- Mechanism:
- Example:

---

## Section C — Cross-deck production reframes

Same content as the referenced recall cards, drilled in production mode: speak the full
claim/mechanism/example before flipping to the source card.

### PD-11 · least autonomy (→ AO-03, AO-04)
**Front:** An interviewer asks: "How agentic should a production system be?" Answer with your default rule and y30 as the example. (Speak, 60 seconds.)

### PD-12 · promotion ladder (→ HC-03)
**Front:** "How do you keep an AI coding setup from repeating the same mistakes?" Answer with the promotion ladder, including what qualifies something for hook promotion. (Speak, 90 seconds.)

### PD-13 · untrusted content (→ IP-01, IP-02)
**Front:** "How do you safely feed untrusted content to an LLM?" Include the failure you actually hit. (Speak, 60 seconds.)

### PD-14 · obligatory retrieval (→ SL-02, SL-03)
**Front:** "Most AI memory systems don't work. Why? What makes yours compound?" (Speak, 90 seconds.)

### PD-15 · capstone — the 4-minute run
**Front:** Explain y30's architecture end-to-end in 4 minutes with accurate vocabulary. No reaching for intuition. (This is the Week 8 checkpoint criterion — attempt it early and fail informatively.)
**Back:** Grade against the Week 8 checkpoint list in SYLLABUS.md. Log stall points below the deck; each stall point is the next thing to formalize.

---

## Stall log

| Date | Card | Stall point (where speech went vague) | Fixed by |
| --- | --- | --- | --- |

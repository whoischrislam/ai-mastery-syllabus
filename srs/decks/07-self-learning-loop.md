# Deck 07 · Self-Learning Loop & Agent Memory

Source: built 2026-06-09 (the global Claude Code self-learning loop). Grounded in
Reflexion, MemGPT, Voyager. Theme: what makes agent memory actually *compound*
across sessions instead of rotting.

Card ID prefix: `SL`. Scheduling state lives in `../schedule.md`.

---

### SL-01 · the compounding requirement
**Front:** Three things a memory system needs before it actually compounds across sessions — name them.
**Back:** (1) structured, queryable **storage**; (2) **obligatory retrieval** (bound back into future decisions); (3) a **quality gate** before promotion. Break any one and the loop stays open — knowledge accumulates but never improves behavior.

### SL-02 · the keystone
**Front:** Of the three compounding requirements, which one does most "AI memory" skip — and what failure does that cause?
**Back:** **Obligatory retrieval.** Without a guaranteed read, storage becomes a write-only log nobody consults → it rots (the 161KB LEARNINGS.md). The fix: make retrieval **structural** (a hook), not **optional** (remembering to check).

### SL-03 · stored ≠ learned
**Front:** Why isn't "I saved it to a file" the same as the system having "learned" it?
**Back:** Learning requires the stored thing to **change future behavior**. Storage is necessary but inert; only retrieval-into-decisions closes the loop. *"Stored but not retrieved is not learning."*

### SL-04 · the five stages
**Front:** Name the 5 stages of the loop in order, and which handle single entries vs. aggregates.
**Back:** **Capture → Retrieve(review) → Extract → Validate → Promote.** Capture/Retrieve handle *individual* entries; Extract *aggregates* across entries; Validate grounds externally; Promote enforces.

### SL-05 · data point vs. signal
**Front:** What turns a pile of individual captured observations into "knowledge"?
**Back:** **Cross-time aggregation.** One observation is a data point; the *same* observation repeated is a signal. The extractor finds signals across accumulated points — and must *refuse* to fabricate signal from singletons. (Like log lines → an alert on threshold.)

### SL-06 · external grounding
**Front:** Why validate a candidate against an external source instead of promoting whatever recurred?
**Back:** To prevent **ossification** — a system that only learns from itself mistakes "this repeated" for "this is correct" and hardens its own habits. External signal is the reference that keeps it honest. (Cf. model collapse, echo chambers.)

### SL-07 · tombstones
**Front:** In the promotion state machine, what do `dismissed`/`deprecated` do that plain deletion wouldn't?
**Back:** They're **tombstones** — they remember rejection so the same candidate can't keep resurfacing every extraction run. Deletion would let it be re-proposed forever. This is what keeps the review queue from becoming noise.

### SL-08 · a named failure mode
**Front:** Name two named failure modes of agent-memory systems (with the one-line mechanism for one).
**Back:** Any two: **open loop** (capture w/o retrieval → never used), **shoebox problem** (accumulation w/o distillation → 400 unsorted bullets), **non-actionable entries** (no trigger/scope/target → can't enforce), **validation-cost blowup** (expensive API on every entry → unaffordable).

### SL-09 · automate vs. surface
**Front:** Why is capture automated in a background hook, but extraction/validation/promotion offered interactively at session start?
**Back:** Split by **consequence**. Capture MUST be automatic — an unrecorded session is lost forever. Extract/validate/promote are heavier and env-changing (API calls, writing rules), so they belong at the visible, human-present review moment. *"Automate the irreversible-if-skipped; surface the consequential."*

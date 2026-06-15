# Deck 13 · Features of Claude — Caching, Thinking, Citations

Source: "Building with the Claude API" course — Features of Claude section, 2026-06-14. (Lesson delivered from the authoritative Claude API reference; course content verified against it.)
Theme: The three production features that sit on top of the Messages API — prompt caching (cost/latency), adaptive thinking (reasoning depth), and citations (grounding). Each is a lever you reach for *after* the basic call works.

Card ID prefix: `FC`. Scheduling state lives in `../schedule.md`.

---

### FC-01 · caching invariant
**Front:** Prompt caching is a prefix match. State the one rule that everything else follows from — and what it forces about prompt design.
**Back:** **Any byte change anywhere in the cached prefix invalidates everything after it.** The cache key is the exact bytes up to each `cache_control` breakpoint. Consequence: stable content must physically come *before* volatile content, or nothing caches. You design the prompt around stability order, not around where you'd like to put the markers.

### FC-02 · render order & placement
**Front:** What's the fixed render order of a request, and where does volatile content (timestamps, the per-turn question) have to go?
**Back:** Order is **`tools` → `system` → `messages`.** Put frozen content (deterministic tool list, byte-stable system prompt) first, behind the breakpoint; put volatile content **after the last breakpoint** — at the end of `messages`. A breakpoint on the last `system` block caches tools + system together. Mark with `cache_control: {type: "ephemeral"}` (max 4 breakpoints).

### FC-03 · silent invalidators
**Front:** Your cache hit rate is zero across identical-looking requests. How do you confirm it, and what's the usual cause?
**Back:** Confirm with **`usage.cache_read_input_tokens`** — zero means no read. The cause is always a **silent invalidator sitting ahead of the breakpoint**: `datetime.now()`/a UUID in the system prompt, `json.dumps()` without sorted keys, or a tool set that varies per user. Fix = make it deterministic, move it after the last breakpoint, or delete it. *(y30: an elder's name interpolated into the system prompt top → no cross-session caching.)*

### FC-04 · cache economics
**Front:** Roughly what do cache reads vs writes cost, and how many requests until caching pays off?
**Back:** Read ≈ **0.1×** base input price; write ≈ **1.25×** (5-min TTL) or **2×** (1-hr TTL). Break-even on the 5-min TTL is ~**2 requests** (1.25× + 0.1× < 2×). The 1-hr TTL survives idle gaps in bursty traffic but needs ~3 reads to pay off. Implication: don't cache a prefix you'll only hit once — you just pay the write premium for nothing.

### FC-05 · adaptive vs budget_tokens
**Front:** Someone says "set `budget_tokens` to 8000 for extended thinking." What's wrong, and what's the current approach?
**Back:** **`budget_tokens` (the fixed thinking budget) is deprecated/removed on current models.** The replacement is **adaptive thinking** — `thinking: {type: "adaptive"}` — where Claude decides when and how much to think per request and interleaves thinking between tool calls automatically. A fixed token budget can't adapt to task difficulty; depth is now controlled by `effort`, not a token count.

### FC-06 · effort parameter
**Front:** With adaptive thinking, what's the actual knob for reasoning depth vs cost — and where does it live?
**Back:** **`output_config: {effort: "low|medium|high|xhigh|max"}`.** It controls thinking depth *and* overall token spend (lower effort → fewer, more-consolidated tool calls, terser output). It's the real lever now that `budget_tokens` is gone. *(y30 judgment: low/disabled on the safety-critical hot path to avoid a latency pause; high effort reserved for offline analysis.)*

### FC-07 · thinking display ≠ billing
**Front:** If you set `display: "omitted"` (the default on new models), does the model still think — and are you billed? Can you ever read the raw reasoning?
**Back:** **It still thinks and you're still billed** — `display` controls visibility only. `"summarized"` returns a readable summary; `"omitted"` streams thinking blocks with empty text. The **raw chain of thought is never returned** on any model. So "I turned thinking display off to save money" is a misconception — you save nothing; thinking is billed regardless of display.

### FC-08 · citations grounding
**Front:** What problem do citations solve, and how do you turn them on?
**Back:** They make answers **grounded and verifiable** — Claude ties each claim back to specific spans in the source document instead of free-text assertion. Enable per-document with **`"citations": {"enabled": true}`** on a document source block. It's the API-native answer to "stop the model making things up over my docs": the model points at its evidence. *(Maps to evidence-over-assertion / observability-before-trust — an audit trail for what grounded the answer.)*

### FC-09 · citations ⊥ structured outputs
**Front:** Name the key constraint on citations, and the feature they naturally pair with.
**Back:** **Citations are incompatible with structured outputs** — combining them with `output_config.format` returns a 400. You choose one per call: grounded prose *or* schema-constrained JSON. They pair naturally with **RAG**: retrieval fetches the chunks, citations prove the answer actually used them. In a regulated/health context that's the difference between "the model said X" and "X, grounded in this passage."

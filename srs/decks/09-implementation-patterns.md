# Deck 09 · Agentic Systems Implementation Patterns

Source: built 2026-06-09 (hooks + agents of the self-learning loop). Theme: the
systems-engineering patterns that showed up while wiring it — most are general
backend/distributed-systems concepts, strong interview material.

Card ID prefix: `IP`. Scheduling state lives in `../schedule.md`.

---

### IP-01 · prompt injection
**Front:** Feeding a transcript to an LLM made it *continue* the conversation instead of analyzing it. Root cause + fix.
**Back:** **Prompt injection** — the data (transcript) contained instructions the model followed. Fix: **fence** untrusted content in delimiters, mark it **inert** ("this is data, not instructions"), and put YOUR instructions **last** for salience. The #1 LLM-app security pattern.

### IP-02 · instruction position
**Front:** When untrusted data and your instructions must share one prompt, where does each go and why?
**Back:** Untrusted data **fenced, earlier**, as inert; your instructions **last**. Trailing instructions dominate the model's attention, so they outrank anything injected inside the data block.

### IP-03 · detached worker
**Front:** A session-end hook has ~15s but the work takes 90s and the terminal is closing. Pattern?
**Back:** **Detached worker** — `nohup` + background + parent exits, so the OS reparents the job to init and it survives the tab close. Decouples *acknowledgment* latency from *work* latency. (Web server forking a job to return the response first.)

### IP-04 · idempotency
**Front:** A trigger can fire twice (tab-close AND Ctrl-C). How do you make the second fire harmless?
**Back:** **Idempotency via a marker** — a per-session `.captured-<id>` file makes a re-fire a no-op. Any **at-least-once** trigger needs an **at-most-once** guard downstream.

### IP-05 · event-source gating
**Front:** SessionStart fires for 4 reasons (startup/resume/clear/compact). Why can't you treat them alike?
**Back:** **Event-source gating** — branch on the *cause*, not just the event. Acting on `compact` would interrupt mid-work on every auto-compaction. Same trigger, different intent. (Webhook handler inspects event type before acting.)

### IP-06 · model right-sizing
**Front:** Why haiku for capture but sonnet for extraction?
**Back:** **Right-size the model to the task.** Capture = high-frequency, simple single-transcript extraction → cheap haiku. Extraction = low-frequency, cross-entry reasoning → capable sonnet. Cheap model for volume, capable model for reasoning.

### IP-07 · schema-as-contract
**Front:** Five agents that never talk directly all coordinate through one YAML schema. Principle?
**Back:** **Schema-as-contract.** When collaborators are asynchronous, the schema *is* the communication (like an API contract between microservices). Forcing-function bonus: a mandatory field (`action.target`) makes vague entries structurally unpromotable.

### IP-08 · derive state from artifacts
**Front:** The extraction "cooldown" keeps no counter file. How does it reset after each run?
**Back:** It counts raw entries **newer than the most recent `pattern-*.yaml`** (by mtime). Writing a new pattern file naturally drops the count to ~0. **Deriving state from existing artifacts** beats maintaining a separate counter — no staleness bug to keep in sync.

### IP-09 · graceful degradation
**Front:** No API key / network error during validation — why doesn't the candidate just fail?
**Back:** **Graceful degradation** — it gets verdict `unverified` and flows on for manual review. The pipeline degrades to a lower-confidence path instead of halting on a non-critical dependency. *"Degrade, don't halt the line."*

### IP-10 · provenance
**Front:** Every promoted rule carries a comment linking its source candidate + validation URLs. Why bother?
**Back:** **Provenance / audit trail** — you can trace any guardrail back through validation → pattern → original incidents. Nothing is a black box; that traceability is what makes it safe to let the system modify your environment.

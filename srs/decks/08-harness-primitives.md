# Deck 08 · Harness Primitives, Config & Promotion

Source: built 2026-06-09 (global Claude Code toolkit). Theme: the config/enforcement
primitives, how scope and layering work, and how a learning climbs from passive
prose to automatic enforcement.

Card ID prefix: `HC`. Scheduling state lives in `../schedule.md`.

---

### HC-01 · the primitives decision
**Front:** The one question that decides whether something should be a hook vs. a rule vs. an agent.
**Back:** *"Should this happen automatically without me asking?"* Yes → **hook** (enforce). Needs a specialist's isolated context → **agent**. Every session should just know it → **rule/CLAUDE.md**. (Rules inform, hooks enforce, skills execute, agents specialize, workflows orchestrate.)

### HC-02 · narrowest scope
**Front:** The default rule for *where* a rule/config should live — and the cost of getting it wrong.
**Back:** **Use the narrowest scope that works.** Over-globalizing costs tokens in every session of every repo, adds context pressure (→ early compaction → quality loss) and latency. (Same shape as CSS / Git config / IAM scoping.)

### HC-03 · the promotion ladder
**Front:** The 3 rungs a learning climbs from passive → automatic, and what earns the top rung.
**Back:** **Prose rule → path-scoped rule → enforced hook.** A rule earns a hook only when it's **deterministic AND (high-cost OR frequently violated)**. Same maturity curve as manual runbook → script → CI/CD gate.

### HC-04 · merge vs. override
**Front:** In layered config (global + repo), which fields merge and which override?
**Back:** **Array** fields (hooks, permissions) **concatenate + dedupe** across layers — both fire. **Scalar** fields (model, theme) → **highest-precedence layer wins**. Knowing the difference prevents hours of "why is this firing" debugging.

### HC-05 · blast radius governs autonomy
**Front:** Why does the PROMOTE agent write rules automatically but only *stage* hooks (never auto-register)?
**Back:** **Blast radius governs autonomy.** A rule is low-blast (text in context). A buggy hook fires on every tool call and can block *all* work — high-blast. The more damage an action can do, the more human gating it gets. (Deployment rings, canary, `terraform plan`→`apply`.)

### HC-06 · advisory vs. authority
**Front:** The validator annotates but never promotes; the human promotes. Name that boundary and why keep it.
**Back:** **Advisory vs. authority.** Keep the machine advisory (flags, suggests) and the human authoritative (decides, applies) for consequential/irreversible actions. (Linter flags vs. a required CI gate.) Preserves trust and a human gate where it matters.

### HC-07 · progressive defaults
**Front:** The principle behind "silent background capture by default; immediate review only if you opt in."
**Back:** **Progressive defaults** — design for the user's *most common* state, make the exception easy to reach (not the default). (iPhone silent switch, Git branch defaults.)

### HC-08 · HITL load
**Front:** Two UX rules that make a human-in-the-loop review actually get *used* instead of abandoned.
**Back:** (1) **Cap choices** — surface ≤3 at a time (decision fatigue). (2) **Conversational prose over codes** — humans process narrative in fewer cognitive steps (cognitive load / progressive disclosure).

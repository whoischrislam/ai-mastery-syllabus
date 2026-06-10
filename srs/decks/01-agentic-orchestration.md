# Deck 01 · Agentic Orchestration

Source: Lesson 1 (Claude, 2026-06-08), grounded in Anthropic's *Building Effective Agents*.
Theme: the workflow↔agent spectrum, the 5 canonical patterns, and how each maps onto y30
(FSM for flow, LLM for phrasing).

Card ID prefix: `AO`. Scheduling state lives in `../schedule.md`.

---

### AO-01 · definition
**Front:** Workflow vs. agent — what's the one structural difference?
**Back:** Who owns control flow. **Workflow** = LLM calls orchestrated through *predefined code paths* (you decide the steps). **Agent** = the LLM *dynamically directs its own process*, choosing tools/next-steps in a loop from environmental feedback.

### AO-02 · the axis
**Front:** Name the single tradeoff axis that runs prompt-chaining → full agent.
**Back:** **Autonomy vs. reliability.** Moving right buys flexibility & capability; you pay in predictability, cost, latency, eval-ability, and error-compounding.

### AO-03 · the judgment principle
**Front:** What's the Staff-level default when deciding how "agentic" to build something?
**Back:** **Use the least autonomy that solves the problem.** Start with a workflow; spend autonomy only where dynamic decision-making is the actual value. Most production "agents" should be workflows.

### AO-04 · y30 mapping
**Front:** In y30's vocabulary, which layer is the "workflow" and which is the bounded-autonomy "agent" use — and why that split?
**Back:** **FSM = workflow layer** (deterministic flow control — safety-critical for elders, you *want* predictability). **LLM = scoped to phrasing inside a state** (bounded autonomy, lowest-risk place to spend the model). "A workflow that rents autonomy by the sentence."

### AO-05 · prompt chaining
**Front:** Pattern: decompose into a fixed sequence, each call consumes the prior output, optional gates between steps. Name it + the core tradeoff.
**Back:** **Prompt chaining.** Trades **latency for reliability/accuracy**. Gates let you validate intermediate output before continuing.

### AO-06 · routing
**Front:** Pattern: classify the input, then dispatch to a specialized handler. Name it + why bother.
**Back:** **Routing.** Separation of concerns — each path is optimized for its input class instead of one bloated prompt handling everything. (y30: provider fallback; intent → FSM state.)

### AO-07 · parallelization (two flavors)
**Front:** Parallelization has two distinct flavors. Name both and what each is *for*.
**Back:** **Sectioning** — split into *independent* subtasks run concurrently (speed / separable work). **Voting** — run the *same* task N times for confidence/diversity, then aggregate.

### AO-08 · orchestrator-workers
**Front:** Pattern: a central LLM decomposes the task *at runtime* and delegates to workers, then synthesizes. Name it.
**Back:** **Orchestrator-workers.** The orchestrator (model) decides the subtasks dynamically based on the input.

### AO-09 · THE distinction
**Front:** Parallelization-sectioning vs. orchestrator-workers — both fan out. What single bit decides which it is?
**Back:** **Who decides the subtasks.** Predefined by *you* → sectioning. Decided by the *model* at runtime → orchestrator-workers. That bit is the autonomy/reliability tradeoff showing up at the structural level.

### AO-10 · evaluator-optimizer
**Front:** Pattern: one LLM generates, another critiques against a rubric, loop until it passes. Name it + where it already lives in y30.
**Back:** **Evaluator-optimizer.** y30's **LLM-judge eval pipeline** is the evaluator half of this loop.

### AO-11 · the trap (application)
**Front:** A post-session pipeline runs a *fixed* scoring step + summary step + flag-for-review step. Orchestrator-workers or parallelization-sectioning? Why?
**Back:** **Parallelization-sectioning.** The three subtasks are *predefined by you*, not chosen by a model at runtime. It only becomes orchestrator-workers if a model decides *which* subtasks to spawn per session.

### AO-12 · failure modes
**Front:** Name two things that measurably get *worse* as you add agent autonomy — and the mechanism for one.
**Back:** Any two of: **cost, latency, non-determinism, error-compounding.** Mechanism (compounding): each step conditions on the prior output, so an early error propagates and amplifies; per-step success multiplies (≈0.95ⁿ), so reliability decays with loop length.

### AO-13 · when an agent earns it
**Front:** When is a workflow the *wrong* choice and a real agent genuinely worth the cost?
**Back:** When you **can't predefine the steps** — the path varies per input, the task needs flexible model-driven decisions at scale, *and* you can tolerate the cost/latency/variance. Otherwise prefer the workflow.

### AO-14 · contracts
**Front:** What's the main thing that keeps a multi-agent system from drifting into chaos?
**Back:** **Explicit contracts between agents** — defined input/output schemas (structured output), so every handoff is *validated, not vibes*. Coordination cost rises with agent count; contracts bound it.

### AO-15 · cost framing
**Front:** Cost intuition for multi-agent vs. single-agent, and the implication?
**Back:** Multi-agent **multiplies token spend** — each agent carries its own context, so fan-out can cost many× a single chat. Implication: reserve fan-out for tasks where **parallel breadth** or **independent verification** actually pays for the tokens.

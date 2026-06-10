# Deck 11 · Agents & Workflows — Implementation Patterns

Source: "Building with the Claude API" course — Agents and Workflows section, 2026-06-10.
Theme: Implementation-level details of the 5 patterns. Deck 01 covers the concepts; this deck covers how you actually build them in code.

Card ID prefix: `AW`. Scheduling state lives in `../schedule.md`.

---

### AW-01 · chaining gate
**Front:** In a prompt chain, what is a gate and what does it protect against?
**Back:** A **gate** is a validation check on a step's output before passing it to the next step. If the output fails (wrong format, missing fields, below quality threshold) you abort, retry, or redirect — not blindly forward. Gates are what make chaining reliable. A chain without gates is optimistic serial execution.

### AW-02 · parallelization in code
**Front:** What's the implementation tool for parallel LLM calls, and what does that imply for wall-clock time?
**Back:** `asyncio.gather()` (Python) or `Promise.all()` (JS) — fire concurrent requests simultaneously. Wall-clock time = **slowest single call**, not the sum of all calls. This is why parallelization buys time: you pay the cost of the longest task, not all tasks combined.

### AW-03 · routing classifier
**Front:** In a routing workflow, what does the first call do and why should it be as cheap as possible?
**Back:** The first call is a **classifier** — a cheap, fast call (small model, regex, or keyword match) that returns a category. Based on that category you dispatch to the specialized handler. It should be lightweight because it runs on **every request** — classifier latency/cost multiplies across all traffic.

### AW-04 · environment inspection
**Front:** What should an agent do before taking any write/modify/delete action — and what principle does this connect to?
**Back:** **Inspect the current state first** — read the file before editing, check what exists before creating, query the current value before updating. Prevents acting on stale assumptions or overwriting something important. Connects to the reversibility principle (CA-06): you can't prefer a reversible action if you don't know what's already there.

### AW-05 · workflow vs. agent in code
**Front:** At the code level, what's the structural difference between a workflow and an agent?
**Back:** **Workflow:** *you* write the control flow — `if/else`, `for` loops, function calls. The model is called at fixed points you defined. **Agent:** the model's output determines what happens next — you have a runtime loop, and the model's response (tool call or `end_turn`) drives the next iteration. Your code is a **runtime**, not a script.

# Deck 03 · Claude API — Agents & Workflows

Source: "Building with the Claude API" course (first 1/3), 2026-06-10.
Theme: API implementation layer — tool use mechanics, the agentic loop, agent safety principles, context management. Deck 01 covers the conceptual patterns; this deck covers how you actually build them.

Card ID prefix: `CA`. Scheduling state lives in `../schedule.md`.

---

### CA-01 · tool definition
**Front:** What are the three fields of a tool definition, and which one does Claude use to decide *when* to call it?
**Back:** `name` (machine ID), `description` (when/why to call it — **most important**), `input_schema` (JSON Schema for arguments). Claude reads the description to decide whether the tool fits the situation; a weak description means wrong or missed calls.

### CA-02 · tool use response
**Front:** When Claude wants to use a tool, what does the response look like — stop_reason and content?
**Back:** `stop_reason: "tool_use"`. Content includes a block of `type: "tool_use"` with three fields: `id` (unique call ID), `name` (which tool), `input` (the arguments Claude chose). You act on this; it's not a final answer.

### CA-03 · tool result format
**Front:** After you execute a tool, how do you feed the result back to Claude?
**Back:** Append a `"tool_result"` content block keyed by `tool_use_id` (matches the `id` from CA-02) with `content` (the result string or structured data) and optionally `is_error: true` if execution failed. This becomes the next user turn.

### CA-04 · agentic loop
**Front:** The agentic loop has two exit outcomes from the model. What are they and what do you do with each?
**Back:** `stop_reason: "end_turn"` → model is done, return the response. `stop_reason: "tool_use"` → execute the tool(s), append assistant turn + tool_result user turn, loop again. You own execution; the model owns when to stop.

### CA-05 · minimal footprint
**Front:** Minimal footprint principle — define it and the rule it implies for permissions.
**Back:** Request only the permissions the *current task* needs. Don't pre-acquire broad access "just in case." Scope narrowly; ask for more only when you actually need it. Limits blast radius if the agent misbehaves or is hijacked.

### CA-06 · reversibility preference
**Front:** Two actions solve the problem equally well — one is reversible, one isn't. What's the rule, and what does it imply for ambiguous high-stakes actions?
**Back:** **Prefer the reversible path.** Don't delete when you can archive; don't overwrite when you can version. For ambiguous high-impact irreversible actions: **pause and confirm with the human** before proceeding. Autonomy is not worth an unrecoverable mistake.

### CA-07 · prompt injection in agents
**Front:** Why are tool results a security concern, and what's the threat called?
**Back:** **Prompt injection.** A malicious web page, document, or API response can embed instructions ("ignore previous instructions and…") that the model treats as legitimate direction. Tool results are untrusted input, not safe prompts — the model can be fooled. Your architecture must assume this, not rely on the model to resist it.

### CA-08 · context accumulation
**Front:** Why do long-running agents hit context limits, and what are the three strategies to handle it?
**Back:** Every loop iteration appends tool calls + results to the message array — context grows unboundedly. Three strategies: **truncate** old turns (lose history), **summarize** intermediate state (compress history), **externalize state** into a structured schema (discard conversation, keep only what matters). Choice depends on whether the agent needs full history or just current state.

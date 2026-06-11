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

### CA-09 · tool description quality
**Front:** A tool description should cover four things — what are they?
**Back:** (1) What the tool does, (2) when Claude should use it, (3) what it returns, (4) detailed descriptions for each argument. Missing any one causes misfires — Claude either calls the wrong tool, calls it at the wrong time, or passes wrong arguments.

### CA-10 · required array
**Front:** In a tool's `input_schema`, what does the `required` array control?
**Back:** Which parameters Claude *must* provide when calling the tool. Listed in `required` → Claude cannot omit them. Absent from `required` → optional. Empty `required: []` → everything optional. Controls whether Claude can call the tool with missing critical inputs.

### CA-11 · multi-block preservation
**Front:** When appending an assistant tool-use response to message history, what must you preserve — and what breaks if you don't?
**Back:** Save `response.content` (all blocks — text + tool_use), not just the text block. If you drop the ToolUse block, the next call arrives with a tool_result in history but no record of Claude having requested it — breaks the conversation. The API is stateless; you own the full history.

### CA-12 · is_error on failure
**Front:** A tool throws an error during execution. What do you do — and why?
**Back:** Still send back a `tool_result` with `is_error: true` and the error message as content. Never leave Claude waiting with no response — it's blind to your server. Claude reads the error and can handle it gracefully: retry, explain to the user, or choose a different approach.

### CA-13 · tool routing
**Front:** How do you scale a system to handle many tools without changing the core loop?
**Back:** A **tool router** — a dispatcher that maps tool names to functions (`if name == "x": call x()`). The agentic loop never changes; you just add entries to the router. Keeps core logic stable as tool count grows.

### CA-14 · loop condition
**Front:** What exact field and value tells you to keep the agentic loop running vs. stop?
**Back:** `stop_reason == "tool_use"` → keep going (execute tools, feed results back, loop). Anything else (usually `"end_turn"`) → Claude is done, return the response. This single check drives the entire loop — Claude owns when it stops.

### CA-15 · built-in tools
**Front:** What makes built-in tools (text editor, web search) different from custom tools?
**Back:** Claude already knows the schema — you only provide a small version stub; Claude expands it internally. But you still implement the execution layer. Schema is Claude's responsibility; execution is yours. Same pattern as custom tools, just Claude brings the definition.

### CA-16 · allowed_domains
**Front:** What does `allowed_domains` do in the web search tool, and why does it matter for health applications?
**Back:** Restricts searches to specific domains only (e.g., `nih.gov`). Prevents Claude from citing random blogs or unreliable sources. For health applications like y30: lock queries to authoritative medical sources (NIH, Mayo Clinic) to maintain trust and accuracy with vulnerable users.

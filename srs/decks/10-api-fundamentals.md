# Deck 10 · Accessing the Claude API — Fundamentals

Source: "Building with the Claude API" course — Accessing Claude with the API section, 2026-06-10.
Theme: The stateless API model, messages structure, system prompts, temperature, streaming, structured output. Foundational mechanics that everything else (tool use, agents, RAG) builds on.

Card ID prefix: `AB`. Scheduling state lives in `../schedule.md`.

---

### AB-01 · statefulness
**Front:** Does the Claude API remember previous conversations? What does that imply for multi-turn?
**Back:** **No — the API is stateless.** Every call is isolated. To maintain a conversation, you pass the full conversation history as the `messages` array on every single request. You own state; the API owns nothing between calls.

### AB-02 · messages array
**Front:** Two structural rules for the messages array — what are they?
**Back:** (1) **First message must be `user`.** (2) **Roles must strictly alternate** (`user` → `assistant` → `user` → …). Violating either causes an API error. This is how multi-turn state is represented — you reconstruct the full history on every call.

### AB-03 · system prompt
**Front:** Where does the system prompt live in an API call — and what does it do?
**Back:** It's a **separate `system` parameter**, not inside the messages array. Sets persona, constraints, and persistent context. The model sees it on every turn even though it's invisible to the messages history. Scope: applies to the whole conversation, not a single turn.

### AB-04 · temperature
**Front:** What does temperature control, what's the range, and when do you go low vs. high?
**Back:** Controls **randomness**. Range 0–1. **Low (→0):** near-deterministic — use for factual tasks, code, structured output where consistency matters. **High (→1):** more varied and creative — use for brainstorming, writing. Most production tasks run 0–0.5.

### AB-05 · streaming
**Front:** What does streaming change about how you receive a response — and what's the actual benefit?
**Back:** Delivers tokens **as they're generated** (server-sent events) instead of waiting for the full response. Total generation time is the same either way. The benefit is **perceived latency** — users see output immediately instead of waiting for a complete reply. Critical for conversational UX.

### AB-06 · structured output
**Front:** Two approaches to get structured JSON from Claude — which is the production approach and why?
**Back:** (a) **Prompt-based:** instruct Claude to respond in JSON — works but unreliable at scale (model can drift). (b) **Tool-forced:** define a tool with the target schema, use `tool_choice` to force Claude to call it — produces **guaranteed valid JSON** because the model must conform to the schema. Option (b) is the production approach.

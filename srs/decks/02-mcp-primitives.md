# Deck 02 · MCP Primitives

Source: "Introduction to Model Context Protocol" Skilljar course, 2026-06-10.
Theme: The three MCP primitives (tools, resources, prompts), how MCP differs from custom tool use, and when to use each primitive.

Card ID prefix: `MC`. Scheduling state lives in `../schedule.md`.

---

### MC-01 · three primitives
**Front:** Name the three MCP primitives and one sentence each for what they do.
**Back:** **Tools** — actions Claude can take (write, fetch, execute). **Resources** — read-only data injected as context. **Prompts** — pre-built, tested instruction templates users can trigger. Tools *do* things; resources *read* things; prompts *start* things.

### MC-02 · tools vs resources
**Front:** An elder's care plan needs to be available to Claude. Tool or resource — which and why?
**Back:** **Resource.** Resources are for read-only data that gets injected as context. Tools are for actions (write, modify, execute, cause side effects). Care plan is read-only context, not an action. Rule: needs to *do* something → tool. Needs to *read* something → resource.

### MC-03 · MCP message types
**Front:** Two core MCP message types — what does each do?
**Back:** **ListToolsRequest/Result** — client asks server "what tools do you have?" Gets back the available list. **CallToolRequest/Result** — client asks server to run a specific tool with given args, gets back the result. Everything else in MCP is built on these two exchanges.

### MC-04 · transport agnostic
**Front:** What does "transport agnostic" mean for MCP, and what are the common options?
**Back:** MCP client and server can communicate over different protocols — **stdio** (same machine, most common), **HTTP**, **WebSockets**. The protocol layer is swappable without changing application logic. Lets you run MCP servers locally or remotely with the same interface.

### MC-05 · MCP prompts
**Front:** Why define prompts in an MCP server instead of letting users write their own?
**Back:** You invest time crafting and testing prompts that work consistently. Users get expert-quality results without becoming prompt engineers. Pre-built prompts encode domain expertise — `/weekly_summary`, `/care_plan_review` — tasks too complex to reliably prompt from scratch. Update once, all clients benefit.

### MC-06 · MCP vs custom tools
**Front:** When do you use an existing MCP server vs. building a custom tool?
**Back:** **MCP server exists** → connect and move on; someone else wrote and maintains the integration. **No MCP server** (like Perplexity) → build and maintain the tool yourself. Check for MCP first. Custom tools are the fallback when no MCP alternative exists — not the default.

# Deck 04 · Evals (Your AI Product Needs Evals)

Source: Hamel Husain — "Your AI Product Needs Evals" (hamel.dev/blog/posts/evals), read 2026-06-13.
Theme: Evaluating *is* the work; prompting is one tool. The three-level eval system (unit tests → human/model eval → A/B), LLM-as-judge with alignment, error analysis, and the data flywheel. Framed for interviews — each card's "apply" side anchors to y30.

Card ID prefix: `EV`. Scheduling state lives in `../schedule.md`.

---

### EV-01 · what evals actually buy you (the velocity reframe)
**Front:** For an AI product, what does an eval system change about how you ship — stated as a one-line reframe?
**Back:** It turns **velocity** into "how fast you can *safely change behavior with feedback*," not "how fast you can ship prompts." Evals convert vibes-based prompt-poking into an engineering loop: test → change → re-run. The interview soundbite: *evaluating is the work; prompting is just one of the tools.* The payoff is **risk-bounded change** — you can edit a prompt or swap a model and know whether you broke something critical.

### EV-02 · the three-level model (the napkin drawing)
**Front:** Name the three concentric levels of evaluation and the axis they trade along.
**Back:** **L1 — unit tests** (fast, cheap, automated, inner loop). **L2 — human & model eval** (slower, higher fidelity, read traces + LLM-as-judge). **L3 — A/B testing** (slowest, real usage, business outcomes). The axis is **cost/speed vs. fidelity**: cheap deterministic checks at the center, expensive real-world signal at the edge. You build them outward — start at L1, only reach L3 once you have live traffic.

### EV-03 · what a Level-1 test is (and the scoping rule)
**Front:** What is a Level-1 eval, and what's the rule for scoping one?
**Back:** An **assertion about behavior** checked automatically on every change — "AI pytest." Scope it **by feature + scenario, not by "the whole assistant."** (Hamel's Listing Finder: scenarios = one result / many / none, assertion on result-set size.) Always include generic safety/format assertions too: output JSON parses, no PHI leaks, no raw IDs. Track pass-rate over time in CI — you don't need 100%, you need **visibility**.

### EV-04 · generating test inputs with an LLM
**Front:** How do you get enough Level-1 test cases without hand-writing them, and why does this work?
**Back:** Ask an LLM to generate scenario-targeted inputs: *"write 50 different instructions a caregiver might give about tracking Mrs. Tanaka's medication adherence."* It works because the bottleneck in L1 isn't the *assertion* (cheap to write) — it's **coverage of the input space**. The LLM cheaply fans out across phrasings and edge cases you'd never enumerate by hand. Save them in the repo as a fixture.

### EV-05 · error analysis (the trace-review ritual)
**Front:** What is the Level-2 "look at traces" practice, and what's Hamel's stop heuristic?
**Back:** Log full traces (utterance → tools/steps → retrieved context → final response), sample 20–30, label each, and write down failure modes. It's **design crit for AI behavior**. Recurring issues become new L1 assertions, prompt changes, or data fixes (e.g. bad RAG chunking). **Stop heuristic:** when you're no longer seeing *new* failure patterns. This is where you learn whether the **eval** is weak or the **model** is weak.

### EV-06 · LLM-as-judge + the alignment step
**Front:** How do you use a model to auto-score traces — and what's the keystone step people skip?
**Back:** Use a strong model as a **critic** that outputs good/bad + a short rationale. The keystone is **alignment**: periodically check the critic's verdicts against your *own* hand labels and tune the critic prompt until it agrees with you. A judge you haven't aligned is just another unvalidated model — its scores are vibes wearing a number. The senior model is your *junior reviewer*, not an oracle.

### EV-07 · binary labels first
**Front:** When labeling traces, why start with good/bad instead of a 1–5 scale?
**Back:** **Minimum-information / decision-driven.** A binary label forces a clear judgment, makes inter-rater agreement (and judge alignment, [[EV-06]]) measurable, and is enough to gate a change. Rich scales add noise and disagreement before they add signal. Only move to a richer scale when a real decision actually needs the granularity — not before.

### EV-08 · Level-3 metrics (and when to reach for it)
**Front:** What kind of metrics belong at Level 3, and when is L3 the right tool?
**Back:** **Product/business outcomes, not academic scores** — medication-confirmation rate, time-on-task, caregiver error reports, protocol adherence. *Not* BLEU. Reach for L3 only when you have **real usage** and care about behavior change in the wild; use controlled rollouts to confirm a new prompt/model improves outcomes **without raising safety incidents.** It's product experimentation applied to AI behavior — slow and expensive, so it's the last ring.

### EV-09 · the data flywheel
**Front:** Beyond gating changes, what asset does an eval system produce — and what does that asset feed?
**Back:** It turns messy conversation logs into a **labeled dataset**. That asset feeds three things: **regression tests** (lock in fixed bugs), **fine-tuning data** (labeled good/bad examples), and **debugging** (traceability — when a bad output ships, you can trace *why*: prompt, model, or data, and show the fix in eval history). The eval system compounds: every trace you review makes the next change safer.

### EV-10 · the judgment rule (evals before prompts)
**Front:** When an AI feature "feels off," what's the disciplined first move — and why?
**Back:** **Improve the evals first, then the prompt.** A felt-wrong output without a failing test means your eval system has a blind spot — patching the prompt blind just moves the problem. Codify the failure as an assertion or a trace label, *then* fix the behavior, so the fix is measured and can't silently regress. Corollary: **eval UIs are first-class product surfaces**, not internal afterthoughts — the trace viewer is where this judgment actually happens.

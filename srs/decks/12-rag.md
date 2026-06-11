# Deck 12 · Retrieval Augmented Generation (RAG)

Source: "Building with the Claude API" course — RAG and Agentic Search section, 2026-06-10.
Theme: When and why to use RAG, chunking strategies, embeddings, semantic vs. lexical search, hybrid search, and result merging.

Card ID prefix: `RG`. Scheduling state lives in `../schedule.md`.

---

### RG-01 · what RAG solves
**Front:** What problem does RAG solve, and what's the core tradeoff?
**Back:** Documents too large to fit in a prompt. RAG chunks the document, indexes the chunks, retrieves only relevant ones at query time. **Tradeoff:** simplicity (stuff it all) vs. scalability (chunk + retrieve). Stuffing works until the document is too big, too expensive, or too slow — RAG solves all three at the cost of a preprocessing step.

### RG-02 · chunking strategies
**Front:** Four chunking strategies — name them and the decision rule for choosing.
**Back:** **Structure-based** (best quality, requires controlled doc format — headers, sections), **sentence-based** (good middle ground for most text), **semantic-based** (best results, computationally expensive), **size-based with overlap** (production default — works with any document type). Decision rule: use structure-based when you control the format; size-based with overlap otherwise.

### RG-03 · chunking overlap
**Front:** What is overlap in chunking and what problem does it solve?
**Back:** Including some content from neighboring chunks at each boundary. Solves **context loss** — without overlap, a thought split across two chunk boundaries loses meaning. Overlap ensures complete ideas stay intact across chunk edges. Critical for size-based chunking where splits are arbitrary.

### RG-04 · embeddings
**Front:** What is a text embedding, and what makes two embeddings "similar"?
**Back:** A list of numbers representing the *meaning* of text. Similar meaning = similar numbers (vectors pointing in the same direction). The dimensions aren't human-interpretable — the model learned them during training. You compare vectors mathematically; you don't need to understand what each number represents.

### RG-05 · cosine similarity
**Front:** What does cosine similarity measure in RAG, and what do the values mean?
**Back:** The angle between two vectors in meaning-space. **1 = identical meaning**, **0 = unrelated**, **-1 = opposite**. Cosine *distance* = 1 − cosine similarity (lower distance = more similar). Vector databases use this to return the most relevant chunks for a query.

### RG-06 · hybrid search
**Front:** Why isn't semantic search alone enough — and what's the fix?
**Back:** Semantic search misses exact term matches (specific IDs, names, medical terms) because it searches by meaning, not keywords. Fix: **hybrid search** — run semantic (embeddings) + lexical (BM25) in parallel, merge results. BM25 weights rare terms highly and nails exact matches; semantic finds conceptual relevance. Combined covers both failure modes.

### RG-07 · reciprocal rank fusion
**Front:** Why can't you combine semantic and BM25 scores directly — and what's the solution?
**Back:** They use different scoring scales — raw scores aren't comparable across methods. Solution: **reciprocal rank fusion** — use *rank position* instead of raw scores. A chunk ranked #1 in both methods scores highest regardless of actual numbers. Rank-based merging normalizes across different systems.

### RG-08 · RAG for y30
**Front:** Where does RAG apply in y30 — and what's the trigger to implement it?
**Back:** Elder session history, care plans, caregiver notes — corpus too large to stuff into every prompt. RAG retrieves only relevant logs when a caregiver asks a question about a specific elder. **Trigger:** when accumulated data exceeds prompt limits or makes calls expensive/slow. Not needed yet; becomes obvious when real users accumulate history.

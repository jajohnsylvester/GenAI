# API & Product FAQ

Answers cross-cutting exam vs production questions. Distinguishes **exam guide content** (Feb 2025, v0.1) from **current production API** behavior.

---

## Is prompt prefilling deprecated?

**Production (2025–2026):** Yes, for modern Claude models. **Assistant message prefilling** (starting the assistant turn with e.g. `{`) returns **HTTP 400** on Opus 4.6+, Sonnet 4.5+, and related models.

**Exam guide:** Teaches structured output via **`tool_use` + JSON schema** and `tool_choice` (Tasks 4.3–4.4, pp. 17–18) — not prefilling.

### What to use instead

| Goal | Recommended approach |
|------|---------------------|
| Guaranteed JSON answer shape | `output_config.format` with `type: "json_schema"` ([Structured outputs](https://docs.anthropic.com/en/docs/build-with-claude/structured-outputs)) |
| Structured data in agent loop | `tool_use` with `strict: true` on tool `input_schema` |
| Force a specific extraction tool | `tool_choice: {"type": "tool", "name": "extract_metadata"}` |
| Classification label | Tool with enum schema or structured outputs |

### Are stop sequences deprecated?

**No.** `stop_sequences` remains a valid Messages API parameter. It sets custom strings that yield `stop_reason: "stop_sequence"`. The exam focuses on agentic loops using **`stop_reason: "tool_use"` vs `"end_turn"`** (Task 1.1), not prefilling.

### Best practices beyond the exam guide

1. **`output_config.format`** for extraction pipelines where the final artifact is JSON (replaces prefill-for-JSON pattern).
2. **`strict: true`** on tools when parameters must validate.
3. **Validation-retry loop** (Task 4.4) for semantic errors strict mode cannot catch.
4. **Do not** rely on assistant prefills on newer models — migrate before model upgrades.


---

## Is `/memory` deprecated?

**Exam guide (Task 3.1, p. 11–12):** `/memory` is **in scope** — use it to **verify which memory files are loaded** and diagnose inconsistent behavior across sessions.

**Current Claude Code:** Persistent project context is primarily via:
- **CLAUDE.md hierarchy** (user / project / directory)
- **`.claude/rules/`** path-scoped rules
- **Skills** (`.claude/skills/`)
- **Project memory** files (evolving product surface — check current [Claude Code docs](https://docs.anthropic.com/en/docs/claude-code))

**For the exam:** Know `/memory` as a **diagnostic** command. Alternatives for *storing* standards: project `CLAUDE.md`, `@import`, rules files (Task 3.1 in the official exam guide).

---

## Batch API FAQ (Task 4.5)

### What does "no guaranteed SLA" mean?

The Message Batches API processes asynchronously with a **processing window of up to 24 hours**. Anthropic does **not** guarantee completion within a fixed latency (unlike synchronous API). Most batches finish faster, but you must design for worst case.

### Does Batch API support tool calling?

**Exam guide (p. 18–19):** States batch **does not support multi-turn tool calling within a single request** — cannot execute tools mid-request and feed results back in the same batch entry.

**Production nuance (2026 docs):** Batch supports tools and server-side agentic loops for **server tools**, with `pause_turn` continuation patterns. **Client-side MCP tool loops** (your app executes tool, returns result, model continues) still require **multiple requests** — often separate batch entries or sync calls.

**Mitigation for extraction pipelines:**
1. **Single-shot extraction** — one request, one structured response (no loop).
2. **Pre-process** documents before batch (chunk, OCR, metadata).
3. **Post-process** tool calls outside batch if multi-step required.
4. **Use sync API** when latency-bound (pre-merge CI).


### `custom_id` fields

Per-request developer ID within a batch. Results may arrive **out of order** — use `custom_id` to match responses to inputs. Resubmit failures by `custom_id` only.

### Uploading documents for batch

Include document content in the `messages` payload (text, or image blocks for vision). For large corpora: chunk per `custom_id`, or pre-convert PDFs to text/markdown upstream.

### SLA math: 30-hour SLA with 24-hour batch window

**Guide example (p. 18–19):** *"4-hour windows to guarantee 30-hour SLA with 24-hour batch processing."*

| Variable | Meaning |
|----------|---------|
| 24h | Worst-case batch processing time |
| 30h | Your downstream SLA deadline |
| 6h | Buffer = 30 − 24 |
| 4h | **Submission frequency** — submit new work every 4h so a job started near deadline still completes within 30h |

**Your question (24+4=28 vs 30):** The 4 hours is **how often you submit**, not added to the 24h processing cap. Worst case: submit at T₀ → completes by T₀+24h. With 6h buffer before a 30h SLA, you need submission scheduling so **start_time + 24h ≤ deadline**. Submitting every 4h ensures no document waits too long in queue before processing begins.

**Example:** SLA = deliver report within 30h of document arrival.
- Submit batches every 4h.
- Any document waits at most ~4h to enter a batch + at most 24h processing = **28h** < 30h.

---

## Exam vs production summary

| Topic | Exam (guide) | Production delta |
|-------|--------------|------------------|
| Structured output | `tool_use` + JSON schema | Also `output_config.format`; prefill removed |
| Batch tool use | No multi-turn in one request | Server tools + `pause_turn`; client loops still multi-request |
| `/memory` | Diagnostic command | Plus expanded memory/rules ecosystem |
| `stop_sequences` | Not emphasized | Still supported |
| Confidence | Self-reported unreliable (5.2); field-level calibrated (5.5) | Same distinction critical for exam |

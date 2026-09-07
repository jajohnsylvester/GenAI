# Anti-Patterns Catalog

Systematic catalog from the **CCAF exam guide** (avoid / do not / instead of / rather than language). Columns: anti-pattern, why it fails, preferred pattern, guide ref.

> **Note:** The guide does not use the label "anti-pattern" everywhere; this catalog maps explicit warnings and common distractors.

| Anti-pattern | Why it fails | Preferred pattern | Guide ref |
|--------------|--------------|-------------------|-----------|
| Parsing natural language to decide loop termination | Non-deterministic; model prose varies | Check `stop_reason == "tool_use"` vs `"end_turn"` | 1.1, p. 4 |
| Arbitrary iteration cap as primary stop | May cut off mid-task or run too long | `stop_reason`-driven loop | 1.1, p. 4 |
| Checking assistant text for "done" | Model may emit text before tools complete | `stop_reason` + tool_result cycle | 1.1, p. 4 |
| Overly narrow coordinator decomposition | Incomplete coverage of broad topics | Dynamic subagent selection; partition scope | 1.2, p. 4–5 |
| Step-by-step coordinator micromanagement | Blocks subagent adaptability | Research goals + quality criteria | 1.3, p. 5 |
| Prompt-only ordering for financial ops | Non-zero failure rate on critical paths | Programmatic prerequisite gates / hooks | 1.4, p. 5–6 |
| Brute-force parallelization on unknown bug path | Wastes cost; misses actual path | Adaptive investigation subtasks | 1.6, p. 7 |
| Fixed investigation sequence regardless of findings | Explores irrelevant layers | Generate next subtask from evidence | 1.6, p. 7 |
| Resuming session with stale tool results | Agent acts on outdated state | New session + structured summary | 1.7, p. 7–8 |
| Minimal / overlapping tool descriptions | Misrouting among similar tools | Distinct names, I/O contracts, examples | 2.1, p. 8–9 |
| Generic `analyze_document` + free-text mode | Inconsistent output shapes | Split: `extract_data_points`, `summarize_content`, etc. | 2.1, p. 8–9 |
| Keyword routing in system prompt | Overrides good tool descriptions | Intent-based descriptions; audit prompts | 2.1, p. 8–9 |
| Generic "Operation failed" errors | Agent cannot recover appropriately | `errorCategory`, `isRetryable`, context | 2.2, p. 9 |
| Treating valid empty result as error | False retries / escalation | Distinguish access failure vs no matches | 2.2, p. 9 |
| Giving synthesis agent web search tools | Cross-specialization misuse | Scoped `verify_fact`; route complex lookups via coordinator | 2.3, p. 9–10 |
| 18 tools on one agent | Degraded tool selection | 4–5 role-relevant tools per agent | 2.3, p. 9–10 |
| Preferring Grep over capable MCP tool | Misses richer integration | Enhance MCP descriptions; expose catalogs | 2.4, p. 10–11 |
| Grep only original function name through wrappers | Misses alias callers | Read modules → list exports → grep each | 2.5, p. 11 |
| User-level CLAUDE.md for team standards | Teammates don't get instructions | Project-level `.claude/CLAUDE.md` + VCS | 3.1, p. 11–12 |
| Monolithic CLAUDE.md | Token bloat; hard to maintain | `@import` + `.claude/rules/` | 3.1, p. 11–12 |
| Plan mode for single-file bug fix | Unnecessary overhead | Direct execution | 3.4, p. 13–14 |
| Same session reviews its own generated code | Retains reasoning bias | Independent review instance | 3.6, p. 15–16; 4.6, p. 19–20 |
| Vague criteria ("be conservative") | No precision improvement | Explicit categorical criteria | 4.1, p. 16 |
| Post-hoc normalization only | Brittle permutation handling | Schema + normalization rules in prompt | 4.3, p. 17–18 |
| Required fields when source may omit data | Model fabricates values | Optional/nullable fields; `unclear` enum | 4.3, p. 17–18 |
| Retry when info absent from document | Wastes tokens; never succeeds | Identify absence vs format error; only retry format/structural errors | 4.4, p. 18 |
| Batch API for pre-merge blocking checks | Up to 24h latency | Synchronous Messages API | 4.5, p. 18–19 |
| Self-review only for subtle issues | Model won't question own reasoning | Second independent instance | 4.6, p. 19–20 |
| Sliding window drops resolved threads | Loses topic customer returns to | Progressive summarization of resolved issues | 5.1, p. 20–21 |
| Verbose tool results unfiltered | Token bloat; attention dilution | Trim to relevant fields before append | 5.1, p. 20–21 |
| Progressive summarization of exact amounts/dates | Loses precision | Case facts block outside summary | 5.1, p. 20–21 |
| Heuristic customer selection on multi-match | Wrong-account actions | Ask for email/phone/order ID | 5.2, p. 21 |
| Self-reported confidence threshold for identity | Unreliable; overconfident wrong picks | Explicit disambiguation questions | 5.2, p. 21; 4.6, p. 19–20 |
| Sentiment-based escalation | Unreliable proxy for complexity | Policy gaps, explicit requests, progress | 5.2, p. 21 |
| Immediate escalation with zero context | Cold handoff | Acknowledge + one targeted question | 5.2, p. 21 |
| Silently suppressing subagent errors | Coordinator blind to partial failure | Structured error + partial results | 5.3, p. 21–22 |
| Returning empty as success to hide errors | Masks failures | Valid empty vs access failure distinction | 5.3, p. 21–22 |
| Terminating entire workflow on single subagent fail | Loses partial value | Propagate structured error; coordinator recovers | 5.3, p. 21–22 |
| Periodic full context clear during exploration | Loses valid findings | Scratchpad file for key findings | 5.4, p. 22 |
| Trusting aggregate 97% accuracy alone | Masks weak document types/fields | Stratified sampling by segment | 5.5, p. 22–23 |
| Summarizing without claim-source mapping | Attribution lost | Structured claim-source through pipeline | 5.6, p. 23–24 |
| Arbitrarily picking one conflicting statistic | Hides uncertainty | Annotate conflict with sources | 5.6, p. 23–24 |

## Anti-pattern categories

### Agentic loop (1.1)
- Natural-language stop signals
- Arbitrary max-iterations as primary control
- Assistant-text completion heuristics

### Coordinator / multi-agent (1.2–1.4, 5.3, 5.6)
- Narrow decomposition
- Procedural step lists instead of goals
- Subagent-to-subagent direct comms (bypass coordinator)
- Synthesis agent doing search instead of verify

### Tooling (2.1–2.5)
- Overlapping generic tools
- Keyword-based routing
- Tool sprawl per agent

### Context (5.1, 5.4)
- Sliding window on multi-topic sessions
- Unfiltered MCP payloads
- Clearing context instead of externalizing notes

### Escalation & identity (5.2)
- Heuristic disambiguation
- Confidence-score auto-proceed
- Escalate for multi-intent when agent can handle both

### Extraction (4.3–4.4)
- Fabrication-prone required fields
- Post-processing-only normalization
- Retries when source lacks data

## Cross-reference: heuristic selection

**Heuristic customer identification** appears explicitly in Task 5.2 (p. 21): multiple matches require clarification **rather than heuristic selection**. Common distractors include confidence thresholds, backend ranking algorithms, and conversational context inference.

See Task 5.2 in the [official exam guide](https://anthropic.skilljar.com/claude-certified-architect-foundations-access-request) and [02-mock-exam-trap-guide.md](02-mock-exam-trap-guide.md).

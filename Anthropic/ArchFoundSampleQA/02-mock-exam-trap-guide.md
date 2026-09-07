# Mock Exam Trap Guide

Trap taxonomy for mapping mock exam misses. Take the [free CyberSkill mock](https://ccaf.cyberskill.world/) and [Certification Guide mock](https://claudecertificationguide.com/), then map your misses to this taxonomy.

## Trap taxonomy

| Trap type             | Sounds like…                                   | Why tempting                   | Guide-preferred                                    | Memory hook                         |
| --------------------- | ---------------------------------------------- | ------------------------------ | -------------------------------------------------- | ----------------------------------- |
| **Sounds enterprise** | Structured data layer, reference IDs           | Feels scalable/architectural   | Progressive summarization when narrative matters   | "Facts layer ≠ conversation memory" |
| **Sounds efficient**  | Re-fetch via MCP, parallel workers             | Saves tokens or time           | Trim/summarize context; adaptive single path       | "Fresh fetch ≠ shorter context"     |
| **Sounds smart**      | Confidence threshold, routing classifier       | Automates judgment             | Explicit criteria; programmatic gates for ordering | "Confidence ≠ verified identity"    |
| **Sounds helpful**    | Immediate escalation, try unauthorized action  | Protects customer/relationship | Calibrated: brief, one question, or resolve        | "Angry + no context → one question" |
| **Sounds thorough**   | Plan everything first, pre-summarize all files | Feels rigorous                 | Adaptive evidence-driven steps                     | "Debug follows clues, not scripts"  |
| **Sounds simple**     | Better description on generic tool             | Minimal change                 | Split tools + typed schemas                        | "Description < contract"            |
| **Sounds pragmatic**  | Post-processing normalization                  | Code handles edge cases        | Canonical format at extraction                     | "Fix at source, not after"          |

---

## CyberSkill mock misses

| Topic                  | Trap                               | Correct                              | Task | Pages |
| ---------------------- | ---------------------------------- | ------------------------------------ | ---- | ----- |
| Multi-issue context    | A: structured issue layer          | **C**: progressive summarization     | 5.1  | 20–21 |
| Document tools         | B: enum on one tool                | **A**: split purpose-specific tools  | 2.1  | 8–9   |
| Menu normalization     | B: post-processing                 | **D**: schema + prompt normalization | 4.3  | 17–18 |
| Wrapper tracing        | B/C: grep imports or original name | **A**: list aliases → grep each      | 2.5  | 11    |
| Agent forgets          | B: add "remember" prompt           | **C**: missing message history       | 5.1  | 20    |
| Intermittent 500s      | A/D: plan first or parallel        | **B**: adaptive subtasks             | 1.6  | 7     |
| Long exploration       | B: bigger model                    | **A**: scratchpad file               | 5.4  | 22    |
| Mid-process escalation | C/D: unauthorized retry or ref ID  | **B**: structured handoff            | 1.4  | 5–6   |
| Angry, no tools yet    | C: immediate escalate              | **A**: acknowledge + one question    | 5.2  | 21    |

---

## Certification Guide mock misses

| Topic                      | Trap                          | Correct                       | Task    | Pages |
| -------------------------- | ----------------------------- | ----------------------------- | ------- | ----- |
| Pre-compaction logging     | C: PreToolUse on Compact      | **B**: PreCompact hook        | 3.2–3.3 | 13–14 |
| Retry on unknown language  | C: add language to prompt     | **B**: retry boundary → human | 4.4     | 18–19 |
| Integration test standards | D: rules ban all mocks        | **B**: tighten CLAUDE.md      | 3.6     | 15–16 |
| Package naming             | D: custom tool_choice wrapper | **B**: PostToolUse hook       | 1.5     | 6–7   |
| Cancel info vs action      | D: few-shot routing           | **A**: boundary descriptions  | 2.1     | 8–9   |
| Explicit human request     | D: ask preference             | **B**: escalate immediately   | 5.2     | 20–21 |

---

## High-risk trap themes

| Theme                   | Typical wrong pick                   | Correct principle             | Task               |
| ----------------------- | ------------------------------------ | ----------------------------- | ------------------ |
| Escalation = policy gap | Escalate multi-intent or speculative | Escalate when policy silent   | 5.2                |
| Self-critique vs human  | Add human review overhead            | Self-critique reflection step | 1.1 / quality loop |
| Heuristic identity      | Confidence threshold / ranking       | Ask for identifiers           | 5.2                |
| Keyword tool routing    | Fix tool descriptions only           | Audit system prompt keywords  | 2.1                |
| Programmatic vs prompt  | Prompt mandating tool order          | Prerequisite gate / hook      | 1.4                |
| Batch for CI            | Batch overnight reviews for PR gate  | Sync API for blocking         | 4.5                |
| Synthesis tool scope    | Give synthesis web search            | Scoped `verify_fact` only     | 2.3                |
| Narrow coordinator task | Fixed pipeline all queries           | Dynamic subagent selection    | 1.2                |

---

## Guide mapping cheat sheet

```
Context filling up (multi-issue)     → 5.1 Summarize resolved; active thread full
Generic tool, inconsistent output    → 2.1 Split typed tools
Messy source formats                 → 4.3 Schema + normalization in prompt
Function behind wrappers             → 2.5 List aliases → grep each
Agent forgets mid-conversation       → 5.1 Pass full messages array
Unknown bug path                     → 1.6 Adaptive investigation
Long code exploration (30+ min)      → 5.4 Scratchpad file
Mid-process escalation               → 1.4 Structured handoff brief
Angry + no context                   → 5.2 Acknowledge + one question
Angry + fix ready                    → 5.2 Offer resolve or escalate
Identity multi-match                 → 5.2 Ask identifiers, never guess
```

---

## Suggested review order

1. Customer support — multi-issue context, mid-process escalation, angry/no context (Domain 5)
2. Tool design & extraction — document tools, menu normalization (Domains 2 & 4)
3. Code exploration — wrapper tracing, intermittent bugs, long sessions (Domains 1 & 5)
4. API fundamentals — agent forgets, message history (Domain 5)

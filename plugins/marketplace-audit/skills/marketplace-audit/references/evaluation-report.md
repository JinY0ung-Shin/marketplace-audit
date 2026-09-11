# Evaluation and reporting criteria

## Default report

1. Assessment: use evidence-appropriate terms such as priority improvements needed, generally appropriate, or insufficient evidence. Do not declare a complete pass after partial review.
2. Scope: target revision, runtime, active configuration, reviewed/excluded paths, total and fully read components by type, and whether execution occurred.
3. Responsibility matrix and dimension statuses: appropriate / needs improvement / unverified / not applicable. Link evidence and findings.
4. Findings: order by priority and use the format below.
5. Good design to preserve, prioritized fixes, behavioral verification scenarios, and limitations.

### Finding format

- ID / title / dimension / severity / evidence classification / confidence.
- Evidence: exact file path and line number or symbol/JSON path, with a short excerpt; for runtime evidence, identify trace events, commands, and results.
- Current behavior and impact: conditions, affected parties, and consequences.
- Boundary judgment: overlapping or missing ownership of responsibilities, procedures, or service contracts.
- Counterevidence: intended exceptions and benefits of the current arrangement.
- Minimal fix: what to move, combine, or separate, its destination, and affected callers.
- Verification: a check or request demonstrating that the failure is resolved.

## Optional scoring

Score only when requested. This is a project heuristic, not an official standard.

| Dimension | Weight |
| --- | ---: |
| Structure/compatibility | 15 |
| Responsibility boundaries/rule ownership | 25 |
| Invocation/routing | 15 |
| Contracts/dependencies | 15 |
| Permissions/side effects | 10 |
| Distribution/maintenance | 10 |
| Context/efficiency | 5 |
| Execution/evaluability | 5 |

Score each dimension from 0 to 4: 0 = core use impossible; 1 = serious defects; 2 = substantial improvements needed; 3 = generally appropriate with limited issues; 4 = evidence confirms requirements within the reviewed scope. Use unverified instead of a number when essential evidence is absent or review is insufficient. Link each score to findings or positive evidence.

Observed score = 100 × sum(assessed dimension weight × score/4) / sum(assessed dimension weights).
Coverage = sum(assessed dimension weights) / sum(applicable dimension weights).

Use not applicable only when the dimension does not apply to the task, and explain why. Missing evidence is unverified. Do not score a zero denominator. Below 80% coverage, omit an aggregate score and report dimension results only. Even above that threshold, label static results as static design scores, not operational assurance. Show unresolved Critical/High findings separately from scores.

## Behavioral evaluation design

If new runs were not requested, propose scenarios or analyze supplied traces only. Never label a static walkthrough as a measurement. For actual runs, record model, runtime, configuration revision, active skills/tools, data snapshot, and cache conditions.

Define for each scenario:
- User request and input fixture.
- Acceptable agent/skill/tool paths and alternatives; do not assume one correct path.
- Components that must not be selected and why.
- Expected deliverable, supporting data, and completion/stopping conditions.
- Expected side effects, isolation/mocking, and traces/costs to observe.

Choose representative success, neighboring-skill boundary requests, out-of-scope requests, missing inputs, MCP failures, insufficient permissions, and write requests according to actual target risks. Add scenarios for discovered rule duplication and dependency issues.

| Metric | Definition and cautions |
| --- | --- |
| Task success rate | Runs meeting deliverable criteria / runs executed. Withhold judgment without a known acceptance criterion |
| Routing accuracy | Runs satisfying acceptable paths and required selections / assessable runs |
| Incorrect call rate | Calls with incorrect target, schema, preconditions, or permissions / all calls. Track categories separately |
| Missed selection rate | Runs missing required skill/tool selection / assessable runs |
| Recovery success rate | Completed runs with recoverable failures / runs with recoverable failures |
| Efficiency | Compare calls, repeated queries, tokens, and latency for successful runs under equivalent conditions. Early failure is not efficiency |

Report numerator and denominator for every rate; use N/A for zero denominators. Choose repetitions according to variability and cost and disclose sample sizes. If using an LLM judge, retain the rubric and supporting evidence, then review boundary cases and disagreements. Do not fabricate unobserved token or timing measurements.

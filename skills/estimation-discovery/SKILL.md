---
name: estimation-discovery
description: "Trigger: unclear estimation inputs, messy notes, transcripts, missing scope. Produce an estimation brief and readiness gate."
license: Apache-2.0
metadata:
  author: gentleman-programming
  version: "1.0"
---

## Activation Contract

Load this skill when estimation inputs are ambiguous, incomplete, transcript-like, or not ready for a sizing method.

## Hard Rules

- Do not estimate size, duration, cost, or staffing from discovery output.
- Do not invent business rules, acceptance criteria, actors, entities, or transactions.
- Mark missing facts as `[UNKNOWN]`; mark insufficient scope as `NOT READY`.
- Separate business problem, proposed solution, assumptions, and open questions.

## Decision Gates

| Evidence | Next step |
|---|---|
| Stories with acceptance criteria and team context | Recommend `agile-story-estimation` |
| Component/module list with local proxy examples | Recommend `proxy-component-estimation` |
| Functional boundary with data and transaction candidates | Recommend `function-point-estimation` |
| Missing boundary, actors, or rules | Return `NOT READY` and ask clarification questions |

## Execution Steps

1. Read `references/estimation-brief-template.md`.
2. Extract only facts present in the supplied material.
3. Populate every mandatory brief section; use `[UNKNOWN]` for gaps.
4. List assumptions separately from facts and questions.
5. Assess readiness and recommend one method only when inputs meet its minimum gate.

## Output Contract

Return an estimation brief, readiness status (`READY` or `NOT READY`), missing inputs, clarification questions, recommended next skill if ready, and `> [HUMAN REVIEW REQUIRED]` when extracted facts may drive sizing.

## References

- `references/estimation-brief-template.md`

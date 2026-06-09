---
name: estimation-review
description: "Trigger: estimate audit, proposal review, timeline critique, false precision. Review estimates by severity."
license: Apache-2.0
metadata:
  author: gentleman-programming
  version: "1.0"
---

## Activation Contract

Load this skill when reviewing an existing estimate, proposal, roadmap, timeline, forecast, sizing worksheet, or estimation transcript.

## Hard Rules

- Return findings ordered Critical, High, Medium, Low.
- Each finding must state what is wrong, why it matters, and the recommended correction or question.
- Treat a single-point estimate without range, assumptions, or confidence as Critical false precision.
- Treat modified/refactored code estimated like new work as High unless comprehension cost is explicit.
- Separate transcript-derived observations from externally validated method claims.
- Do not recalculate the estimate unless the user explicitly asks after the audit.

## Decision Gates

| Evidence | Severity |
|---|---|
| Single date/cost/effort with no range or assumptions | Critical |
| Missing DoD, QA/UAT, infra, security, performance, or integration scope | High |
| Modified/refactor work lacks comprehension overhead | High |
| Cross-team velocity or uncalibrated productivity used | High |
| Transcript-only rule presented as external standard | Medium |

## Execution Steps

1. Read `references/review-checklist.md`.
2. Identify estimate method, inputs, assumptions, scope, DoD, calibration source, and confidence.
3. Audit false precision, missing scope, modified-code cost, calibration, and source boundaries.
4. Order findings by severity and avoid duplicates.
5. Return pass confirmations when no Critical or High findings exist.

## Output Contract

Return audit scope, method reviewed, severity-ordered findings, passed checks, source-boundary notes, recommended corrections/questions, and `> [HUMAN REVIEW REQUIRED]` for downstream use.

## References

- `references/review-checklist.md`

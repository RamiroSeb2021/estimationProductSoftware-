# Estimation Review Checklist

Use this checklist to audit an existing estimate without silently replacing it.

## Severity Rules

| Severity | Use for |
|---|---|
| Critical | False precision, deterministic commitment without range, absent assumptions, or unsafe downstream use. |
| High | Missing DoD/quality scope, NFR/integration omissions, uncalibrated cross-team productivity, modified-code underestimation. |
| Medium | Weak rationale, incomplete confidence statement, transcript-only idea presented too strongly. |
| Low | Formatting, naming, or clarity issues that do not change forecast safety. |

## Required Finding Shape

Each finding includes:

- What is wrong.
- Why it matters.
- Recommended correction or question.
- Evidence from the reviewed artifact.
- Source boundary: external reference, team artifact, or `(Source: internal Tech Talk — illustrative; verify against formal method reference)`.

## Checks

- False precision: single date, cost, staffing, size, or point total with no optimistic/expected/pessimistic range.
- Assumptions: missing productivity baseline, capacity, confidence, scope boundary, or DoD.
- Scope gaps: QA, UAT, infra, deployment, docs, security, performance, integrations, AI/LLM calls.
- Modified work: refactor or existing-code changes treated as greenfield/new work.
- Calibration: cross-team velocity, generic productivity rate, or proxy class without local reference.
- Function points: calculated FP without approved workbook or missing human-review gate.

## Clean Estimate Confirmation

If no Critical or High findings exist, confirm the estimate has scope, DoD, assumptions, confidence range, method, calibration source, and human review gate.

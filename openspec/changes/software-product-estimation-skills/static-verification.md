# Static Verification Notes: Software Product Estimation Skills

## Scope

Manual/static verification for PR 3 / Slice 3. No verify/archive phase was launched.

## Static Checks

| Check | Result | Evidence |
|---|---|---|
| Seven skill directories exist | Pass | `software-product-estimation`, `estimation-discovery`, `agile-story-estimation`, `proxy-component-estimation`, `function-point-estimation`, `estimation-to-plan`, `estimation-review`. |
| Frontmatter present | Pass | All seven `SKILL.md` files include `name`, quoted `description`, `license`, `metadata.author`, and `metadata.version`. |
| Required section order | Pass | All seven follow Activation Contract, Hard Rules, Decision Gates, Execution Steps, Output Contract, References. |
| References linked and present | Pass | All referenced local files exist under each skill's `references/` directory. |
| Token budget | Pass | Manual line/token review: all `SKILL.md` bodies are concise and under the 1000-token hard cap. |
| Registry includes project skills | Pass | `.atl/skill-registry.md` includes all seven project-local estimation skills. |
| FP calculations unavailable | Pass | `function-point-estimation` blocks adjusted/unadjusted FP counts unless approved workbook tables replace the stub. |
| Safety gates | Pass | Human review, local calibration, FP workbook, false precision, and Brooks staffing gates are present in the relevant skills. |

## Traceability Matrix

| Spec domain | Requirements | Scenarios | Coverage |
|---|---:|---:|---|
| `software-product-estimation` | 3 | 7 | Covered by router gates, size-duration separation, false-precision guard, and handoff output. |
| `estimation-discovery` | 3 | 5 | Covered by brief template, `[UNKNOWN]`, `NOT READY`, no-invention rules, and readiness method routing. |
| `agile-story-estimation` | 4 | 7 | Covered by INVEST/DoR/DoD checks, implementer-led sizing, divergence handling, and local calibration gate. |
| `proxy-component-estimation` | 3 | 4 | Covered by worksheet, S/M/L classes, new/modified/refactor status, NFR flags, and proxy calibration gate. |
| `function-point-estimation` | 4 | 6 | Covered by worksheet-only mode, ILF/EIF/EI/EO/EQ classification, navigation exclusion, workbook block, and AI human-review gate. |
| `estimation-to-plan` | 4 | 5 | Covered by range-only forecast, required assumptions, DoD/QA/UAT line items, Brooks's Law guard, and cross-team velocity block. |
| `estimation-review` | 4 | 5 | Covered by severity ordering, false-precision Critical finding, modified-code High finding, and source-boundary notes. |
| **Total** | **25** | **39** | **Pass — all requirements and actual spec scenarios mapped at concise static level.** |

## Corrective Count Reconciliation

The prior static-verification summary overstated scenario coverage as 44 scenarios. Recounting the seven authoritative OpenSpec files found 25 `### Requirement:` blocks and 39 `#### Scenario:` blocks. No spec file was missing scenario coverage for a requirement, so this corrective update changes the summary counts instead of adding invented scenarios.

## Known Verification Boundary

This artifact records manual/static checks only. The slice preflight stated strict TDD is inactive and no test runner is available, so no automated test cycle evidence is produced.

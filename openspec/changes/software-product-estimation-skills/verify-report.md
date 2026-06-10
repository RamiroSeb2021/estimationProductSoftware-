## Verification Report

**Change**: software-product-estimation-skills
**Version**: N/A
**Mode**: Standard static/manual verification rerun after corrective apply; strict TDD inactive; no applicable runtime test runner detected for this skill/documentation slice

### Completeness

| Metric | Value |
|--------|-------|
| Tasks total | 22 |
| Tasks complete | 22 |
| Tasks incomplete | 0 |
| Skill directories expected/found | 7 / 7 |
| `SKILL.md` files expected/found | 7 / 7 |
| Referenced local skill references expected/found | 8 / 8 |
| Requirements independently counted from spec files | 25 |
| Scenarios independently counted from spec files | 39 |
| Current scenario source of truth | 39 actual `#### Scenario:` blocks |
| Stale 44-scenario overstatement | Not present as current truth; remaining mentions are historical/corrective only |
| Delivery strategy | ask-always |
| Resolved chain strategy | stacked-to-main |

### Build & Tests Execution

**Build**: Not applicable

```text
No application build exists for this documentation/project-local skill artifact change.
```

**Tests**: Runtime tests unavailable / not applicable

```text
Strict TDD is inactive. No package-level application test runner was detected.
`skills/setup_test.sh` exists, but it tests `skills/setup.sh`; it is not a behavioral test runner for these seven new estimation skills.

Static/manual inspection commands executed:
- python3 spec counter over all seven OpenSpec `spec.md` files: 25 requirements, 39 scenarios.
- python3 skill structure check: 7/7 frontmatter blocks valid; required sections in order; 8/8 referenced local files present.
- python3 safety-gate text check: false precision, human review, FP workbook block, local calibration, cross-team velocity block, Brooks guard, UNKNOWN/NOT READY no-invention gates, NFR surfacing, and source boundary present.
- grep for `44` / `44 scenarios`: only historical/corrective mentions remain in `static-verification.md` and this report.
- git diff --check: passed; no whitespace errors.
- git status --short --ignored: `.atl/` and `.pi/` are ignored; current OpenSpec files are modified/untracked as expected for the artifact slice.
```

**Coverage**: Not available

### Spec Compliance Matrix

| Domain | Requirements | Scenarios | Static verification result |
|--------|--------------|-----------|----------------------------|
| `software-product-estimation` | 3 | 7 | STATIC COVERED: router routes, false-precision guard, human-review gate, size-duration separation. |
| `estimation-discovery` | 3 | 5 | STATIC COVERED: brief template, `[UNKNOWN]`, `NOT READY`, no-invention rules, readiness routing. |
| `agile-story-estimation` | 4 | 7 | STATIC COVERED: INVEST/DoR/DoD checks, implementer-led sizing, divergence handling, local calibration, cross-team block. |
| `proxy-component-estimation` | 3 | 4 | STATIC COVERED: worksheet, S/M/L proxy sizing, modified/refactor warning, NFR/AI complexity handling, proxy calibration gate. |
| `function-point-estimation` | 4 | 6 | STATIC COVERED: worksheet-only mode, workbook gate, ILF/EIF/EI/EO/EQ classification, AI human-review gate, size-productivity separation. |
| `estimation-to-plan` | 4 | 5 | STATIC COVERED: range-only forecast, missing-input block, DoD/quality line items, Brooks staffing guard, cross-team velocity block. |
| `estimation-review` | 4 | 5 | STATIC COVERED: severity ordering, false-precision Critical finding, modified-code check, clean-estimate confirmation, source-boundary notes. |
| **Total** | **25** | **39** | **STATIC COVERED** |

**Compliance summary**: 39/39 scenarios are present in the authoritative spec files and statically mapped to implemented skill rules/checklists. Runtime behavioral compliance cannot be claimed because no applicable runner exists for these LLM skill artifacts.

### Correctness (Static Evidence)

| Requirement area | Status | Notes |
|------------------|--------|-------|
| Seven project-local skills | Implemented | All expected `skills/{name}/SKILL.md` files exist. |
| Frontmatter | Implemented | All seven include `name`, quoted trigger-first `description`, `license`, `metadata.author`, and `metadata.version`. |
| Required section order | Implemented | All seven follow Activation Contract, Hard Rules, Decision Gates, Execution Steps, Output Contract, References. |
| Local references | Implemented | All eight referenced `references/*` files exist. |
| False precision guard | Implemented | Router, forecast, review, and supporting references block deterministic single-point estimates without assumptions/ranges/confidence. |
| Human review gates | Implemented | Human-review gates are present in output-producing skills. |
| FP worksheet/default workbook block | Implemented | `function-point-estimation` blocks adjusted/unadjusted FP counts while workbook is a stub. |
| Local calibration | Implemented | Agile and proxy skills gate uncalibrated story/proxy outputs. |
| Cross-team velocity conversion | Implemented | Agile and forecast flows block cross-team point/velocity conversion. |
| Brooks guard | Implemented | Forecast skill/reference surface onboarding, knowledge-transfer, and communication overhead. |
| UNKNOWN / NOT READY no-invention gates | Implemented | Discovery and FP flows mark missing facts `[UNKNOWN]`; discovery/agile block unsafe sizing as `NOT READY`. |
| NFR surfacing | Implemented | Discovery, proxy, forecast, and review references surface NFR/integration/AI complexity. |
| Source boundary | Implemented | Router notes and review checklist distinguish internal Tech Talk claims from external method claims. |
| Tasks/apply decisions | Implemented | `tasks.md` shows all checkboxes complete and chain strategy resolved as `stacked-to-main`. |
| Corrective scenario-count reconciliation | Implemented | `design.md`, `tasks.md`, `static-verification.md`, and this report use 25 requirements / 39 scenarios as current truth. |

### Coherence (Design)

| Decision | Followed? | Notes |
|----------|-----------|-------|
| Router plus six focused skills | Yes | Seven project-local skills exist and keep workflows bounded. |
| Keep `SKILL.md` concise; move detail to references | Yes | Long checklists/workbooks live under local `references/`. |
| FP worksheet/review-only by default | Yes | Stub workbook blocks calculated FP output. |
| AI outputs require human review before commitments | Yes | Required gates appear in hard rules and output contracts. |
| Registry sync | Partially operational | `.atl/skill-registry.md` includes all seven project skills, but `.atl/` is ignored by `.gitignore`. |

### Issues Found

**CRITICAL**
- None in the corrected source of truth.

**WARNING**
- No applicable runtime behavioral tests exist for the seven LLM skill artifacts. This rerun can verify structure, traceability, and static safety gates, but cannot prove model-runtime behavior with executable scenario tests.
- `.atl/skill-registry.md` is updated on disk and includes the seven project-local skills, but `.atl/` is ignored by `.gitignore`; normal commits will not include the registry unless the workflow explicitly handles ignored artifacts.

**SUGGESTION**
- Add a lightweight static verifier script if this skill suite becomes a maintained artifact, covering frontmatter, section order, reference existence, scenario counts, safety gates, and stale-count checks.

### Verdict

**PASS WITH WARNINGS**

Corrective apply resolved the prior count mismatch. The authoritative OpenSpec source now verifies as 25 requirements and 39 scenarios, all tasks are complete, all seven skills and references exist, and the required safety constraints are statically present. Warnings remain because runtime skill behavior is not executable in this project and the generated `.atl/` registry is ignored by Git.

### Phase Contract

**status**: PASS_WITH_WARNINGS

**executive_summary**: Verification rerun passed the corrected static/manual quality gate. The prior 44-scenario overstatement is no longer current truth; the active source of truth is 25 requirements / 39 scenarios. Runtime tests are unavailable for these LLM skill artifacts, so the verdict is not a full executable behavioral proof.

**artifacts**:
- `openspec/changes/software-product-estimation-skills/proposal.md` — read and verified scope/success criteria.
- `openspec/changes/software-product-estimation-skills/specs/*/spec.md` — independently counted 25 requirements / 39 scenarios.
- `openspec/changes/software-product-estimation-skills/design.md` — verified corrected traceability and design coherence.
- `openspec/changes/software-product-estimation-skills/tasks.md` — verified 22/22 complete and `stacked-to-main` resolved.
- `openspec/changes/software-product-estimation-skills/static-verification.md` — verified corrected 39-scenario traceability matrix.
- `openspec/changes/software-product-estimation-skills/verify-report.md` — updated with this rerun result.
- `skills/*/SKILL.md` and `skills/*/references/*` — verified 7/7 skills and 8/8 local references.
- `.atl/skill-registry.md` — verified all seven project skills are indexed, with ignored-file warning.
- Engram `sdd/software-product-estimation-skills/apply-progress` #854 — read as corrective apply context.

**next_recommended**: Proceed to orchestrator/user acceptance of the PASS_WITH_WARNINGS result, then archive the SDD change if the warnings are acceptable for a documentation/project-local skill slice.

**risks**:
- Runtime LLM behavior may drift from static instructions because no executable scenario harness exists.
- Ignored `.atl/` registry changes may be omitted from review/commit unless intentionally handled.

**skill_resolution**: Loaded and applied `sdd-verify`, `skill-creator`, and `cognitive-doc-design`. Strict TDD verify was intentionally not loaded because strict TDD is inactive and no applicable test runner was detected.

**verification_summary**: Static/manual rerun verified source counts, artifact consistency, 7/7 skill existence, valid frontmatter/sections/references, required estimation safety constraints, complete tasks, resolved chain strategy, git ignored registry behavior, and absence of stale current 44-scenario claims.

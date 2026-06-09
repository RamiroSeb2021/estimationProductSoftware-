# Tasks: Software Product Estimation Skills

## Review Workload Forecast

| Field | Value |
|-------|-------|
| Estimated changed lines | 600–850 (15 new files × avg 40–55 lines each + registry modify) |
| 400-line budget risk | High |
| Chained PRs recommended | Yes |
| Suggested split | PR 1 → PR 2 → PR 3 |
| Delivery strategy | ask-always |
| Chain strategy | pending (user decision required) |

Decision needed before apply: Yes
Chained PRs recommended: Yes
Chain strategy: pending
400-line budget risk: High

> **Decision required before `sdd-apply`**: The planned change exceeds the 400-line review budget.
> Please choose a chain strategy:
> - **stacked-to-main** — PR 1, PR 2, PR 3 each merge directly to main in order.
> - **feature-branch-chain** — a tracker branch (`feature/software-product-estimation-skills`) accumulates the full change; child PRs target their immediate parent branch; only the tracker merges to main.
> - **size:exception** — single oversized PR with maintainer approval.

### Suggested Work Units

| Unit | Goal | Likely PR | Notes |
|------|------|-----------|-------|
| 1 | Shared infrastructure + router skill | PR 1 | Base: main (or tracker branch). Includes `docs/skill-style-guide.md` validation, router SKILL.md + 2 references. |
| 2 | Four method skills (discovery, agile, proxy, FP) | PR 2 | Base: PR 1 branch (feature-chain) or main (stacked). Each skill + its references directory. |
| 3 | Forecast + review skills + registry sync + static verification | PR 3 | Base: PR 2 branch (feature-chain) or main (stacked). Closes all remaining files. |

---

## Phase 1: Foundation — Shared Infrastructure (PR 1 scope)

- [x] 1.1 Verify `docs/skill-style-guide.md` exists and is readable; confirm section order and token-budget rules are in place before any skill is written.
- [x] 1.2 Create `skills/software-product-estimation/` directory and `skills/software-product-estimation/references/` directory.
- [x] 1.3 Create `skills/software-product-estimation/SKILL.md` — router skill with frontmatter, Activation Contract, Hard Rules (false-precision guard, size-before-duration boundary), Decision Gates (6-route table), Execution Steps, Output Contract, References.
- [x] 1.4 Create `skills/software-product-estimation/references/router-decision-tree.md` — full routing rules with minimum required inputs per route.
- [x] 1.5 Create `skills/software-product-estimation/references/meeting-notes.md` — transcript-derived concepts marked `[ILLUSTRATIVE — not validated external standard]`.

## Phase 2: Core Method Skills — Discovery, Agile, Proxy, FP (PR 2 scope)

- [ ] 2.1 Create `skills/estimation-discovery/SKILL.md` — Activation Contract, Hard Rules (no invented business rules), Execution Steps producing estimation brief, Output Contract, References.
- [ ] 2.2 Create `skills/estimation-discovery/references/estimation-brief-template.md` — brief sections (problem space, solution space, scope, actors, capabilities, entities, transactions, integrations, NFRs, assumptions, unknowns) and readiness checklist.
- [ ] 2.3 Create `skills/agile-story-estimation/SKILL.md` — INVEST/DoR readiness check, Planning Poker workflow, `[LOCAL CALIBRATION REQUIRED]` gate, DoD scope inclusion.
- [ ] 2.4 Create `skills/agile-story-estimation/references/planning-poker-checklist.md` — readiness gate, divergence-trigger rules, cross-team comparison block.
- [ ] 2.5 Create `skills/proxy-component-estimation/SKILL.md` — component decomposition worksheet, S/M/L class rules, new/modified/refactor distinction, NFR flagging, `[LOCAL PROXY CALIBRATION REQUIRED]` gate.
- [ ] 2.6 Create `skills/proxy-component-estimation/references/proxy-sizing-guide.md` — S/M/L guidance table, comprehension-cost warning for modified/refactor, AI/integration complexity flags.
- [ ] 2.7 Create `skills/function-point-estimation/SKILL.md` — ILF/EIF/EI/EO/EQ classification, worksheet-only default, `[COUNTING WORKBOOK REQUIRED]` block, `[HUMAN REVIEW REQUIRED — AI-extracted count]` gate on every AI classification.
- [ ] 2.8 Create `skills/function-point-estimation/references/counting-workbook.md` — stub with `[STUB — approved tables required before FP counts are emitted]`; no fabricated complexity weights.

## Phase 3: Forecast + Review Skills (PR 3 scope)

- [ ] 3.1 Create `skills/estimation-to-plan/SKILL.md` — uncertainty range output (optimistic/expected/pessimistic), DoD/QA/UAT line items, Brooks's Law staffing guard, no single-point date, `[HUMAN REVIEW REQUIRED]` gate.
- [ ] 3.2 Create `skills/estimation-to-plan/references/forecast-model.md` — capacity checklist, DoD/QA/UAT items, Brooks's Law overhead table, staffing-addition warning.
- [ ] 3.3 Create `skills/estimation-review/SKILL.md` — severity-ordered audit (Critical/High/Medium/Low), false-precision detection as Critical, modified-code-as-new as High, transcript-vs-external source boundary.
- [ ] 3.4 Create `skills/estimation-review/references/review-checklist.md` — false precision, scope gaps, DoD completeness, modified-code comprehension, source-boundary checks.

## Phase 4: Integration + Registry + Static Verification (PR 3 scope)

- [ ] 4.1 Update `.atl/skill-registry.md` — add all 7 new skills (name, trigger/description, scope, path) to the Skills table; update `Last updated` date.
- [ ] 4.2 Run `bash skills/setup_test.sh` and confirm all existing tests pass with no regressions.
- [ ] 4.3 Manual static check for each of the 7 `SKILL.md` files: frontmatter complete, required sections in order, body ≤1000 tokens, `references/` files linked and present.
- [ ] 4.4 Verify traceability matrix: confirm all 25 requirements and 44 scenarios from spec are covered by skill rules/checklists (document pass/fail per spec scenario in verification notes).
- [ ] 4.5 Verify safety gates: confirm `[HUMAN REVIEW REQUIRED]`, `[COUNTING WORKBOOK REQUIRED]`, and `[LOCAL CALIBRATION REQUIRED]` strings appear in the correct skills and are not omittable by prompt phrasing.

# Design: Software Product Estimation Skills

## Technical Approach

Create seven project-local LLM-first skills under `skills/`, each as a compact runtime contract governed by `docs/skill-style-guide.md`. The router (`software-product-estimation`) selects one focused workflow; method skills produce bounded worksheets, reviews, or handoff-ready outputs. Long background, transcript notes, checklists, worksheets, source notes, and examples live in `references/` so every `SKILL.md` stays under the 1000-token hard cap.

## Architecture Decisions

| Option | Tradeoff | Decision |
|---|---|---|
| One monolithic estimator | Simple trigger, but bloated and mixes methods | Use router + six focused skills to preserve boundaries and reviewability. |
| Put examples/tables in `SKILL.md` | Easier to read once, worse runtime budget | Keep `SKILL.md` concise; move details to local `references/`. |
| FP calculation by default | Useful output, high risk without approved tables | Worksheet/review-only by default; no calculated FP until approved workbook exists and human reviews AI extraction. |
| AI-generated commitments | Fast but unsafe | AI may extract/categorize/forecast ranges; commitments require explicit human review. |

## Data Flow

```text
User request
  -> software-product-estimation router
  -> one focused skill
  -> worksheet/review/range output
  -> [HUMAN REVIEW REQUIRED]
  -> optional next-step handoff
```

Router decision tree:
1. Existing estimate/proposal/timeline to audit -> `estimation-review`.
2. Formal size, FP, IFPUG/ISO, ILF/EIF/EI/EO/EQ -> `function-point-estimation`.
3. Backlog, stories, Planning Poker, points/hours -> `agile-story-estimation`.
4. Conceptual design, modules/components, S/M/L proxy -> `proxy-component-estimation`.
5. “How long/cost/people/when?” with validated size -> `estimation-to-plan`.
6. Ambiguous/messy notes, transcript, missing boundary -> `estimation-discovery`.

## File Changes

| File | Action | Description |
|---|---|---|
| `skills/software-product-estimation/SKILL.md` | Create | Router, false-precision guard, size-before-duration boundary. |
| `skills/software-product-estimation/references/router-decision-tree.md` | Create | Routing rules and minimum inputs. |
| `skills/software-product-estimation/references/meeting-notes.md` | Create | Clean transcript-derived concepts, marked illustrative. |
| `skills/estimation-discovery/SKILL.md` | Create | Extract estimation brief without inventing rules. |
| `skills/estimation-discovery/references/estimation-brief-template.md` | Create | Brief sections and readiness checklist. |
| `skills/agile-story-estimation/SKILL.md` | Create | INVEST/DoR/DoD and Planning Poker workflow. |
| `skills/agile-story-estimation/references/planning-poker-checklist.md` | Create | Readiness, divergence, local calibration notes. |
| `skills/proxy-component-estimation/SKILL.md` | Create | Component decomposition and proxy worksheet. |
| `skills/proxy-component-estimation/references/proxy-sizing-guide.md` | Create | S/M/L guidance, new/modified/refactor caveats. |
| `skills/function-point-estimation/SKILL.md` | Create | FP worksheet/review with calculation block. |
| `skills/function-point-estimation/references/counting-workbook.md` | Create | Stub requiring approved tables; no fabricated weights. |
| `skills/estimation-to-plan/SKILL.md` | Create | Converts validated size to forecast ranges. |
| `skills/estimation-to-plan/references/forecast-model.md` | Create | Capacity, DoD, QA/UAT, Brooks-law checklist. |
| `skills/estimation-review/SKILL.md` | Create | Severity-ordered audit workflow. |
| `skills/estimation-review/references/review-checklist.md` | Create | False precision, scope, DoD, source-boundary checks. |
| `.atl/skill-registry.md` | Modify | Re-index after apply. |

## Interfaces / Contracts

Each skill uses frontmatter with `name`, one-line quoted `description`, `license`, `metadata.author`, and `metadata.version`; body sections follow Activation Contract, Hard Rules, Decision Gates, Execution Steps, Output Contract, References.

Shared output gates:
- `> [HUMAN REVIEW REQUIRED]` for any size, forecast, or AI-assisted classification.
- `[COUNTING WORKBOOK REQUIRED — no calculated FP emitted]` when FP workbook lacks approved tables.
- `[LOCAL CALIBRATION REQUIRED]` for story points/proxy sizes without team-local history.

## Testing Strategy

| Layer | What to Test | Approach |
|---|---|---|
| Static | Frontmatter, required section order, token budget, local references | Manual checklist plus `bash skills/setup_test.sh` where applicable. |
| Layout | Seven skill directories and expected references | Path/layout review. |
| Traceability | 25 requirements and 44 scenarios covered by skill rules/checklists | Scenario coverage matrix in verification notes. |
| Safety | FP blocks, no single-point estimates, no commitments | Static review of Hard Rules and Output Contracts. |

## Migration / Rollout

No data migration required. Apply creates new skill directories, then refreshes the skill registry. No final skills are created during this design phase.

## Open Questions

- [ ] Organization must later supply official DoR/DoD, productivity baselines, cost rates, and approved FP counting tables before formal proposal use.

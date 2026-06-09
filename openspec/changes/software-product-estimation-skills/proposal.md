# Proposal: Software Product Estimation Skills

## Intent

Build a suite of project-local skills that apply software product estimation concepts from the internal Tech Talk transcript, backed by external sources (Scrum Guide, INVEST, ISO/IEC 20926, Fowler, Brooks). No estimation tool or calculator exists today; engineers estimate ad-hoc without a shared method or guardrails.

## Scope

### In Scope
- `software-product-estimation` — router skill (entry point, method selection, false-precision guard)
- `estimation-discovery` — extract estimation-ready inputs from ambiguous artifacts
- `agile-story-estimation` — backlog readiness, Planning Poker reasoning, team-local calibration
- `proxy-component-estimation` — conceptual design decomposition into small/medium/large components
- `function-point-estimation` — conservative IFPUG-style worksheet/review (no fabricated official tables)
- `estimation-to-plan` — size-to-duration/cost/staffing forecast with confidence range
- `estimation-review` — audit existing estimates for gaps and invalid assumptions
- Supporting `references/` files per skill (cleaned transcript notes, checklists, workbooks)
- Skill-registry sync after creation

### Out of Scope
- Production estimation calculator or database
- Official IFPUG counting tables (require organizational approval)
- Organizational productivity baselines, cost rates, DoR/DoD templates (must be supplied externally)
- `estimation-knowledge-artifact` and `construction-estimation-analogy` skills (deferred to Phase 2)
- Cross-team story-point normalization tooling

## Capabilities

### New Capabilities
- `software-product-estimation`: router skill; selects method and enforces false-precision guard
- `estimation-discovery`: structured extraction from messy product artifacts into estimation briefs
- `agile-story-estimation`: INVEST/DoR/DoD readiness and Planning Poker facilitation workflow
- `proxy-component-estimation`: component decomposition and proxy sizing with prior-calibration checks
- `function-point-estimation`: IFPUG-aligned ILF/EIF/EI/EO/EQ worksheet and conservative counting rules
- `estimation-to-plan`: productivity-based forecast with uncertainty, staffing risk, and Brooks-law guard
- `estimation-review`: severity-ordered audit of existing estimates with gap detection

### Modified Capabilities
None

## Approach

Seven `SKILL.md` files under `skills/{name}/`, each under the 1000-token budget. Long content (transcript notes, checklists, count workbooks, forecast models) moves into `skills/{name}/references/`. The router skill (`software-product-estimation`) orchestrates by instruction, not by sub-agent delegation. Function Point skill defaults to review/worksheet mode; full counting requires local `references/counting-workbook.md` to be supplied before formal count output.

Human review gates: any AI-generated size estimate must surface a clearly marked `> [HUMAN REVIEW REQUIRED]` block with assumptions, uncertainty, and confidence before being used downstream.

Source citations are mandatory in each skill's evidence base; transcript claims must be distinguished from externally validated method rules.

## Affected Areas

| Area | Impact | Description |
|------|--------|-------------|
| `skills/software-product-estimation/` | New | Router skill + meeting-notes reference |
| `skills/estimation-discovery/` | New | Discovery skill |
| `skills/agile-story-estimation/` | New | Agile skill + planning-poker checklist |
| `skills/proxy-component-estimation/` | New | Proxy skill + proxy-sizing guide |
| `skills/function-point-estimation/` | New | FP skill + counting-workbook stub |
| `skills/estimation-to-plan/` | New | Forecast skill + forecast-model reference |
| `skills/estimation-review/` | New | Review skill + review-checklist reference |
| `.atl/skill-registry.md` | Modified | Re-index after all skills are created |

## Risks

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| FP skill produces invalid counts without approved tables | High | Default to worksheet/review mode; block calculation until `counting-workbook.md` is populated |
| Transcript-derived rules contradict ISO standard | Med | Skills cite external sources as authoritative; transcript as illustrative only |
| Skills exceed token budget and become hard to invoke | Med | Move all long content to `references/`; enforce 1000-token hard cap |
| Estimates used as commitments | High | Mandatory `[HUMAN REVIEW REQUIRED]` block in every size/forecast output |
| Story points compared across teams | Med | `agile-story-estimation` blocks cross-team comparisons explicitly |
| Skill-registry not updated after creation | Low | `skill-registry` sync is the final task in apply |

## Rollback Plan

Skills are new files under `skills/`. If a skill produces wrong output or violates the style guide, delete or rename the offending `SKILL.md`/`references/` files and restore `.atl/skill-registry.md` to its pre-change state. No existing files are modified except `skill-registry.md`.

## Dependencies

- `docs/skill-style-guide.md` must remain valid as the authoring contract during apply
- Organization must supply DoR, DoD, productivity baselines, and FP counting tables before estimation outputs can be used for formal proposals

## Success Criteria

- [ ] All 7 `SKILL.md` files exist under `skills/` and pass `bash skills/setup_test.sh`
- [ ] Each skill body is ≤ 1000 tokens; long content lives in `references/`
- [ ] Router skill correctly identifies at least 5 distinct estimation request types
- [ ] FP skill defaults to worksheet/review mode and blocks calculation output when no counting workbook is present
- [ ] Every size/forecast output includes a `[HUMAN REVIEW REQUIRED]` gate
- [ ] `.atl/skill-registry.md` reflects all 7 new skills
- [ ] No skill output compares story points across teams as absolute units

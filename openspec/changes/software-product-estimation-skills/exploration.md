# Exploration: software-product-estimation-skills

## Current State

The project is a documentation and skill-authoring workspace, not an application repository. OpenSpec is initialized in hybrid persistence mode in `openspec/config.yaml`; no main specs exist under `openspec/specs/`; no project-local `skills/**/SKILL.md` files were found; `.atl/skill-registry.md` indexes user/global skills only; and `docs/skill-style-guide.md` matches the injected skill style guide.

Relevant inspected files:

- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/openspec/config.yaml` — project context, hybrid persistence, strict TDD flag, Bash test runner metadata, and OpenSpec rules.
- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/openspec/specs/` — no spec markdown files found.
- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/skills/` — no project-local `SKILL.md` files found.
- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/docs/skill-style-guide.md` — LLM-first skill authoring contract.
- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/.atl/skill-registry.md` — generated registry with relevant global skills: `skill-creator`, `cognitive-doc-design`, and SDD skills.
- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/[P0095] Tech Talks _ 18_ estimacion de productos de software, una primera aproximacion [PnP].vtt` — complete source transcript processed from line 1 through line 4772.

## Transcript Findings

### Core framing

The talk frames software product estimation as a disciplined answer to stakeholder questions:

- How large is the thing to build?
- How long will it take?
- How much will it cost?
- How many people are needed?
- When will it be done?

The speaker repeatedly separates **size** from **duration/cost/staffing**. First estimate product size from requirements, scope, problem space, solution space, and conceptual structure. Then convert size into schedule, people, and cost using productivity, capacity, Definition of Done, quality needs, technology, and risk assumptions.

### Meeting concepts and terminology

- **Problem space**: the business problem and context the customer needs solved.
- **Solution space**: the proposed software slice that addresses that problem.
- **Desired requirements**: initial wants from the client; estimates are better when these are stable.
- **Scope / bounded context**: the module, product area, or domain boundary being estimated.
- **Conceptual model / domain model**: the entities, processes, and structure that make the product countable.
- **Requirement stability**: unstable requirements can hide “Goliath” work inside apparently small scope.
- **Decomposition**: large uncertain work should be split into smaller parts, milestones, modules, stories, or components.
- **Expert judgment / Delphi-style estimation**: ask experienced people, compare similar projects, and reconcile differences.
- **Proxy-based estimation**: use familiar attributes or component categories to infer size, such as rooms/bathrooms/parking for home size.
- **Agile estimation**: estimate backlog items iteratively, commonly with Planning Poker, and deliver increments each iteration.
- **Function Point Analysis**: formal size measurement based on business-facing data and transactional functions.
- **Definition of Ready**: criteria a story must satisfy before estimation/planning.
- **Definition of Done**: explicit agreement of what completion includes: implementation, unit tests, integration, infrastructure, docs, branches/environments, etc.
- **INVEST**: Independent, Negotiable, Valuable, Estimable, Small, Testable.
- **Technical enabler**: supporting technical work needed to make a user story possible.
- **Unadjusted Function Points**: raw count from data and transaction functions.
- **Adjusted Function Points**: raw count modified by non-functional/general system characteristics.
- **Productivity layer**: technology/team/productivity conversion applied after functional size is known.

### Estimation workflow extracted from the meeting

1. Clarify the customer problem and proposed solution slice.
2. Stabilize or explicitly mark volatile requirements.
3. Define the scope/bounded context to estimate.
4. Choose a method appropriate to the available inputs:
   - expert/analogy when only prior similar experience exists;
   - proxy-based when a conceptual design and comparable components exist;
   - agile sizing when backlog stories are available and iteration planning is needed;
   - Function Point Analysis when functional size must be counted more formally.
5. Decompose large or unclear work into smaller pieces.
6. Identify functional work and non-functional drivers separately.
7. Estimate size first; only then convert to time, cost, and staffing.
8. Capture assumptions, unknowns, and confidence.
9. Re-estimate at lifecycle checkpoints: proposal, design, QA, delivery, and maintenance/change work.
10. Keep expectations aligned as features evolve so the client does not keep an outdated “small” mental model.

### Method-specific findings

#### Expert judgment / Delphi-style

- Ask experts for similar past projects and their durations/costs.
- Compare analogies carefully; similarity must be validated, not assumed.
- Use multiple experts to contrast perspectives.
- Beware hidden details: “the devil is in the details” and missed requirements can break the estimate later.

#### Proxy-based estimation

- Build a conceptual design first.
- Divide the product into constituent parts.
- Classify each part as small/medium/large.
- Use a prior-measurement database or proxy table to map parts to size/effort.
- Distinguish new work from modifications/refactors of existing work.
- Home/apartment analogy: rooms, bathrooms, parking, and family size become proxies for square meters and cost.

#### Agile estimation

- Begin with a backlog after understanding the problem and solution.
- Prioritize stories and estimate iteratively by sprint/cycle.
- Use Planning Poker-style cards and discussion to converge on estimates.
- Participants who estimate should be those who will do/suffer the work; Product Owner clarifies but does not size unless also implementing.
- Differences between high and low estimates should trigger explanation and reconciliation.
- Stories should satisfy INVEST and Definition of Ready before being estimated.
- Keep stories small enough to produce visible progress, with transcript heuristics around half-day or one-day chunks for very granular work.
- Definition of Done must be explicit because “done” may include tests, integration, infrastructure provisioning, documentation, and environment/branch state.
- Points are a proxy; hours may be easier for teams starting out. Points become team-local and are hard to compare across teams.

#### Function Point Analysis

The talk presents Function Point Analysis as a more formal, ISO-standardized, technology-agnostic way to measure business functionality. It is record/data-oriented and intended to be interpretable by users so they can validate whether requested functionality was counted.

Extracted steps:

1. Determine count type: new/development, enhancement/modification, or application count.
2. Determine application boundary/scope/bounded context.
3. Count unadjusted function points from data functions and transactional functions.
4. Apply adjustment values for non-functional/general system characteristics.
5. Produce adjusted function points.

Count categories mentioned:

- **ILF — Internal Logical File**: business data maintained by the application.
- **EIF — External Interface File**: data consumed from/owned by another system.
- **EI — External Input**: user/system input that updates or affects application data.
- **EO — External Output**: output/report with processing or derived data.
- **EQ — External Inquiry**: query/retrieval interaction.
- **DET — Data Element Type**: business-significant field/element.
- **RET — Record Element Type**: logical subgroup/record within a data function.
- **FTR — File Type Referenced**: data function referenced by a transaction.

Counting heuristics from the transcript:

- Use mockups, entity-relationship diagrams, endpoint specifications, stories, and integration notes as inputs.
- Count business-significant data elements and records, not pure navigation.
- Do not count menus, navigation links, or buttons that only navigate/cancel without business-data effect.
- A simple `Project` entity example had fields like project name, type, and description; these become DETs under a RET/entity.
- Transaction complexity grows when reports/outputs join multiple entities/FTRs or require extra computation/integrations.
- AI-related calls or integrations can justify additional complexity because “it is not just adding a button.”
- Transcript example: FP Tracker yielded 99 unadjusted function points and 95.04 adjusted function points after applying adjustment factors.
- Non-functional adjustment examples included high transaction rate, user efficiency, reusability, and stability.
- Function points should remain separate from productivity/time/cost conversion.

### Examples extracted

- **Apartment/home proxy**: estimate by number of rooms, bathrooms, parking spaces, and size categories rather than starting with an exact square-meter guess.
- **Moon trip decomposition**: split an unknown giant goal into team, materials, rocket launch, milestones, and sub-activities before estimating.
- **Adding people late**: more staff can be a double-edged sword due to onboarding, knowledge transfer, and communication overhead; nine women do not make a baby in one month.
- **Children/communication analogy**: each added team member increases communication relationships and latency.
- **Video game racing realism story**: a user-facing story about immersive race audio depends on technical enablers like sound systems, recordings, event triggers, and acceptance criteria.
- **FP Tracker application**: a function-point-counting app with project management, entities, ILF/EIF, inputs, outputs, queries, and reports used to demonstrate FP counting.
- **UAT bugs question**: bug volume affects estimates; modified code can be more expensive than base/new code because understanding existing behavior is part of the work. Related bugs may need grouping, but each independent issue/story still needs clear scope.
- **Points vs hours question**: points are a proxy to standardize team work; hours are a reasonable starting point; points are hard to compare across self-organized teams.
- **Template question**: there is currently no standardized organizational estimation guide/template; seed teams are starting to encourage Planning Poker with Definition of Ready.

### Implicit heuristics and risks

- Estimates become more reliable when requirements and scope are explicit.
- Hidden non-functional requirements can dominate effort.
- Existing/modified code often needs comprehension time and can cost more than new code.
- UAT defect volume can radically alter remaining effort.
- AI can help extract entities, mockup fields, endpoints, and candidate counts, but it should not replace the method or human accountability.
- Estimates should expose uncertainty; the only exact duration is known after the project ends.
- Treat size as a measure, not a promise.
- Avoid cross-team comparison of story points.
- Keep customer expectations synchronized as features and size evolve.
- Do not weaponize estimates as fixed commitments without assumptions and confidence.

## Candidate Skills

### 1. `software-product-estimation`

Purpose: Entry/router skill for choosing the right estimation workflow from messy user requests.

Trigger: User asks to estimate a software product, feature, backlog, proposal, mockup, transcript, endpoint set, or delivery forecast.

Inputs: User request, available artifacts, scope notes, backlog, mockups, architecture/design notes, team/capacity data, requested output type.

Outputs: Selected estimation path, required inputs, assumptions, method boundary, and next-step prompt or handoff to a focused estimation skill/reference.

Workflow: Classify the request as discovery, agile story estimation, proxy/component sizing, function point sizing, forecast conversion, or estimate review; validate minimum inputs; refuse false precision; route to the focused workflow; keep size separate from duration/cost.

Evidence base: Transcript separation of size/duration/cost; multiple methods; skill style guide preference for compact focused skills.

Boundaries: Does not perform all methods in one runtime body. Does not produce deterministic commitments from incomplete inputs.

### 2. `estimation-discovery`

Purpose: Extract estimation-ready facts from ambiguous product material before applying a sizing method.

Trigger: User provides transcript, brief, vague requirements, notes, mockups, diagrams, APIs, or asks “can you estimate this?”

Inputs: Raw notes/transcript, product goals, requirements, user stories, mockups, entity hints, integrations, constraints, non-functional requirements.

Outputs: Estimation brief with problem space, solution space, scope/bounded context, actors, capabilities, entities, transactions, integrations, non-functional drivers, assumptions, unknowns, and readiness warnings.

Workflow: Normalize the source; separate business problem from solution; identify boundary; extract functional/non-functional work; list entities/processes/screens/integrations; identify volatility; recommend agile/proxy/FP/clarification path.

Evidence base: Transcript emphasis on stable requirements, problem/solution space, conceptual model, decomposition, and AI as an extraction aid.

Boundaries: Does not calculate final effort/cost. Does not invent missing business rules.

### 3. `agile-story-estimation`

Purpose: Guide backlog/story estimation using readiness checks, Planning Poker reasoning, and team-local calibration.

Trigger: User asks to estimate stories, prepare Planning Poker, validate backlog readiness, split oversized stories, or review points/hours.

Inputs: Backlog items, acceptance criteria, DoR, DoD, team capacity, team historical estimates/actuals, roles participating.

Outputs: Story readiness assessment, estimation notes, uncertainty spread, high/low rationale, split/clarification recommendations, capacity caveats.

Workflow: Check INVEST and DoR; ensure implementers size the work; have PO clarify but not override implementer estimate; capture high/low reasons; flag oversized or non-estimable stories; relate estimates to capacity only with team-local data.

Evidence base: Transcript Planning Poker section, INVEST, DoR/DoD, implementers estimate because they do the work, points/hours Q&A.

Boundaries: Does not treat points as universal. Does not force consensus when disagreement indicates uncertainty. Does not estimate unready stories as if ready.

### 4. `proxy-component-estimation`

Purpose: Estimate by decomposing a conceptual design into comparable components and size classes.

Trigger: User has a conceptual design or product outline but no formal function point worksheet/backlog.

Inputs: Component/module list, comparable past work, small/medium/large definitions, prior measurement table, new-vs-modified classification, non-functional drivers.

Outputs: Component sizing worksheet, proxy rationale, assumptions, comparable examples, uncertainty notes, and recommended conversion inputs.

Workflow: Define boundary; decompose into components; classify each component; compare against historical/proxy examples; mark new/modified/refactor work; surface hidden non-functional and integration costs.

Evidence base: Transcript apartment proxy, conceptual design/decomposition, prior measurements, new vs modification distinction.

Boundaries: Does not claim formal FP accuracy. Requires calibrated local proxy examples for stronger forecasts.

### 5. `function-point-estimation`

Purpose: Produce or review a structured Function Point Analysis from product artifacts.

Trigger: User asks for function points, functional size, IFPUG/ISO style counting, ILF/EIF/EI/EO/EQ, DET/RET/FTR, or formal estimation.

Inputs: Count type, application boundary, entity model, mockups, endpoints, reports, queries, integrations, non-functional adjustment factors, approved counting tables/manual.

Outputs: Count worksheet with ILF/EIF/EI/EO/EQ candidates, DET/RET/FTR rationale, complexity class, unadjusted FP, adjustment notes, adjusted FP when justified, and open counting questions.

Workflow: Confirm count type and boundary; classify data functions; classify transactional functions; count business-significant DETs/RETs/FTRs; ignore navigation-only UI; apply approved complexity/weight tables; document adjustments; keep productivity conversion separate.

Evidence base: Transcript Function Point section, ISO mention in Q&A, FP Tracker example, non-functional adjustment discussion.

Boundaries: Must not fabricate official table values unless provided by local references or approved source. Must distinguish size from effort/duration/cost. Must flag AI-extracted counts for human review.

### 6. `estimation-to-plan`

Purpose: Convert size estimates into forecast ranges for duration, cost, and staffing.

Trigger: User asks “how long?”, “how much?”, “how many people?”, “when will it be done?”, or needs proposal forecast from size.

Inputs: Size estimate, method used, confidence, productivity baseline, team capacity, cost rates, DoD, QA/UAT expectations, technology, dependencies, risk buffer.

Outputs: Forecast range, assumptions, capacity model, cost/staffing implications, risk register, and review checkpoints.

Workflow: Validate size measure; choose productivity basis; account for DoD, tests, QA, UAT defects, infra, docs, non-functionals, tech stack; model capacity; expose confidence; explain staffing tradeoffs and communication overhead.

Evidence base: Transcript separation of FP from productivity, staffing cautions, UAT bug question, Definition of Done discussion.

Boundaries: Does not promise deterministic dates. Does not compare story points across teams. Does not recommend adding people without onboarding/communication costs.

### 7. `estimation-review`

Purpose: Review existing estimates for missing scope, hidden complexity, and invalid assumptions.

Trigger: User asks to audit an estimate, proposal, timeline, story sizing, FP worksheet, or explain estimation failure.

Inputs: Existing estimate, scope, requirements, backlog, DoR/DoD, architecture notes, historical actuals, UAT defects, change requests, assumptions.

Outputs: Severity-ordered findings, missing assumptions, scope gaps, over/under-estimation risks, correction recommendations, and stakeholder questions.

Workflow: Verify problem/solution/scope; compare functional/non-functional coverage; inspect readiness and DoD; check modified-code and technical debt impact; validate productivity conversion; flag false precision and cross-team point misuse.

Evidence base: Transcript risks around hidden requirements, modified code, UAT bugs, non-functional drivers, and expectation drift.

Boundaries: Review-only unless user asks to rewrite. Does not silently normalize estimates without rationale.

### 8. `construction-estimation-analogy`

Purpose: Use construction-style analogies to teach or structure proxy estimation without confusing analogy with proof.

Trigger: User needs an intuitive explanation of estimation, proxy sizing, decomposition, or scope/cost tradeoffs.

Inputs: Product scope, comparable physical/construction analogy, component dimensions, quality levels, constraints.

Outputs: Analogy-backed explanation, mapping table from construction concepts to software concepts, and limits of the analogy.

Workflow: Map rooms/materials/quality/square meters to features/components/non-functionals/size; show where analogy helps; explicitly state where software differs.

Evidence base: Transcript apartment/home, construction/maestro de obra, materials/quality, moon trip decomposition.

Boundaries: Teaching/design aid only. Does not replace actual software estimation method.

### 9. `estimation-knowledge-artifact`

Purpose: Turn meeting recordings or transcripts into canonical internal estimation references.

Trigger: User asks to convert `.vtt`, workshop notes, talks, or recordings into reusable guidance for skills/docs.

Inputs: Transcript, slides/links if available, local style guide, approved sources.

Outputs: Clean notes, glossary, workflows, examples, source-backed reference docs, and candidate skill references.

Workflow: Remove VTT noise; preserve meeting concepts/examples; separate meeting claims from validated method rules; chunk into references/checklists/templates; avoid bloating runtime `SKILL.md` files.

Evidence base: Current transcript processing; cognitive-doc-design; skill-creator rule to move long background into `references/`.

Boundaries: Does not create final skills during explore. Does not overfit one talk where official method references are required.

## Recommended Skill Architecture

Use one entry skill plus focused method skills and references, rather than one large skill.

Recommended first construction set:

- `skills/software-product-estimation/SKILL.md` — router/entry workflow.
- `skills/estimation-discovery/SKILL.md` — messy-input extraction and readiness.
- `skills/agile-story-estimation/SKILL.md` — Planning Poker/INVEST/DoR/DoD workflow.
- `skills/proxy-component-estimation/SKILL.md` — conceptual design and component proxy sizing.
- `skills/function-point-estimation/SKILL.md` — conservative FP worksheet/review workflow.
- `skills/estimation-to-plan/SKILL.md` — size-to-duration/cost/staffing forecast.
- `skills/estimation-review/SKILL.md` — audit existing estimates.

Keep each `SKILL.md` compact per the style guide and move long examples, official tables, transcript notes, and templates into local `references/` or `assets/`.

Likely supporting references for later phases:

- `skills/software-product-estimation/references/meeting-notes.md`
- `skills/agile-story-estimation/references/planning-poker-checklist.md`
- `skills/proxy-component-estimation/references/proxy-sizing-guide.md`
- `skills/function-point-estimation/references/counting-workbook.md`
- `skills/estimation-to-plan/references/forecast-model.md`
- `skills/estimation-review/references/review-checklist.md`

## Affected Areas

- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/skills/` — future project-local skill directories would be added here.
- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/docs/skill-style-guide.md` — governs final skill style.
- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/.atl/skill-registry.md` — should be refreshed later if skills are created/synced.
- `/home/sebastian-ramirez/trabajo/estimationProductSoftware/openspec/changes/software-product-estimation-skills/` — active OpenSpec change folder.

## Approaches

1. **Single comprehensive estimation skill** — one `SKILL.md` covers discovery, agile, proxy, FP, forecasting, and review.
   - Pros: One trigger surface.
   - Cons: Violates compact skill guidance; mixes methods; high false-precision risk.
   - Effort: Medium.

2. **Router plus focused method skills** — one entry skill plus specialized estimation skills and references.
   - Pros: Best fit for skill style; boundaries stay clear; formal FP can remain conservative; easier to test/review.
   - Cons: More files and registry/sync work later.
   - Effort: Medium.

3. **Reference-first docs only** — cleaned transcript notes and checklists without executable skills.
   - Pros: Lowest methodological risk; useful human reference.
   - Cons: Does not satisfy reusable skill goal.
   - Effort: Low.

## Recommendation

Proceed to proposal with Approach 2: a compact `software-product-estimation` router plus focused skills for discovery, agile story estimation, proxy component estimation, Function Point estimation, forecast conversion, and estimate review. Keep Function Point Analysis conservative until approved counting tables/manuals and local productivity baselines are provided.

## Risks

- Function Point Analysis is formal; transcript-derived rules are insufficient for official counting tables and weights.
- Story points and hours are team-local; skills must prevent cross-team point comparisons.
- Missing DoR/DoD, productivity baselines, and organizational templates limit forecast accuracy.
- AI extraction from mockups/transcripts/endpoints can hallucinate or miss business-significant data.
- Estimates can be mistaken for commitments unless assumptions and confidence are explicit.
- Non-functional requirements, infra, QA/UAT, docs, technical debt, and modified-code comprehension can dominate effort.
- A monolithic skill would exceed the style guide and be harder to invoke safely.
- Primary source is Spanish and VTT-noisy; later references should preserve intent while normalizing artifact language according to project convention.

## Open Questions

- Should final skill artifacts be authored in English by default, or should Spanish references be kept because the meeting and likely users are Spanish-speaking?
- Which skills should be included in the first proposal slice to stay reviewable?
- Does the organization have official DoR, DoD, estimation templates, FP tables/manuals, productivity baselines, or cost-rate policies?
- Should the FP skill calculate counts or only produce/review worksheets until official references are supplied?
- Should AI-generated estimates include a mandatory human sign-off line?
- Should cleaned transcript notes be created as a reference artifact in a later phase?

## Ready for Proposal

Yes. The next SDD phase should define a bounded proposal for creating project-local estimation skills and references. Do not build a full estimation calculator unless official counting tables, productivity baselines, and validation expectations are supplied.

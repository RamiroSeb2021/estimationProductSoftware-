# Router Decision Tree

Use this reference after loading `software-product-estimation/SKILL.md`. Select one route only. When signals conflict, prefer the first matching route in priority order unless the user explicitly narrows the goal.

## Priority Order

| Priority | Route | Strong signals | Minimum inputs before handoff |
|---|---|---|---|
| 1 | `estimation-review` | Existing estimate, quote, roadmap, proposal, delivery date, audit request | Artifact to review, stated method if known, scope covered, assumptions or lack of them |
| 2 | `function-point-estimation` | Function Point, FP, IFPUG, ISO/IEC 20926, ILF, EIF, EI, EO, EQ, formal functional size | Application boundary, user-visible functions, data groups, transaction descriptions, counting workbook status |
| 3 | `agile-story-estimation` | Backlog, stories, acceptance criteria, Planning Poker, story points, sprint planning | Stories, acceptance criteria, team context, DoR/DoD, local historical calibration if forecast is requested |
| 4 | `proxy-component-estimation` | Components, modules, conceptual design, S/M/L sizing, comparable past work | Component list, new/modified/refactor status, NFR drivers, local proxy examples if effort conversion is requested |
| 5 | `estimation-to-plan` | How long, cost, staffing, when, forecast, capacity, deadline | Validated size, productivity baseline, DoD, team capacity, technology context, uncertainty assumptions |
| 6 | `estimation-discovery` | Vague idea, transcript, meeting notes, missing boundary, unclear artifact | Any available notes plus known business goal; missing sections may be `[UNKNOWN]` |

## Routing Rules

- Use `estimation-review` first when the user brings an existing estimate, even if the estimate mentions points, function points, or dates.
- Use `function-point-estimation` for formal functional size language. Do not calculate counts unless the specialized skill confirms an approved workbook.
- Use `agile-story-estimation` only when the unit of work is a backlog/story and implementer-led team estimation is plausible.
- Use `proxy-component-estimation` when the artifact is architectural or component-oriented rather than story-oriented.
- Use `estimation-to-plan` only after size exists. If the user asks for duration without size, route to `estimation-discovery` or a sizing method first.
- Use `estimation-discovery` when the method cannot be chosen safely from the available inputs.

## False-Precision Guard

If the user asks for a deterministic answer such as "how many days?" or "give me the date", return:

```markdown
> [HUMAN REVIEW REQUIRED]
> I cannot produce a deterministic estimate from the current inputs. Provide size, assumptions, DoD, team capacity, productivity baseline, and uncertainty tolerance before converting to a forecast range.
```

## Handoff Template

```markdown
Selected route: `<skill-name>`
Why: <evidence from user input>
Minimum missing inputs: <short list or "None for first pass">
Safety gates: <false precision / local calibration / workbook / human review>
Next action: Load `skills/<skill-name>/SKILL.md` and continue there.
```

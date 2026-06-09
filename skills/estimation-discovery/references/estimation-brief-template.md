# Estimation Brief Template

Use this template before applying any estimation method. Populate from provided artifacts only. If a fact is absent, write `[UNKNOWN]`; do not infer business rules.

## Brief

| Section | Content |
|---|---|
| Problem space | Business problem, user pain, or opportunity. |
| Solution space | Proposed product, feature, workflow, or system change. |
| Scope / bounded context | In-scope area, out-of-scope area, system boundary. |
| Actors | Human roles, external systems, services, administrators. |
| Capabilities | User-visible capabilities or business functions. |
| Entities | Business data concepts, records, files, master data. |
| Transactions | Create, update, delete, query, report, import, export, notifications. |
| Integrations | APIs, files, queues, third-party systems, AI/LLM calls. |
| Non-functional drivers | Security, performance, availability, audit, privacy, compliance, scale. |
| Assumptions | Explicitly stated assumptions only; mark source. |
| Unknowns | Missing boundaries, rules, acceptance criteria, data, dependencies. |
| Readiness warnings | Why sizing may be unsafe or incomplete. |

## Readiness Checklist

- [ ] Product/application boundary is clear.
- [ ] Actors and primary workflows are identified.
- [ ] Core capabilities have acceptance criteria or observable outcomes.
- [ ] Main entities and transactions are visible.
- [ ] Integrations and NFR drivers are listed.
- [ ] Team context, proxy history, or FP workbook exists for the target method.

## Method Recommendation Rules

| Ready evidence | Recommend |
|---|---|
| Backlog items with acceptance criteria, team context, and DoD/DoR | `agile-story-estimation` |
| Component list with new/modified/refactor status and local comparable work | `proxy-component-estimation` |
| Functional boundary, data groups, and transaction candidates | `function-point-estimation` |
| Missing boundary, unclear rules, no acceptance criteria | `NOT READY` |

## Clarification Questions

Ask only for the minimum missing inputs blocking the next method. Prefer specific questions tied to `[UNKNOWN]` sections.

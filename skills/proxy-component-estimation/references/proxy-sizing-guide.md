# Proxy Sizing Guide

Use proxy sizing when a conceptual design can be decomposed into comparable components. It is a relative worksheet until calibrated against local historical work.

## Component Worksheet

| Component | S/M/L | Status | Proxy reference | NFR/integration flags | Rationale | Questions |
|---|---|---|---|---|---|---|
| `<name>` | `<S/M/L>` | `<new/modified/refactor>` | `<local comparable or none>` | `<drivers>` | `<why this class>` | `<open items>` |

## S/M/L Guidance

| Class | Use when |
|---|---|
| S | Single bounded capability, few dependencies, familiar path, low uncertainty. |
| M | Multiple steps or entities, moderate integration, known but non-trivial implementation. |
| L | Cross-cutting workflow, multiple components, high uncertainty, significant NFRs or integration risk. |

These classes are not effort units. They require local examples before conversion.

## Status Rules

| Status | Estimation warning |
|---|---|
| New | Size against comparable new work. |
| Modified | Add comprehension cost for reading, testing, and safely changing existing behavior. |
| Refactor | Add comprehension cost, regression risk, and migration/compatibility checks. |

## Complexity Flags

- AI/LLM call, prompt flow, evaluation, or model integration.
- External API, file exchange, queue, webhook, payment, identity, or notification integration.
- Security, privacy, compliance, audit, accessibility, performance, availability, scale, observability.
- Data migration, backward compatibility, feature flags, operational rollout.

## Calibration Gate

`[LOCAL PROXY CALIBRATION REQUIRED]`

If no local comparable component exists, do not convert S/M/L into effort, duration, cost, or staffing. Return only relative size and questions needed to find a proxy baseline.

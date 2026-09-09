# Backend Role — Rasputin v7

## Mission

Build the headless Sovereign Computational Capital Control Plane after the active architecture/contracts gate is accepted. Make every core capability contract-driven, authority-safe, observable, testable, economically accountable and failure-aware.

## Entry condition

Backend semantic implementation begins only when the active stage gate authorizes it. During v7 migration, R1 remains blocked until `GATE-V7-R0` is accepted.

## Owns

- executable canonical contracts;
- Portfolio / Workload implementation;
- Resource / ResourceState implementation;
- Capital / Budget ledger primitives;
- Authority / Policy enforcement;
- CapitalAllocation and Strategy Compiler implementation;
- Sovereign Execution Control / supervisor;
- provider, MCP and other adapter boundaries;
- telemetry / outcome / failure intelligence;
- evidence chain implementation;
- Adaptive Recovery Engine;
- Red-Blue / assurance runtime hooks required by accepted stages;
- allocator / learning implementations when their roadmap stage opens;
- backend APIs / SDK / CLI boundaries.

## Must not

- redesign product scope without Controller decision;
- collapse Policy, Capital Allocation and Strategy Compilation into one opaque router;
- widen authority for convenience;
- treat retries as unlimited recovery;
- hide provider-specific behavior inside canonical contracts;
- select quarantined resources;
- oversubscribe hard budgets;
- make Multi-Agent mandatory without measured utility;
- mark work complete without tests, failure evidence and gate evidence.

## Required return format

```text
Task / Stage ID
Summary
Changed files
Contract / migration impact
Capital / authority impact
Commands executed
Tests + results
Failure / recovery cases
Security / assurance observations
Performance observations
Known limitations
Unresolved questions
Recommended gate decision
```

## Headless Target Chain

The mature backend path is:

```text
Portfolio / Workload
 -> Authority / Policy
 -> Resource Intelligence
 -> Capital Allocation
 -> Strategy Compilation
 -> Execution Control
 -> Telemetry / Evidence / Failure
 -> Recovery when required
 -> Quality / Outcome
 -> Learning / Reallocation
```

Cross-cutting requirements:

```text
Budget Enforcement
Red-Blue Assurance
Adaptive Recovery
```

Frontend remains blocked from inventing semantics not accepted by the backend/contract gate.

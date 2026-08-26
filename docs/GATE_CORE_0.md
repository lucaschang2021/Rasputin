# Rasputin — GATE-CORE-0 Review

> Gate: GATE-CORE-0  
> Scope: Architecture & Contracts  
> Decision: PASS WITH CONTROLLED ASSUMPTIONS  
> Date: 2026-08-26

## 1. Reviewed Artifacts

- `README.md`
- `docs/ARCHITECTURE.md`
- `docs/PRE_DEVELOPMENT.md`
- `docs/contracts/EXECUTION_SCHEMA.md`
- `docs/contracts/POLICY_CONTRACT.md`
- `docs/contracts/EVIDENCE_CONTRACT.md`

## 2. Gate Criteria

### Architecture coherence

PASS.

The kernel is consistently defined around:

```text
Execution Schema
Policy
Economics
Routing
Telemetry
Evidence
Optimization
```

No P0 component requires blockchain, zk, A2A, polished UI or enterprise multi-tenancy.

### Separation of concerns

PASS.

Policy, Economics, Execution and Evidence are explicitly separated.

### Trust claims bounded

PASS.

P0 claims only tamper-evident local provenance under a local-runtime trust assumption. Remote attestation, semantic correctness and zero-knowledge guarantees remain future work.

### Scope firewall

PASS.

Commoditized/integration capabilities are not treated as core moat and P1/P2/P3 features are prevented from blocking P0.

### Backend implementability

PASS.

Backend can implement CORE-1 schemas and fixtures without inventing new top-level architecture.

## 3. Controlled Assumptions

The following are intentionally unresolved until implementation evidence exists:

1. programming-language and schema-library choice;
2. canonical serialization implementation choice;
3. persistent store choice;
4. concrete LiteLLM/provider integration details;
5. quality evaluator design;
6. economics objective weighting;
7. runtime attestation standard/adapters.

These are implementation or later-phase decisions and do not block CORE-1.

## 4. Decision

`GATE-CORE-0 = PASS`

Rasputin state changes from:

```text
PRE-DEVELOPMENT / CORE-0
```

to:

```text
ACTIVE ALPHA DEVELOPMENT / CORE-1
```

Only CORE-1 work is authorized next. CORE-2+ work remains blocked until `GATE-CORE-1` passes.

## 5. CORE-1 Backend Dispatch

### CORE-1-T1 — Canonical Task Schema

Objective:

Implement the Task object defined in `EXECUTION_SCHEMA.md`.

Deliverables:

- typed schema/model;
- validation;
- serialization;
- fixture: valid minimal task;
- fixture: invalid budget/task constraints;
- unit tests.

Forbidden scope:

- provider routing;
- API calls;
- database integration;
- UI;
- blockchain;
- Agent orchestration.

### CORE-1-T2 — PolicyDecision Schema

Implement the canonical PolicyDecision object only.

Deliverables:

- typed model;
- validation;
- stable serialization;
- allow/deny fixtures;
- tests.

No policy engine logic yet.

### CORE-1-T3 — ExecutionPlan Schema

Implement canonical ExecutionPlan and strategy sub-objects.

Required cases:

- cloud model strategy;
- local strategy;
- tool-using strategy;
- fallback plan.

No routing algorithm yet.

### CORE-1-T4 — Run / Telemetry / Quality Schemas

Implement:

- Run;
- TelemetryRecord;
- QualityEvaluation.

Tests must cover failed run, retry-relevant error metadata and finalized success.

### CORE-1-T5 — Versioning & Golden Fixtures

Build the canonical fixture suite required by the execution contract.

Required fixtures:

1. cloud model run;
2. local-model run;
3. tool-using run;
4. denied-by-policy task;
5. budget-constrained fallback run;
6. failed run with retry;
7. finalized run with evidence references.

Define compatibility tests for schema version handling.

## 6. GATE-CORE-1 Acceptance

CORE-1 passes only if:

```text
all canonical objects implemented
+ validation tests pass
+ serialization tests pass
+ golden fixtures pass
+ versioning behavior is explicit
+ no forbidden P1+ dependency introduced
```

The Controller must review the evidence before CORE-2 begins.

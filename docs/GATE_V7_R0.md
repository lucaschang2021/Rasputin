# Rasputin v7 — GATE-V7-R0

> **Gate:** Strategic Constitution / Architecture / Contract Migration  
> **Status:** ACCEPTED  
> **Decision date:** 2026-09-09  
> **Purpose:** freeze the v7 strategic/contract baseline before executable R1 implementation.

## 1. Reviewed Documents

Controller consistency review covered:

- `README.md`;
- `docs/00-PROJECT-CONTROL.md`;
- `docs/01-MASTER-TECHNICAL-DESIGN.md`;
- `docs/02-DELIVERY-BOARD.md`;
- `docs/03-DEVELOPMENT-WORKFLOW.md`;
- `docs/04-PROJECT-STATE.md`;
- `docs/05-V7-STRATEGIC-TECHNICAL-CONSTITUTION.md`;
- `docs/10-BACKEND-WORK-PACKAGE.md`;
- `docs/ARCHITECTURE.md`;
- `docs/PRE_DEVELOPMENT.md`;
- `docs/GATE_CORE_0.md` historical boundary;
- `docs/contracts/EXECUTION_SCHEMA.md`;
- `docs/contracts/POLICY_CONTRACT.md`;
- `docs/contracts/EVIDENCE_CONTRACT.md`;
- `docs/contracts/CAPITAL_CONTRACT.md`;
- `docs/contracts/RESILIENCE_CONTRACT.md`;
- role documents under `docs/roles/`.

## 2. Strategic Acceptance Criteria

- [x] Rasputin is defined as a Sovereign Computational Capital Control Plane.
- [x] Workload Portfolio sits above per-execution routing.
- [x] Execution remains the atomic economic object.
- [x] `DO_NOT_EXECUTE / DEFER / WAIT_FOR_INFORMATION` are first-class decisions.
- [x] Resource Intelligence is broader than a model registry.
- [x] Capital Allocation is distinct from Policy/Authority and Strategy Compilation.
- [x] Outcome value is distinct from quality score.
- [x] Multi-Agent is an Execution Strategy, not core identity.
- [x] Gateways/RAG/orchestration/provenance/blockchain/TEE/ZK are adapters, standards or research by default.
- [x] Red-Blue Assurance is a permanent cross-cutting loop.
- [x] Adaptive Recovery follows `Detect → Diagnose → Contain → Recover → Verify → Reallocate → Learn`.
- [x] Recovery is budgeted and may terminate economically.
- [x] Risk, Irreversibility and Recovery Budgets are explicit.

## 3. Contract Acceptance Criteria

- [x] Canonical Portfolio and Workload objects exist.
- [x] Resource and ResourceState objects exist.
- [x] BudgetEnvelope / BudgetLedger semantics exist.
- [x] PolicyDecision / AuthorityEnvelope semantics exist.
- [x] CapitalAllocation is distinct from ExecutionPlan.
- [x] FailureRecord / RecoveryEpisode exist.
- [x] OutcomeRecord supports delayed downstream outcomes.
- [x] AssuranceResult supports bounded Red-Blue / chaos evidence.
- [x] Evidence binds policy, authority, allocation, plan and recovery lineage.
- [x] Unknown major versions fail explicitly.
- [x] v6 Task/ExecutionPlan/Run migration mapping is documented.

## 4. Safety / Authority Acceptance Criteria

- [x] Allocator cannot widen policy.
- [x] Strategy Compiler cannot widen policy.
- [x] Fallback/recovery cannot widen policy.
- [x] Hard budget exhaustion is defined as an execution-control boundary.
- [x] Cumulative irreversibility can block individually legal actions.
- [x] Quarantined resources cannot be selected.
- [x] Red-team tooling has explicit bounded test authority.
- [x] Shadow Mode cannot intentionally produce irreversible production side effects.
- [x] Failure history cannot be erased by successful recovery.

## 5. Economic Acceptance Criteria

- [x] Nominal cost and effective/shadow cost are distinct.
- [x] Shared budgets can apply at portfolio scope.
- [x] Recovery cost is separately accountable.
- [x] Opportunity cost/scarcity can affect allocation without changing nominal API price.
- [x] ROCC is defined as a future benchmark metric and is not claimed as validated before measurement.

## 6. Roadmap Acceptance Criteria

- [x] R1–R16 are dependency ordered.
- [x] Adaptive Recovery v0 precedes autonomous online allocation.
- [x] Red-Blue v0 has an explicit stage and gate.
- [x] Learned allocation requires deterministic baseline, offline evidence and rollback.
- [x] Inter-org markets, settlement and Zero-Knowledge Compliance remain R16 research until earlier value is proven.

## 7. v6 → v7 Migration Review

Accepted migration:

```text
v6 Task                -> v7 Workload
v6 ExecutionPlan       -> v7 CapitalAllocation + ExecutionPlan
v6 Run                 -> v7 Run
v6 PolicyDecision      -> v7 PolicyDecision + AuthorityEnvelope
v6 TelemetryRecord     -> v7 TelemetryRecord + Capital Ledger references
v6 QualityEvaluation   -> v7 QualityEvaluation
v6 Evidence            -> v7 Evidence with authority/allocation/recovery lineage
```

New v7 objects:

```text
Portfolio
Resource / ResourceState
BudgetEnvelope / BudgetLedgerEntry
CapitalAllocation
FailureRecord
RecoveryEpisode
OutcomeRecord
RedBlueScenario
AssuranceResult
```

The old `GATE-CORE-0` remains a truthful historical v6 acceptance record but no longer grants implementation authority.

## 8. Controller Consistency Review

### PASS — Core separation

The documents consistently preserve:

```text
Authority: what may happen?
Allocation: what deserves scarce capital?
Strategy: how should admitted capital be spent?
Execution: carry out and enforce.
Recovery: restore within authority and budget.
Evidence: what is reconstructable/provable?
Outcome: what value actually resulted?
```

No reviewed document intentionally collapses these roles into a generic router.

### PASS — Red-Blue / Recovery composition

Red-Blue targets allocator, policy, runtime, resources, context/memory, verifier, telemetry/outcome and recovery. Adaptive Recovery is bounded by authority, Recovery Budget, risk/irreversibility limits and post-recovery verification.

### PASS — Adapter boundary

MCP, A2A, OpenTelemetry, external gateways/routers, policy backends, identity, provenance, attestation, blockchain and ZK remain replaceable standards/adapters or later research rather than the v7 identity.

### PASS WITH IMPLEMENTATION QUESTIONS — R1 details

The following are intentionally unresolved implementation choices, not architecture blockers:

1. programming language / executable schema library;
2. exact quantity/unit types for every non-monetary budget dimension;
3. concurrency primitive / storage transaction model for hard-budget reservations;
4. exact shadow-price calibration and utility scale;
5. evaluator and outcome-attribution implementations;
6. concrete provider/MCP/A2A/identity/attestation adapters;
7. persistent storage and event transport choices.

R1 must resolve schema-level ambiguity before executable contracts pass `GATE-R1`.

## 9. Scope Firewall Confirmation

The gate explicitly does **not** authorize premature implementation of:

```text
learned / online allocator
production autonomous Red Team
inter-org markets / auctions
TEE-specific kernel coupling
blockchain dependency
ZK circuits
custom replacement for MCP / A2A / OTel
polished frontend
```

These remain in their assigned roadmap stages.

## 10. Decision

```text
Decision: ACCEPT
Decided by: Controller
Date: 2026-09-09
Architecture target: Rasputin v7.0
Next admitted stage: R1 — Executable Canonical Contracts
```

### Gate Result

`GATE-V7-R0 = ACCEPTED`

Rasputin may now move from strategic migration to R1 executable contract implementation. v7 contract semantics are frozen for R1; any discovered contradiction must return to Controller through the No-Drift Rule.

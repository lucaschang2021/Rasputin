# Rasputin v7 — GATE-V7-R0

> **Gate:** Strategic Constitution / Architecture / Contract Migration  
> **Status:** OPEN  
> **Purpose:** prevent implementation from freezing superseded v6 semantics.

## 1. Required Documents

The gate cannot pass unless the branch contains mutually consistent versions of:

- `README.md`;
- `docs/00-PROJECT-CONTROL.md`;
- `docs/01-MASTER-TECHNICAL-DESIGN.md`;
- `docs/02-DELIVERY-BOARD.md`;
- `docs/04-PROJECT-STATE.md`;
- `docs/ARCHITECTURE.md`;
- `docs/PRE_DEVELOPMENT.md`;
- `docs/contracts/EXECUTION_SCHEMA.md`;
- `docs/contracts/POLICY_CONTRACT.md`;
- `docs/contracts/EVIDENCE_CONTRACT.md`;
- `docs/contracts/CAPITAL_CONTRACT.md`;
- `docs/contracts/RESILIENCE_CONTRACT.md`.

## 2. Strategic Acceptance Criteria

All must be true:

- [ ] Rasputin is defined as a Sovereign Computational Capital Control Plane.
- [ ] Workload Portfolio sits above per-execution routing.
- [ ] Execution remains the atomic economic object.
- [ ] `DO_NOT_EXECUTE / DEFER / WAIT_FOR_INFORMATION` are first-class decisions.
- [ ] Resource Intelligence is broader than a model registry.
- [ ] Capital allocation is distinct from policy and strategy compilation.
- [ ] Outcome value is distinct from quality score.
- [ ] Multi-Agent is an execution strategy, not core identity.
- [ ] Gateway/RAG/orchestration/provenance/blockchain technologies are adapters or commodities by default.
- [ ] Red-Blue Assurance is a permanent cross-cutting loop.
- [ ] Adaptive Recovery follows Detect→Diagnose→Contain→Recover→Verify→Reallocate→Learn.
- [ ] Recovery is budgeted and can terminate economically.
- [ ] Risk, Irreversibility and Recovery Budgets are explicit.

## 3. Contract Acceptance Criteria

- [ ] Canonical Portfolio and Workload objects exist.
- [ ] Resource and ResourceState objects exist.
- [ ] BudgetEnvelope / BudgetLedger semantics exist.
- [ ] PolicyDecision / AuthorityEnvelope semantics exist.
- [ ] CapitalAllocation is distinct from ExecutionPlan.
- [ ] FailureRecord / RecoveryEpisode exist.
- [ ] OutcomeRecord supports delayed downstream outcomes.
- [ ] AssuranceResult supports bounded red-blue / chaos evidence.
- [ ] Evidence binds policy, authority, allocation, plan and recovery lineage.
- [ ] Unknown major versions fail explicitly.
- [ ] v6 Task/ExecutionPlan/Run migration mapping is documented.

## 4. Safety / Authority Acceptance Criteria

- [ ] Allocator cannot widen policy.
- [ ] Strategy compiler cannot widen policy.
- [ ] Fallback/recovery cannot widen policy.
- [ ] Hard budget exhaustion blocks further authorized spend.
- [ ] Cumulative irreversibility can block individually legal actions.
- [ ] Quarantined resources cannot be selected.
- [ ] Red-team tooling has explicit bounded test authority.
- [ ] Shadow mode cannot create irreversible production side effects.
- [ ] Failure history cannot be erased by successful recovery.

## 5. Economic Acceptance Criteria

- [ ] Nominal cost and effective/shadow cost are distinct.
- [ ] Shared budgets can apply at portfolio scope.
- [ ] Recovery cost is separately accountable.
- [ ] Opportunity cost/scarcity can affect allocation without changing nominal API price.
- [ ] ROCC is defined as a future benchmark metric, not claimed as validated before measurement.

## 6. Roadmap Acceptance Criteria

- [ ] R1–R16 are dependency ordered.
- [ ] Adaptive Recovery precedes autonomous online allocation.
- [ ] Red-Blue v0 has an explicit stage and gate.
- [ ] Learned allocation requires deterministic baseline and rollback.
- [ ] Inter-org markets, settlement and ZK remain R16 research until earlier value is proven.

## 7. Gate Evidence Package

Controller review should include:

```text
document diff
contract consistency review
v6→v7 migration matrix
open questions
known unresolved implementation choices
scope firewall confirmation
Controller ACCEPT / REJECT decision
```

No code benchmark is required for this architecture gate; R1 turns the accepted contracts into executable schemas.

## 8. Decision

```text
Decision: PENDING
Decided by: Controller
Date: TBD
Evidence refs: TBD
```

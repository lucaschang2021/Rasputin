# Rasputin — Project Control

> **Document class:** Controller / Source of Truth  
> **Version:** v7.1  
> **Status:** ACTIVE ALPHA / R1 EXECUTABLE CONTRACTS  
> **Control mode:** Federation-native · Portfolio-first · Contract-first · Backend-first · Gate-driven · Evidence-backed

## 1. Absolute Development Order

Every release train follows:

```text
Controller
   ↓
ARCHITECTURE / CONTRACT GATE
   ↓
BACKEND
   ↓  STAGE GATE
FRONTEND where admitted
   ↓
INTEGRATION + TEST + RED-BLUE + RECOVERY
   ↓  SYSTEM GATE
GITHUB / RELEASE
   ↓
MAIN ACCEPTED STATE
```

`GATE-V7-R0` is ACCEPTED. `GATE-V7.1-A0` is ACCEPTED as a backward-compatible architecture amendment. R1 executable contract implementation remains the active admitted stage.

## 2. Controller Authority

The Controller owns:

- strategic version boundary;
- portfolio / release scope;
- task IDs and dispatch;
- architecture decisions;
- contract freeze / unfreeze;
- budget and risk model admission;
- red-blue scope admission;
- recovery policy admission;
- stage-gate decisions;
- rollback decisions;
- final release acceptance.

Canonical rule:

> **Agents execute. Tests measure. Red teams challenge. Evidence proves. Recovery restores. Git records. Controller decides.**

## 3. Product Core

Rasputin is not a generic Agent framework, router, gateway, RAG system, provenance graph or blockchain product.

Core identity:

> **Rasputin = Compute Federation + Computational Capital Allocation + Execution Authority + Outcome Intelligence + Adversarial Assurance + Adaptive Recovery.**

The control hierarchy is:

```text
Principal
 -> Portfolio
 -> Workload
 -> Policy / Authority
 -> Capital Allocation
 -> Execution Strategy
 -> Execution
 -> Outcome / Failure / Evidence
 -> Learning / Recovery / Reallocation
```

## 4. Non-Negotiable Principles

### 4.1 Intelligence is capital

Money, compute, quota, time, verification, human attention, risk, irreversibility and recovery capacity are scarce resources.

### 4.2 Execution is the atomic economic object

Every material decision must remain reconstructable at execution level even when allocation occurs at portfolio level.

### 4.3 Portfolio before routing

`DO_NOT_EXECUTE`, `DEFER` and `WAIT_FOR_INFORMATION` are legitimate allocation decisions.

### 4.4 Authority before autonomy

No Agent, router, verifier or recovery mechanism may widen policy or economic authority.

### 4.5 Outcome before output

Optimization targets downstream task / workflow / business / research outcomes whenever measurable.

### 4.6 Recovery is budgeted

Retries and failovers consume capital. Recovery stops when expected remaining value no longer justifies expected recovery cost/risk or when authorized recovery capacity is exhausted.

### 4.7 Red-blue is continuous

Allocator, policy, runtime, MCP/A2A, memory, verifier, telemetry, outcome and recovery are all valid adversarial targets when their stage is active.

### 4.8 Federation preserves physical truth

Rasputin may expose heterogeneous compute as a logical pool, but it must never erase accelerator compatibility, topology, bandwidth, latency, locality, trust, reservation or failure-domain constraints.

Training-scale tightly coupled workloads and distributed inference/batch workloads may therefore receive materially different placement policies.

### 4.9 Standards by composition

External protocols and commodity infrastructure default to adapters. Rasputin concentrates proprietary depth on capital models, resource intelligence, allocation, authority semantics, outcome/failure intelligence, recovery and assurance.

## 5. Frozen v7.1 / R1 Compatibility Scope

`GATE-V7-R0` froze the strategic semantics below. `GATE-V7.1-A0` does not silently widen the current R1 implementation contract:

```text
Principal / Portfolio / Workload
Resource / ResourceState
BudgetEnvelope / BudgetLedger
PolicyDecision / AuthorityEnvelope
CapitalAllocation
ExecutionPlan / Run
Telemetry / Evidence
FailureRecord / RecoveryEpisode
QualityEvaluation / OutcomeRecord
RedBlueScenario / AssuranceResult
Learning / Reallocation boundaries
```

R1 implements these contracts; it does not redesign them silently.

v7.1 target federation objects — `ExecutionDomain`, `ComputePool`, `CapacitySlice`, `TopologyDescriptor`, `PlacementDecision`, `Reservation` — are architecture-level additions for later admitted stages. They are not automatically part of R1.

## 6. Acceptance Evidence

A gate may require:

- changed files / diff;
- executable schemas and golden fixtures;
- unit / contract / integration / security tests;
- failure injection and chaos tests;
- red-blue scenarios;
- recovery traces;
- capital benchmark results;
- adversarial / resilience benchmark results;
- type/lint/static checks;
- build outputs;
- performance data;
- known limitations;
- Controller ACCEPT / REJECT decision.

The required evidence set scales with stage; R1 is principally a schema/fixture/migration gate.

## 7. Quality Bar

Release-grade infrastructure should target:

- deterministic, versioned contracts;
- explicit authority boundaries;
- reproducible capital accounting;
- explainable allocation reason codes;
- failure-aware runtime behavior;
- bounded retries / recovery;
- append-only evidence;
- explicit resource health and quarantine state;
- provider/framework neutrality;
- safe default-deny behavior under unknown major versions;
- benchmarkable utility / cost / resilience;
- no hidden chain-of-thought dependency.

## 8. Scope Firewall

A capability may enter Rasputin Core only if it materially improves at least one of:

1. risk-adjusted outcome value;
2. capital allocation efficiency;
3. execution authority / safety;
4. resilience / recovery efficiency;
5. verifiability;
6. interoperability;
7. learning quality.

Otherwise classify it as Adapter / Commodity / Research / Backlog / Deferred.

## 9. Current Control State

```text
v5.0 historical vision                  FROZEN
v6.0-alpha migration baseline            PRESERVED / HISTORICAL
v7.0 strategic baseline                  PRESERVED / SUPERSEDED
v7.1 strategic target                    ACTIVE
GATE-V7-R0                               ACCEPTED
GATE-V7.1-A0                             ACCEPTED
R1 strategic contracts                   FROZEN / COMPATIBLE
Backend R1                               OPEN
Frontend                                 BLOCKED by backend surface gates
Integration / Assurance                  BLOCKED until relevant implementation exists
Release                                  STAGE-GATED
```

## 10. Current Objective

Execute R1 exactly as defined in `docs/10-BACKEND-WORK-PACKAGE.md`:

```text
Portfolio / Workload schemas
 -> Resource / ResourceState
 -> Capital / Budget
 -> Authority / Policy
 -> CapitalAllocation / ExecutionPlan / Run
 -> Telemetry / Failure / Recovery / Outcome
 -> Assurance contracts
 -> Evidence bindings
 -> Golden fixtures / v6 migration tests
 -> GATE-R1
```

Any contradiction discovered during R1 returns to Controller before code proceeds. No federation feature may be pulled into R1 merely because v7.1 defines its future semantics.

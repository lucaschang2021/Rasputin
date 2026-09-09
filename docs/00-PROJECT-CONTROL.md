# Rasputin — Project Control

> **Document class:** Controller / Source of Truth  
> **Version:** v7.0-strategic-migration  
> **Status:** R0 ARCHITECTURE / CONTRACT MIGRATION  
> **Control mode:** Portfolio-first · Contract-first · Backend-first · Gate-driven · Evidence-backed

## 1. Absolute Development Order

Every release train follows:

```text
Controller
   ↓
ARCHITECTURE / CONTRACT GATE
   ↓
BACKEND
   ↓  GATE-BE
FRONTEND
   ↓  GATE-FE
INTEGRATION + TEST + RED-BLUE + RECOVERY
   ↓  GATE-INT
GITHUB / RELEASE
   ↓  GATE-REL
MAIN ACCEPTED STATE
```

No implementation lane may silently freeze v6 semantics while v7 R0 migration is open.

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

> **Rasputin = Sovereign Computational Capital Allocation + Execution Authority + Outcome Intelligence + Adversarial Assurance + Adaptive Recovery.**

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

Retries and failovers consume capital. Recovery must stop when expected remaining value no longer justifies expected recovery cost or risk.

### 4.7 Red-blue is continuous

Allocator, policy, runtime, MCP/A2A, memory, verifier, telemetry, outcome and recovery must all be adversarially tested.

### 4.8 Standards by composition

External protocols and commodity infrastructure default to adapters. Rasputin concentrates proprietary depth on capital models, resource intelligence, allocation, authority semantics, outcome/failure intelligence, recovery and assurance.

## 5. v7 R0 Strategic Freeze Scope

R0 freezes the following canonical concepts before backend implementation resumes:

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
Learning / Reallocation Decision
```

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
v5.0 historical vision                 FROZEN
v6.0-alpha migration baseline           PRESERVED
v7.0 strategic target                   ACTIVE
v7 R0 architecture migration            OPEN
v7 contracts                             UNFROZEN / MIGRATING
Backend implementation                   PAUSED at semantic-freezing changes
Frontend                                 BLOCKED
Integration / Release                    BLOCKED
```

Backend work that is purely infrastructure-neutral may be prepared, but no code may hard-bind the system to superseded v6 contract semantics before `GATE-V7-R0`.

## 10. Current Objective

Complete v7 R0:

```text
Constitution
 -> Architecture
 -> Contracts
 -> Threat / Failure Model
 -> Capital / Budget Model
 -> Red-Blue / Recovery Semantics
 -> Delivery Board
 -> Migration Gate
```

Only then resume the implementation train.

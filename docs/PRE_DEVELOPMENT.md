# Rasputin v7 — Pre-Development Control Plan

> **Mode:** controller-first strategic migration  
> **Status:** COMPLETE / `GATE-V7-R0` ACCEPTED  
> **Next stage:** R1 Executable Canonical Contracts

## 1. Operating Model

```text
Discover
 -> Read v5/v6 baseline
 -> Migrate architecture
 -> Freeze contracts
 -> Controller review
 -> GATE-V7-R0 ACCEPT
 -> Dispatch R1
```

The strategic migration is complete. Implementation now follows `docs/10-BACKEND-WORK-PACKAGE.md`.

## 2. R0 Migration Results

### V7-R0-A — Strategic Constitution

Accepted:

- Sovereign Computational Capital Control Plane definition;
- v5/v6/v7 version boundary;
- moat vs adapter boundary;
- portfolio-first / authority-first principles;
- Red-Blue and Adaptive Recovery as permanent loops.

### V7-R0-B — Economic / Resource Model

Accepted semantics:

```text
Workload Portfolio
Computational Capital
Resource / ResourceState
Nominal Cost
Shadow Cost
Opportunity Cost
BudgetEnvelope / BudgetLedger
DO_NOT_EXECUTE / DEFER / WAIT_FOR_INFORMATION
```

### V7-R0-C — Authority / Risk Model

Accepted semantics:

```text
Principal / Tenant / Workload authority
Money / Compute / Quota / Latency budgets
Verification / Human Attention budgets
Risk Budget
Irreversibility Budget
Recovery Budget
HITL / approval artifacts
Runtime enforcement invariants
```

### V7-R0-D — Resilience / Adversarial Model

Accepted:

```text
Failure taxonomy
DETECT -> DIAGNOSE -> CONTAIN -> RECOVER -> VERIFY -> REALLOCATE -> LEARN
Red attack classes
Blue response classes
Shadow Mode
Controlled Chaos
RCB / RARB benchmark semantics
```

### V7-R0-E — Contract Migration

Accepted contract families:

```text
Portfolio / Workload
Resource / ResourceState
BudgetEnvelope / BudgetLedger
PolicyDecision / AuthorityEnvelope
CapitalAllocation
ExecutionPlan / Run
TelemetryRecord
EvidenceRecord
FailureRecord
RecoveryEpisode
QualityEvaluation
OutcomeRecord
RedBlueScenario / AssuranceResult
```

## 3. Gate Result

`GATE-V7-R0 = ACCEPTED` on 2026-09-09.

Controller review confirmed:

- policy/allocation/strategy/execution/recovery/evidence/outcome separation;
- v6→v7 migration mapping;
- explicit budget enforcement semantics;
- policy-safe recovery;
- bounded Red-Team authority;
- R1–R16 dependency order;
- historical v6 gate clearly superseded for implementation authority.

## 4. Backlog Classification

Every proposed capability remains classified as:

- **CORE NOW** — necessary for current gate;
- **CORE LATER** — strategic Rasputin logic with later stage;
- **ADAPTER** — external technology integrated behind contract;
- **COMMODITY** — required but not a moat;
- **RESEARCH** — theory/market validation required;
- **DEFER** — complexity not justified.

Current examples:

```text
Workload / Portfolio executable schemas  CORE NOW
Capital / Budget schema + primitives     CORE NOW
Resource Intelligence schemas           CORE NOW
Authority schemas                        CORE NOW
Failure / Recovery schemas              CORE NOW
Red-Blue assurance schemas              CORE NOW
OpenTelemetry                            ADAPTER
MCP / A2A                               ADAPTER / standard
OpenRouter / LiteLLM                    ADAPTER
OPA/Rego / Cedar                        ADAPTER
SPIFFE/SPIRE                            ADAPTER
Semantica / provenance graph            ADAPTER
Generic vector DB / RAG                 COMMODITY
Generic multi-agent framework           ADAPTER
Blockchain anchoring                    DEFER / ADAPTER
TEE attestation                         CORE LATER / ADAPTER
Zero-Knowledge Compliance               RESEARCH
Agent markets / auctions                RESEARCH
```

## 5. R1 Dispatch Queue

```text
R1-T1 Portfolio / Workload executable schemas
R1-T2 Resource / ResourceState schemas
R1-T3 BudgetEnvelope / BudgetLedger schemas
R1-T4 AuthorityEnvelope / PolicyDecision migration
R1-T5 CapitalAllocation / ExecutionPlan schemas
R1-T6 Telemetry / Failure / Recovery / Outcome schemas
R1-T7 Assurance schemas
R1-T8 Evidence bindings
R1-T9 Golden fixtures + v6 migration tests
```

Only after `GATE-R1` should R2 telemetry / capital-ledger implementation proceed.

## 6. Scope Firewall

1. New ideas enter backlog by default.
2. No feature may bypass the current gate.
3. External standards are preferred when they satisfy Rasputin contracts.
4. Optimization claims require benchmark evidence.
5. Trust claims require explicit evidence strength.
6. Recovery claims require failure injection evidence.
7. Safety claims require adversarial test evidence.
8. Multi-Agent complexity requires measured marginal utility.
9. R16 research cannot become an R1-R15 dependency without Controller approval.

## 7. Definition of Pre-Development Complete

All conditions are satisfied:

- [x] v7 architecture internally consistent;
- [x] canonical strategic contracts frozen for R1;
- [x] v6 migration documented;
- [x] threat / failure model defined;
- [x] budget / capital semantics defined;
- [x] Red-Blue and recovery semantics defined;
- [x] first implementation tasks require no top-level strategic invention;
- [x] `GATE-V7-R0` accepted.

Rasputin is now in **ACTIVE ALPHA / R1 EXECUTABLE CONTRACTS**.

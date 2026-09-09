# Rasputin v7 — Pre-Development Control Plan

> Mode: controller-first strategic migration  
> Rule: no semantic implementation before v7 R0 contracts are accepted.

## 1. Operating Model

```text
Discover
 -> Read v5/v6 baseline
 -> Migrate architecture
 -> Freeze contracts
 -> Dispatch
 -> Execute
 -> Observe
 -> Red-team / recover
 -> Accept
 -> Archive
```

Roles remain conceptually separated even if one developer/agent performs several roles.

## 2. R0 Migration Board

### V7-R0-A — Strategic Constitution

Freeze:

- Sovereign Computational Capital Control Plane definition;
- v5/v6/v7 version boundary;
- moat vs adapter boundary;
- portfolio-first / authority-first principles;
- red-blue and adaptive recovery as permanent loops.

### V7-R0-B — Economic / Resource Model

Define:

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

Define:

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

Define:

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

Required contracts:

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

### GATE-V7-R0

Required:

- all canonical concepts have versioning rules;
- v6 migration mapping exists;
- no unresolved conflict between policy, allocation, recovery and evidence;
- every budget has enforcement semantics;
- recovery cannot bypass policy;
- red-team tooling is contained by test authority;
- R1-R16 gates are measurable;
- Controller records ACCEPT / REJECT.

## 3. Backlog Classification

Every proposed capability is classified as:

- **CORE NOW** — necessary for current gate;
- **CORE LATER** — strategic Rasputin logic with later stage;
- **ADAPTER** — external technology integrated behind contract;
- **COMMODITY** — required but not a moat;
- **RESEARCH** — theory/market validation required;
- **DEFER** — complexity not justified.

Current examples:

```text
Workload / Portfolio contracts        CORE NOW
Capital / Budget ledger              CORE NOW
Resource Intelligence                CORE NOW
Authority semantics                  CORE NOW
Adaptive Recovery contract           CORE NOW
Red-Blue contract                    CORE NOW
OpenTelemetry                        ADAPTER
MCP / A2A                            ADAPTER / standard
OpenRouter / LiteLLM                 ADAPTER
OPA/Rego / Cedar                     ADAPTER
SPIFFE/SPIRE                         ADAPTER
Semantica / provenance graph         ADAPTER
Generic vector DB / RAG              COMMODITY
Generic multi-agent framework        ADAPTER
Blockchain anchoring                 DEFER / ADAPTER
TEE attestation                      CORE LATER / ADAPTER
Zero-Knowledge Compliance            RESEARCH
Agent markets / auctions             RESEARCH
```

## 4. First Implementation Queue After GATE-V7-R0

```text
R1-T1 Portfolio / Workload executable schemas
R1-T2 Resource / ResourceState schemas
R1-T3 BudgetEnvelope / BudgetLedger schemas
R1-T4 AuthorityEnvelope / PolicyDecision migration
R1-T5 CapitalAllocation / ExecutionPlan schemas
R1-T6 Failure / Recovery / Outcome schemas
R1-T7 golden fixtures + migration tests
```

Only after R1 acceptance should R2 telemetry / capital ledger implementation proceed.

## 5. Scope Firewall

1. New ideas enter backlog by default.
2. No feature may bypass the current gate.
3. External standards are preferred when they satisfy Rasputin contracts.
4. Optimization claims require benchmark evidence.
5. Trust claims require explicit evidence strength.
6. Recovery claims require failure injection evidence.
7. Safety claims require adversarial test evidence.
8. Multi-agent complexity requires measured marginal utility.
9. R16 research cannot become an R1-R15 dependency without Controller approval.

## 6. Definition of v7 Pre-Development Complete

Pre-development is complete when:

- v7 architecture is internally consistent;
- canonical contracts are frozen for R1;
- v6 migration is documented;
- threat / failure model exists;
- budget / capital semantics exist;
- red-blue and recovery semantics exist;
- first implementation tasks require no strategic invention inside coding prompts;
- `GATE-V7-R0` is accepted.

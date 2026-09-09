# Rasputin v7 — Backend Work Package R1

> **Owner:** Backend  
> **Entry:** BLOCKED until `GATE-V7-R0`  
> **Sequence:** R1 contracts → R2 ledger/telemetry → R3 resources → R4 authority ...  
> **Rule:** No v6 semantic lock-in before v7 R0 acceptance.

## R1 Objective

Turn the accepted v7 Markdown contracts into executable, versioned, tested schemas for portfolio-level computational capital control.

## R1 Required Modules

```text
contracts/
portfolio/
resources/
capital/
authority/
runtime_types/
outcome/
failure/
recovery/
assurance/
```

Implementation may map these to language/framework-specific package names, but semantic boundaries must remain recognizable.

## R1 Tasks

### R1-T1 — Portfolio / Workload

Implement:

- Portfolio;
- Workload;
- admission state;
- dependencies / deadlines;
- expected value / uncertainty references;
- valid defer / do-not-execute states.

### R1-T2 — Resource / ResourceState

Implement:

- heterogeneous Resource types;
- dynamic ResourceState;
- availability / degraded / unavailable / quarantined states;
- nominal price and shadow-price fields;
- quota / health / latency representation.

### R1-T3 — Capital / Budget

Implement:

- BudgetEnvelope;
- BudgetLedgerEntry;
- reserve / consume / release / settle semantics;
- money / compute / quota / latency / verification / human / risk / irreversibility / recovery dimensions;
- concurrency-safe hard-budget primitives or explicit abstraction for them.

### R1-T4 — Authority / Policy

Implement:

- PolicyDecision;
- AuthorityEnvelope;
- explicit allowed/denied resources/capabilities;
- hard budget limits;
- human approval artifacts;
- recovery authority bounds.

### R1-T5 — CapitalAllocation / ExecutionPlan / Run

Implement:

- execute / defer / do-not-execute / wait-for-information decisions;
- allocator identity/version;
- resource-state references;
- strategy representation;
- recovery policy reference;
- run lifecycle including recovering/quarantined states.

### R1-T6 — Telemetry / Failure / Recovery / Outcome

Implement:

- TelemetryRecord;
- FailureRecord;
- RecoveryEpisode;
- QualityEvaluation;
- delayed OutcomeRecord attachment.

### R1-T7 — Assurance Contracts

Implement:

- RedBlueScenario;
- AssuranceResult;
- Shadow / Controlled Chaos mode flags;
- explicit test authority reference;
- forbidden-effect representation.

### R1-T8 — Evidence References

Update executable evidence envelope to bind:

- policy / authority;
- allocation;
- execution plan;
- ledger;
- failure / recovery;
- outcome;
- assurance.

### R1-T9 — Golden Fixtures / Migration

Fixtures must include:

1. two competing workloads under one portfolio budget;
2. execute vs defer decision;
3. do-not-execute due to negative expected utility;
4. quota scarcity changing resource shadow price;
5. denied resource;
6. cumulative irreversibility exhaustion;
7. failed run with bounded recovery;
8. quarantined provider and alternate allocation;
9. delayed outcome attachment;
10. red-blue shadow scenario with no production side effect.

## R1 Gate

`GATE-R1` requires:

- schema validation passes;
- round-trip serialization passes;
- canonical hash fixtures stable where required;
- unknown major versions fail explicitly;
- v6→v7 migration fixtures pass for retained objects;
- no hard budget can be represented ambiguously;
- recovery cannot represent privilege widening;
- assurance test authority is explicit;
- all golden fixtures pass.

## Architecture Constraints

Do not implement during R1:

- learned allocator;
- contextual bandit;
- production OpenRouter/LiteLLM integration;
- production MCP/A2A execution;
- autonomous red team;
- TEE / remote attestation;
- blockchain anchoring;
- ZK circuits;
- inter-org markets;
- polished frontend.

R1 is contract execution, not feature spectacle.

## Backend Return Template

```text
Package ID
Summary
Changed files
Contract / migration impact
Commands executed
Tests / fixtures
Failure cases
Security / authority observations
Performance observations
Known limitations
Unresolved questions
Recommended gate decision
```

The Controller records ACCEPT / REJECT.

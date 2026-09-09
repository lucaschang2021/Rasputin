# Rasputin v7.0 — Technical Architecture

> **Status:** R0 STRATEGIC MIGRATION / PRE-IMPLEMENTATION  
> **Architecture mode:** portfolio-first · authority-first · stage-gated · evidence-backed · adversarially tested  
> **Purpose:** freeze v7 architectural boundaries before implementation.

## 1. System Objective

Rasputin is a **Sovereign Computational Capital Control Plane**.

It allocates scarce AI resources across competing workloads, governs the resulting executions, measures real outcomes, survives failure, and learns how to reallocate capital safely.

The portfolio-level objective is conceptually:

```text
maximize Risk-Adjusted Outcome Value
subject to:
  Monetary Cost <= Budget
  Compute / Quota <= Capacity
  Quality >= Required Floor
  Risk <= Risk Budget
  Irreversibility <= Irreversibility Budget
  Verification <= Verification Capacity
  Human Attention <= Human Budget
  Recovery Spend <= Recovery Budget
  Privacy / Authority / SLA constraints satisfied
```

A workload strategy may allocate:

```text
pi = (
  Model,
  Agent Topology,
  Harness,
  Tools,
  Memory,
  Test-Time Compute,
  Runtime,
  Verification,
  Recovery Policy
)
```

`NULL / DO_NOT_EXECUTE / DEFER / WAIT_FOR_INFORMATION` are first-class allocation outcomes.

---

## 2. Canonical Object Hierarchy

```text
Principal / Organization
  -> Portfolio
      -> Workload[*]
          -> PolicyDecision
          -> CapitalAllocation
          -> ExecutionPlan
          -> Run[*]
              -> TelemetryRecord[*]
              -> FailureRecord[*]
              -> RecoveryEpisode[*]
              -> EvidenceRecord[*]
              -> QualityEvaluation[*]
              -> OutcomeRecord[*]
  -> BudgetLedger[*]
  -> ResourceState[*]
  -> Learning / Reallocation Decision[*]
```

**Execution remains the atomic economic object.** Portfolio and CapitalAllocation provide the higher-level coordination layer.

---

## 3. Eight Core Planes

### 3.1 Workload & Portfolio Plane

Responsibilities:

- accept canonical workload objectives rather than provider-specific prompts;
- group workloads into portfolios;
- record expected value, uncertainty, priority, deadlines and dependencies;
- define quality, privacy, risk and irreversibility requirements;
- expose defer / cancel / do-not-execute as valid decisions;
- preserve principal / tenant / project ownership boundaries.

A workload expresses **what outcome is wanted**, not how to implement it.

### 3.2 Authority & Policy Plane

This plane is authoritative for what may happen.

Inputs may include:

```text
Principal / Tenant Policy
Workload Constraints
Identity / Authority Context
Data Classification
Runtime / Resource State
Budget State
Risk / Irreversibility State
Human Approval State
```

Outputs:

```text
Allowed Execution Space
Hard Constraints
Required Controls
Approval Requirements
Budget Envelopes
Reason Codes
```

Hard constraints dominate optimization preferences. Router / allocator / recovery logic may never widen authority.

### 3.3 Resource Intelligence Plane

Rasputin treats every usable production factor as a resource, including:

```text
Model
Agent / A2A Agent
Harness / Runtime
MCP Tool
Retriever / Memory
Verifier
Human Reviewer
GPU / Compute Runtime
API Quota
Sandbox
Attested Environment
External Router / Gateway
```

Each resource may expose:

```text
identity
capabilities
nominal price
shadow price
availability
quota
latency
reliability
health
task affinity
historical outcome
privacy class
risk class
verification support
attestation state
```

The Resource Intelligence Plane is broader than a model registry.

### 3.4 Computational Capital Allocator

This is the primary v7 differentiator.

It determines:

1. which workloads deserve capital now;
2. how much capital each receives;
3. which resources / strategy classes are admissible;
4. when further information gathering is worth its cost;
5. when capital should be reserved for higher-value future work;
6. when a workload should not execute.

Algorithm ladder:

```text
v0 deterministic allocation / explicit scoring
 -> Lagrangian and shadow-price allocation
 -> contextual bandits / constrained bandits
 -> bandits-with-knapsacks style budgeted learning
 -> offline policy evaluation / policy learning
 -> constrained sequential control / robust optimization
```

No learned allocator ships without deterministic baseline, offline evaluation, rollback and policy-safe bounds.

### 3.5 Execution Strategy Compiler

Converts a CapitalAllocation into a concrete ExecutionPlan.

Candidate dimensions:

```text
model/provider
external router vs direct provider vs local
agent topology
harness
MCP/A2A resources
tool set
memory / retrieval strategy
reasoning effort / sampling / search depth
verification intensity
runtime / sandbox
recovery policy
```

Multi-Agent is an execution strategy, not the product identity.

### 3.6 Sovereign Execution Control Plane

Owns runtime lifecycle:

```text
prepare
 -> authorize
 -> reserve capital
 -> execute
 -> observe
 -> limit / suspend / revoke
 -> recover / reroute / abort
 -> verify
 -> finalize
 -> settle ledgers
```

Required properties:

- cancellation and termination;
- timeout / retry / recovery ceilings;
- capability and tool enforcement;
- idempotency where applicable;
- circuit breakers;
- resource quarantine;
- sandbox / egress boundaries;
- parent/child run lineage;
- policy-safe fallback;
- runtime event emission.

### 3.7 Outcome, Telemetry, Evidence & Failure Intelligence Plane

Rasputin must separate four classes of truth:

**Telemetry** — what the runtime measured.  
**Evidence** — what claims can be reconstructed and integrity-checked.  
**Outcome** — what happened downstream.  
**Failure Intelligence** — what failed, why, under which resource state, and what recovery worked.

Canonical analytical record:

```text
(Workload,
 Context,
 ResourceState,
 Strategy,
 NominalCost,
 ShadowCost,
 RiskConsumed,
 IrreversibilityConsumed,
 Attack,
 Failure,
 Recovery,
 Quality,
 Outcome,
 EconomicValue,
 Evidence)
```

Raw tracing should prefer OpenTelemetry-compatible semantics where practical. Rasputin adds the economic and authority layer rather than reinventing span transport.

### 3.8 Learning & Reallocation Engine

Learning pipeline:

```text
Outcome
 -> delayed reward / credit assignment
 -> failure & recovery attribution
 -> counterfactual / offline evaluation
 -> candidate policy or pricing update
 -> shadow / safe deployment
 -> online exploration within bounds
 -> capital reallocation
```

A model-generated self-reflection message is never sufficient evidence for changing production allocation policy.

---

## 4. Cross-Cutting Loop A — Red-Blue Adversarial Assurance

Red-Blue is a permanent assurance loop across all planes.

### Red targets

```text
value manipulation
urgency manipulation
scarcity / price manipulation
allocator gaming
policy bypass
prompt / tool injection
poisoned context or memory
resource impersonation
verifier manipulation
telemetry falsification
outcome falsification
quota / latency shocks
provider compromise / outage
recovery abuse
cross-agent authority confusion
```

### Blue controls

```text
policy tightening
privilege reduction
resource quarantine
sandbox / egress escalation
secondary verification
human approval
memory rollback
resource substitution
budget reduction
rate limiting
execution cancellation
credential / authority revocation
```

### Assurance invariant

The target is not merely model safety; it is **Computational Capital Integrity**: an adversary must not be able to obtain disproportionate capital, authority or irreversible effect by manipulating value, state or evidence signals.

Red-team intensity itself consumes capital and must be policy- and value-aware.

---

## 5. Cross-Cutting Loop B — Adaptive Recovery & Self-Healing

Permanent recovery protocol:

```text
DETECT
 -> DIAGNOSE
 -> CONTAIN
 -> RECOVER
 -> VERIFY
 -> REALLOCATE
 -> LEARN
```

Failure classes include:

- provider / model degradation;
- tool or runtime failure;
- policy violation;
- verifier disagreement;
- poisoned or corrupted context / memory;
- quota exhaustion;
- latency degradation;
- security incident;
- quality failure;
- business-outcome failure.

Possible recovery actions:

```text
retry
reroute
alternate model/tool/harness
rollback
restore memory
reduce privileges
degrade gracefully
escalate verification
human escalation
quarantine
abort
```

Recovery is budgeted. Conceptual stop rule:

```text
if Expected Remaining Outcome Value < Expected Recovery Cost:
    abort / defer / escalate
```

Provider-wide failures must be able to trigger **portfolio-level reallocation**, not merely per-request fallback.

---

## 6. Capital Ledger and Shadow Pricing

Rasputin distinguishes nominal price from effective computational cost.

Conceptually:

```text
EffectiveCost =
    Money
  + QuotaScarcity
  + LatencyScarcity
  + RiskCost
  + VerificationCost
  + HumanAttentionCost
  + OpportunityCost
  + RecoveryReserveCost
```

Budget dimensions may include:

```text
money
compute
tokens / quota
latency
verification
human attention
risk
irreversibility
recovery
```

Budget ledgers may exist at principal, tenant, portfolio, workload, execution or resource scope.

---

## 7. Outcome Intelligence

Quality score is not the final optimization target.

Rasputin models:

```text
Execution Output
 -> Technical Success
 -> Task Success
 -> Workflow Outcome
 -> Business / Research Outcome
 -> Economic / Strategic Value
```

A future core metric is:

```text
ROCC = Risk-Adjusted Outcome Value / Effective Computational Capital
```

The system must preserve delayed outcomes and allow later outcome records to attach to finalized runs and portfolios.

---

## 8. Verification, Evidence and Trust

Verification is itself an allocatable resource:

```text
deterministic checks
schema validation
reference / domain rules
model judge / cross-model judge
human review
runtime attestation
cryptographic proof
business outcome
```

Evidence path:

```text
Canonical Record
 -> Content Commitment
 -> Hash Chain
 -> Merkle Batch
 -> Optional Signature / Transparency Layer
 -> Optional Runtime / Hardware Attestation
 -> Optional External Anchor
 -> Future Zero-Knowledge Compliance
```

Rasputin does not claim to prove hidden chain-of-thought. ZK work is limited to compliance predicates over stable execution commitments.

---

## 9. Standards and Adapter Boundary

Permanent law:

```text
Frontier Theory -> Core
Frontier Technology -> Adapter / Standard by default
```

Rasputin may integrate:

- MCP for tools/data;
- A2A for agent interoperability;
- OpenTelemetry for raw traces/metrics;
- OPA/Rego or Cedar-compatible policy backends;
- SPIFFE/SPIRE-style workload identity;
- OpenRouter, LiteLLM, direct provider APIs and local runtimes as execution venues;
- LangGraph or other orchestration runtimes;
- context/provenance systems such as Semantica as adapters;
- Sigstore/in-toto/transparency/TEE/attestation systems as trust adapters.

None of these external systems define Rasputin's moat.

---

## 10. Security Invariants

1. No component may widen a PolicyDecision.
2. Every material capital allocation is attributable to policy, resource state and allocator version.
3. Denied workloads never reach runtime.
4. Recovery actions remain inside the same or stricter authority envelope unless a new explicit approval is produced.
5. Risk, irreversibility and recovery budgets fail closed when exhausted.
6. Resource state changes can invalidate queued plans.
7. Sensitive payloads are referenced / committed where possible rather than copied into evidence.
8. Evidence must distinguish declared plan from observed execution.
9. No automatic policy update bypasses offline evaluation, rollback or Controller gate.
10. Red-team tooling never gains broader production authority merely because it is a testing component.
11. Unknown schema / policy major versions fail explicitly.
12. Human approval is a first-class artifact, not an informal message.

---

## 11. Repository Target

```text
rasputin/
  core/
    contracts/
    portfolio/
    authority/
    resources/
    capital/
    strategy/
    runtime/
    telemetry/
    outcome/
    failure/
    recovery/
    evidence/
    evaluation/
    learning/
    assurance/
  adapters/
    models/
    routing_venues/
    mcp/
    a2a/
    policy/
    identity/
    storage/
    observability/
    attestation/
    anchoring/
  benchmarks/
    capital/
    adversarial/
    resilience/
  api/
  cli/
  frontend/
  tests/
    unit/
    contract/
    integration/
    e2e/
    performance/
    security/
    chaos/
  fixtures/
  docs/
  scripts/
  infra/
```

---

## 12. Benchmarks

### RCB — Rasputin Capital Benchmark

Measures success, verified success, effective cost, latency/SLA, policy violations, risk/irreversibility consumption, human intervention, portfolio utility, Utility/$, Utility/token, Utility/compute and ROCC.

### RARB — Rasputin Adversarial & Resilience Benchmark

Measures attack detection, bypass rate, unauthorized action rate, MTTD, MTTR, recovery success, recovery cost, blast radius, portfolio utility under attack/failure, quarantine success, rollback integrity and capital reallocation efficiency.

Optimization claims without benchmark evidence are not release claims.

---

## 13. Version Boundary

- **v5.0** — historical full-domain vision; frozen.
- **v6.0-alpha** — execution-economics migration baseline; preserved for migration history.
- **v7.0** — active strategic and technical target.

Current implementation priority is **R0 contract migration and architecture acceptance**. Existing v6 concepts that remain valid should be migrated, not blindly discarded.

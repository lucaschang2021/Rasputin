# Rasputin v7.1 — Master Technical Design

> **Purpose:** Define the active v7.1 target system while preserving the accepted R1 contract baseline.  
> **Mode:** federation-native · portfolio-first · controller-first · backend-first · stage-gated.

## 1. System Mission

Rasputin is a sovereign control plane and operating system for economically efficient, federated, governed, verifiable and resilient computational capital.

For every portfolio and workload it must answer:

1. **Is this workload worth executing now?**
2. **How much computational capital should it receive?**
3. **Which execution domain, resources and strategy should spend that capital?**
4. **How should heterogeneous capacity be pooled and placed without violating topology, locality or trust constraints?**
5. **Under whose authority and policy may execution occur?**
6. **What actually happened, failed or recovered?**
7. **What real outcome and economic value resulted?**
8. **How should the next allocation and placement change?**

## 2. Capital Brain

```text
WORKLOAD PORTFOLIO
        |
        v
+---------------------------------------------+
| VALUE INTELLIGENCE                          |
| expected outcome / uncertainty / VoI        |
+---------------------------------------------+
| RESOURCE INTELLIGENCE                       |
| capability / health / price / scarcity      |
+---------------------------------------------+
| COMPUTE FEDERATION / PLACEMENT              |
| domains / topology / locality / reservation |
+---------------------------------------------+
| CAPITAL PRICING                             |
| nominal / shadow / opportunity / risk cost  |
+---------------------------------------------+
| ALLOCATION                                  |
| rules / Lagrangian / bandits / scheduling   |
+---------------------------------------------+
| AUTHORITY                                   |
| policy / risk / irreversibility / approval  |
+---------------------------------------------+
| LEARNING                                    |
| attribution / OPE / online safe adaptation  |
+---------------------------------------------+
        |
        v
EXECUTION STRATEGY COMPILER
```

The Capital Brain is the primary proprietary center of gravity.

## 3. Workload / Portfolio Model

Each Workload contains objective-level semantics:

```text
workload_id
portfolio_id
principal_ref
objective
input_refs
expected_value / value_model_ref
uncertainty
priority
deadline
dependencies
capability_requirements
quality_floor
privacy_class
risk_class
irreversibility_class
budget_envelope
metadata
```

A Portfolio groups workloads that compete for shared scarce resources.

## 4. Resource Intelligence

A canonical Resource may represent a model, harness, tool, memory system, verifier, human reviewer, runtime, GPU, quota pool, sandbox or external router.

Canonical dynamic ResourceState should include:

```text
availability
health
nominal_price
quota_remaining
latency estimate
failure rate
historical success by workload class
privacy / locality
risk class
verification support
attestation state
shadow_price components
```

Resource state is time-dependent and may invalidate queued plans.

## 5. Compute Federation & Resource Fabric

### 5.1 Purpose

Expose physically separate compute domains as one **logical resource fabric** for discovery, accounting and placement, while preserving the constraints that make those domains non-interchangeable.

```text
Physical Capacity
  -> Discovery
  -> Normalized Resource / Domain State
  -> Logical ComputePool
  -> Placement Candidates
  -> Reservation
  -> Authorized Execution
```

### 5.2 Canonical objects

```text
ExecutionDomain
ComputePool
CapacitySlice
TopologyDescriptor
InterconnectClass
PlacementConstraint
PlacementDecision
Reservation
FailureDomain
```

These are v7.1 target objects. They do not expand the already admitted R1 contract gate unless separately dispatched.

### 5.3 Physical truth invariant

A logical pool MUST NOT erase:

```text
accelerator compatibility
VRAM / HBM capacity
memory bandwidth
NVLink / fabric topology
east-west network bandwidth
WAN latency
data locality / region
scheduler / runtime capability
trust / attestation
failure domain
reservation / quota state
```

### 5.4 Workload coordination class

Placement should distinguish at least:

```text
tightly_coupled_training
distributed_inference
batch
evaluation
agentic_workflow
latency_sensitive
stateful
embarrassingly_parallel
```

Tightly coupled training normally requires a single high-bandwidth execution domain. Independent inference or batch workloads may be spread across domains.

### 5.5 Federation responsibilities

- capability discovery;
- heterogeneous inventory normalization;
- logical pool construction;
- reservation / release;
- topology-aware and locality-aware placement;
- fragmentation-aware capacity accounting;
- failover eligibility;
- provider / region / cluster isolation;
- placement reason codes;
- telemetry for effective utilization.

Kubernetes, Slurm, cloud schedulers and accelerator-specific runtimes remain adapters or execution substrates unless a proven semantic gap requires native logic.

## 6. Computational Capital Allocator

### 6.1 Objective

The allocator chooses workload admission, budget allocation and strategy class under multiple shared constraints.

### 6.2 Algorithm progression

**A0 — deterministic:** explicit rules, weighted utility, hard budgets.  
**A1 — dual / shadow pricing:** Lagrangian relaxation and scarcity prices.  
**A2 — offline value models:** historical strategy-outcome prediction.  
**A3 — constrained contextual bandits:** bounded online exploration.  
**A4 — portfolio / sequential control:** scheduling, delayed rewards and non-stationarity.  
**A5 — research:** robust/CVaR control, market-assisted allocation, inter-org settlement.

Every learned stage requires a reproducible deterministic baseline and rollback path.

### 6.3 Value of Information

The allocator may spend capital to improve its own decision only when expected information value exceeds decision cost.

Possible actions:

```text
classify cheaply
buy deeper evaluator
run pilot execution
sample alternate model
request human estimate
execute directly
defer
```

## 7. Strategy Compiler

Produces an ExecutionPlan from an admitted allocation.

```text
Model / Provider / Venue
Execution Domain / Compute Pool / Placement
Harness
Agent topology
Tools / MCP
Memory / Retrieval
Test-time compute
Runtime / Sandbox
Verification intensity
Fallback / Recovery policy
```

The compiler cannot select resources outside the AuthorityEnvelope or allocation limits.

## 8. Sovereign Execution Control

Lifecycle:

```text
prepare
 -> validate current resource state
 -> authorize
 -> reserve ledgers / capacity
 -> place
 -> dispatch
 -> observe
 -> control
 -> recover / abort
 -> verify
 -> finalize
 -> release / settle reservations
```

Must support:

- timeouts and cancellation;
- runtime permission checks;
- tool-level scopes;
- resource quarantine;
- provider circuit breakers;
- policy-safe fallback;
- parent/child run lineage;
- structured events;
- idempotency where applicable;
- human approval artifacts;
- graceful degradation.

## 9. Budget and Ledger System

Budget dimensions:

```text
money
compute
token / quota
latency
verification
human attention
risk
irreversibility
recovery
```

Ledger operations should support:

```text
reserve
consume
release
adjust
expire
settle
```

Every material consumption must reference a workload/run and allocation decision.

## 10. Adaptive Recovery Engine

Recovery protocol:

```text
DETECT -> DIAGNOSE -> CONTAIN -> RECOVER -> VERIFY -> REALLOCATE -> LEARN
```

### 10.1 Failure taxonomy

```text
provider_unavailable
model_degraded
tool_failure
runtime_failure
policy_violation
quality_failure
verifier_disagreement
memory_corruption
context_poisoning
quota_exhaustion
latency_degradation
security_incident
outcome_failure
unknown
```

### 10.2 Containment

```text
freeze run
revoke capability
quarantine resource
reduce privilege
block egress
stop child runs
```

### 10.3 Recovery actions

```text
retry
reroute
alternate model / tool / harness
restore checkpoint / memory
rollback state
degrade quality target within policy
escalate verification
human escalation
abort / defer
```

### 10.4 Economic stop rule

Recovery continues only while expected remaining risk-adjusted value justifies expected recovery cost and additional irreversible risk.

Provider-wide or tool-fleet incidents may trigger portfolio reallocation and shadow-price updates.

## 11. Red-Blue Adversarial Assurance Engine

### 11.1 Red targets

- allocator manipulation;
- fake value / urgency / scarcity;
- policy bypass;
- prompt/tool injection;
- poisoned memory/context;
- resource identity spoofing;
- verifier gaming;
- telemetry or outcome manipulation;
- quota / latency / provider shocks;
- recovery abuse;
- cross-agent authority confusion.

### 11.2 Blue responses

- deny / require approval;
- tighten policy;
- reduce privileges / budgets;
- isolate or quarantine resource;
- sanitize context;
- add verification;
- substitute resource;
- rollback memory/state;
- revoke authority;
- terminate execution.

### 11.3 Shadow and Chaos modes

**Shadow Mode:** compare candidate strategies / defenses without producing external side effects.  
**Controlled Chaos:** inject bounded failures such as provider outage, timeout, malformed tool response, quota exhaustion, verifier failure or stale resource state.

Red-team execution must itself obey policy and test-environment boundaries.

## 12. Outcome & Failure Intelligence

Outcome is appendable after run finalization because business/research value may arrive later.

```text
OutcomeRecord:
  technical_success
  task_success
  workflow_outcome
  downstream_event_refs
  realized_value
  currency / value_unit
  risk_adjustment
  attribution_confidence
```

Failure Intelligence records failure class, suspected cause, resource state, blast radius, attempted recoveries, recovery cost and final result.

## 13. Telemetry and Observability

Prefer OpenTelemetry-compatible trace/metric/event semantics for raw execution observability.

Rasputin-specific economic dimensions include:

```text
nominal_cost
shadow_cost
scarcity_cost
capacity_fragmentation_cost
network_locality_cost
opportunity_cost
risk_consumed
irreversibility_consumed
recovery_cost
expected_value
realized_value
marginal_utility
allocation_reason
```

## 14. Evidence and Verification

Evidence is separate from telemetry and quality.

```text
Canonical Record
 -> deterministic serialization
 -> content hash
 -> parent-linked hash chain
 -> Merkle batch
 -> optional signatures / transparency
 -> optional runtime attestation
 -> optional external anchor
 -> future ZK compliance
```

Verification intensity is a capital allocation variable. Hidden chain-of-thought is neither required nor claimed.

## 15. Standards / Adapter Strategy

Rasputin should integrate rather than reimplement where appropriate:

```text
MCP                tool/data protocol
A2A                agent protocol
OpenTelemetry      observability transport
OPA/Rego / Cedar   policy backends
SPIFFE/SPIRE       workload identity
OpenRouter/LiteLLM execution venues / gateway adapters
LangGraph etc.     orchestration adapters
Semantica etc.     context/provenance adapters
TEE/attestation    trust adapters
```

Core semantics remain vendor-neutral.

## 16. Research / Product Metrics

### ROCC

```text
Return on Computational Capital =
Risk-Adjusted Outcome Value / Effective Computational Capital
```

### RCB

Capital allocation benchmark: portfolio utility, verified success, effective cost, SLA, budget/risk consumption and ROCC.

### RARB

Adversarial / resilience benchmark: bypass, unauthorized action, MTTD, MTTR, recovery success/cost, blast radius and portfolio utility under failure/attack.

## 17. Repository Target

```text
core/
  contracts/
  portfolio/
  authority/
  resources/
  federation/
  placement/
  capital/
  strategy/
  runtime/
  telemetry/
  outcome/
  failure/
  recovery/
  evidence/
  learning/
  assurance/
adapters/
benchmarks/
api/
cli/
frontend/
tests/
fixtures/
docs/
```

## 18. Implementation Law

```text
stable contracts
before federation automation
before allocation intelligence
before autonomous learning
before market mechanisms
before ZK / inter-org ambition
```

No feature enters the kernel merely because it is technically impressive. It must improve risk-adjusted outcome value, allocation efficiency, authority, resilience, verifiability, interoperability or learning quality.

# Rasputin v7.1 — Compute Federation Architecture Amendment

> **Gate:** `GATE-V7.1-A0`  
> **Decision:** ACCEPTED  
> **Date:** 2026-09-18  
> **Compatibility:** Backward-compatible with the accepted v7.0 / R1 contract baseline  
> **Implementation effect:** No automatic expansion of R1 scope

## 1. Decision

Rasputin v7.1 extends the v7.0 Sovereign Computational Capital Control Plane with a first-class **Compute Federation & Resource Fabric** boundary.

The product positioning is now:

> **Rasputin is the Operating System for Computational Capital.**

It turns heterogeneous compute into a governable logical capital pool, decides which workloads deserve capacity, places admitted work into appropriate execution domains, and preserves authority, economics, evidence, resilience and learning across that lifecycle.

## 2. What changed

v7.1 adds these target concepts:

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
CoordinationClass
```

The system may federate:

```text
cloud accelerators
private clusters
on-prem infrastructure
reserved capacity
CPU / GPU / NPU / ASIC capacity
specialized execution domains
```

through adapters and normalized resource intelligence.

## 3. Non-goal: fake hardware fusion

Compute Federation means **logical pooling and governed placement**, not pretending every device is one physically coherent accelerator.

The architecture must preserve:

```text
accelerator compatibility
VRAM / HBM capacity
memory bandwidth
interconnect topology
network bandwidth / latency
data locality / residency
runtime / scheduler capability
trust / attestation
reservation / quota
failure domains
```

Therefore:

```text
one logical capital pool
!=
one physical GPU
```

## 4. Training vs inference

Placement policy must distinguish workload coordination requirements.

### Tightly coupled training

Prefer a single high-bandwidth execution domain with suitable accelerator topology. Cross-WAN aggregation is not treated as equivalent capacity.

### Distributed inference / batch / evaluation / agent workloads

May be spread across execution domains when authority, locality, latency, quality and economics permit.

## 5. v7.1 control chain

```text
Principal / Organization
 -> Workload Portfolio
 -> Authority / Policy
 -> Resource Intelligence
 -> Compute Federation / Resource Fabric
 -> Placement
 -> Computational Capital Allocation
 -> Execution Strategy
 -> Sovereign Execution Control
 -> Telemetry / Evidence / Failure
 -> Outcome / Economic Value
 -> Learning / Recovery / Reallocation
```

Allocation and placement are coupled but distinct:

- **Allocation:** how much scarce computational capital a workload deserves.
- **Placement:** where that admitted capital can be spent most effectively and safely.

## 6. Economics

Effective computational cost now explicitly includes federation effects:

```text
Monetary Cost
+ Quota Scarcity
+ Capacity Fragmentation
+ Network / Locality Cost
+ Latency Scarcity
+ Risk Cost
+ Verification Cost
+ Human Attention Cost
+ Opportunity Cost
+ Recovery Reserve Cost
```

The allocator may reserve scarce high-bandwidth or high-trust capacity for workloads with higher marginal value.

## 7. Standards / adapter boundary

Rasputin does not replace commodity schedulers or accelerator runtimes.

Examples of execution substrates/adapters include:

```text
Kubernetes
Slurm
cloud schedulers
provider APIs
local runtimes
MCP / A2A
OpenTelemetry
attestation systems
```

Rasputin owns the higher-order semantics: cross-domain resource intelligence, capital allocation, placement policy, authority, evidence, recovery and reallocation.

## 8. R1 compatibility

The currently admitted R1 contract scope remains frozen.

The v7.1 federation objects are **target architecture**, not an instruction to inject R2+ behavior into R1.

No R1 task should be reopened solely because v7.1 exists unless a proven contradiction with the existing canonical contract semantics is found.

## 9. Acceptance criteria for later federation stages

A future implementation gate should require evidence for:

- discovery of heterogeneous execution domains;
- normalized capability inventory;
- deterministic placement baseline;
- topology/locality constraint enforcement;
- capacity reservation/release;
- provider/cluster failover eligibility;
- placement reason codes;
- fragmentation and utilization metrics;
- policy-safe cross-domain execution;
- failure-domain isolation;
- reproducible benchmark uplift versus non-federated baselines.

## 10. Strategic consequence

v7.0 established **computational capital allocation**.

v7.1 adds the missing physical-to-economic bridge:

```text
heterogeneous physical compute
 -> federated logical resource fabric
 -> governed computational capital
 -> risk-adjusted allocation
 -> placement
 -> execution
 -> measured outcome
```

This makes Rasputin a control plane for both **where computational capital should be spent** and **where that capital can physically execute**.

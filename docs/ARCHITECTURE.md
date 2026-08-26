# Rasputin v6.0-alpha — Technical Architecture

> Status: PRE-DEVELOPMENT  
> Architecture mode: controller-first / stage-gated / evidence-first  
> Purpose: freeze contracts before implementation.

## 1. System Objective

Rasputin is an Agent resource-allocation and execution-governance infrastructure layer.

Its optimization target is:

```text
maximize Expected Task Utility
subject to:
  Cost <= Budget
  Quality >= Q*
  Risk <= R*
  Verifiability >= V*
```

Execution policy π may allocate:

```text
Model + Agent + Harness + Tools + Memory + Compute + Verification
```

## 2. Architectural Boundaries

### Rasputin owns

- canonical execution schema
- task/policy contracts
- routing decision interface
- economics telemetry
- evidence/provenance model
- optimization feedback interface
- governance decisions

### Rasputin integrates

- model gateways such as LiteLLM
- MCP-compatible tools
- orchestration runtimes such as LangGraph where appropriate
- vector databases / RAG engines
- local and cloud model providers
- sandbox runtimes
- identity / attestation providers
- blockchain anchoring backends

### Rasputin does not treat as moat

- generic multi-agent chat
- generic RAG
- generic vector storage
- generic LLM proxying
- generic blockchain logging
- generic code interpreter

## 3. Core Components

### 3.1 Task Contract

A task must be representable independently from any model/provider.

Required conceptual fields:

```text
task_id
objective
input_refs
quality_requirement
budget
risk_level
privacy_level
verification_level
timeout
metadata
```

### 3.2 Policy Engine

Inputs:

```text
Task + Tenant Policy + Runtime State
```

Outputs:

```text
Allowed Execution Space + Hard Constraints + Approval Requirements
```

Policy evaluation occurs before routing and is recorded in evidence.

### 3.3 Economics Engine

Inputs:

```text
Task
Allowed Execution Space
Historical Telemetry
Runtime Prices/Capabilities
```

Output:

```text
ExecutionPlan
```

An ExecutionPlan can specify model, harness, tools, memory strategy, compute target and verification level.

### 3.4 Execution Plane

Responsible only for carrying out an accepted ExecutionPlan and emitting events.

Initial implementation should prefer a small deterministic interface over a broad Agent framework abstraction.

### 3.5 Telemetry Plane

Minimum measurements:

```text
tokens_in
tokens_out
estimated_cost
latency_ms
status
error_type
quality_signals
cache_hit
retry_count
```

Telemetry must be machine-readable and joinable by task_id/run_id.

### 3.6 Evidence Plane

Evidence is not equivalent to raw logs.

Evidence records the claims needed to reconstruct and verify an execution:

```text
run identity
policy identity/version
execution-plan identity
input/output commitments
runtime/tool/model identities
timestamps
telemetry commitment
parent evidence
```

P0 target:

```text
Canonical serialization -> hash -> chained record -> Merkle batch
```

External anchoring is deliberately excluded from P0.

### 3.7 Optimization Loop

P0 optimization is experiment-driven rather than autonomous mutation.

The system should be able to compare two or more execution strategies against the same workload and produce reproducible economics/quality results.

Autonomous harness modification is deferred until evaluation and rollback contracts exist.

## 4. Canonical Execution Flow

```text
Task Submitted
    |
    v
Task Validation
    |
    v
Policy Evaluation
    |
    v
Candidate Strategies
    |
    v
Economics Evaluation
    |
    v
ExecutionPlan Selected
    |
    v
Execution
    |
    +----> Telemetry
    |
    +----> Evidence
    |
    v
Quality Evaluation
    |
    v
Run Finalization
    |
    v
Experiment / Optimization Dataset
```

## 5. Trust Model

P0 trust assumptions:

- local Rasputin runtime is trusted enough to create provenance records;
- cryptographic commitments detect post-hoc mutation but do not by themselves prove trusted hardware execution;
- external runtime attestation is an adapter-level future capability;
- public blockchain anchoring strengthens timestamp/existence claims but does not prove semantic correctness;
- zero-knowledge proofs will target policy/compliance statements, not hidden chain-of-thought.

## 6. Data Strategy

Rasputin must retain structured execution telemetry suitable for both engineering optimization and research.

Core analytical record:

```text
(Task, Strategy, Model, Harness, Tools, Cost,
 Latency, Quality, Failure, Verification, Policy)
```

Sensitive payloads should be referenced or committed by hash where possible rather than duplicated into analytics tables.

## 7. Testbeds

### FlowTracer

Primary recurring-workload testbed for routing, caching, quality/cost and monitoring workloads.

### Möbius

Primary harness/workflow testbed for orchestration, review gates, evidence and development-loop optimization.

Vertical terminals remain consumers of the kernel.

## 8. P0 Non-Goals

Do not block Rasputin Core on:

- polished UI
- full multi-agent visualization
- public-chain deployment
- smart contracts
- zk circuits
- A2A protocol invention
- multimodal chart extraction
- complete Obsidian executable environment
- enterprise multi-tenancy

## 9. Architecture Gates

Implementation cannot advance simply because code exists.

Each phase must produce evidence:

```text
CODE + TEST + BUILD + PERFORMANCE + SECURITY + DECISION
```

A phase closes only when its acceptance gate is satisfied and the Controller records the decision.

## 10. Version Boundary

v5.0 is retained as the historical full-domain vision.

v6.0-alpha is the executable architecture that narrows the first implementation around:

```text
Execution Schema
Policy
Economics
Routing
Telemetry
Evidence
Optimization
```

All later capabilities must attach to these contracts rather than bypass them.

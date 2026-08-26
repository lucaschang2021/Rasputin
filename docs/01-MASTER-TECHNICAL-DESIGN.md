# Rasputin v6.0-alpha — Master Technical Design

> **Purpose:** Define the complete target system before feature-by-feature implementation.  
> **Mode:** Pre-planned, backend-first, stage-gated development.

## 1. System Mission

Rasputin is a full-stack Agent infrastructure kernel for economically efficient, governed and verifiable intelligent execution across finance, legal, supply-chain and other high-responsibility domains.

It is designed to answer four questions for every task:

1. **What resources should execute this task?**
2. **Under what policy constraints may they execute?**
3. **What did the system actually execute and at what economic cost?**
4. **How can the next execution become better without violating governance?**

## 2. Target Architecture

```text
                 APPLICATION / TERMINAL / OBSIDIAN
                              |
                              v
                    +------------------+
                    |   TASK GATEWAY   |
                    +---------+--------+
                              |
                              v
                    +------------------+
                    |  POLICY ENGINE   |
                    +---------+--------+
                              |
                              v
                  +----------------------+
                  | ECONOMICS / ROUTER   |
                  +----------+-----------+
                             |
                 +-----------+-----------+
                 |                       |
                 v                       v
        +----------------+       +----------------+
        | AGENT RUNTIME  |       | TOOL / MCP BUS |
        +-------+--------+       +-------+--------+
                |                        |
                +-----------+------------+
                            |
                            v
                 +-----------------------+
                 | EXECUTION SUPERVISOR  |
                 +-----+-----------+-----+
                       |           |
                       v           v
                 TELEMETRY      EVIDENCE
                       |           |
                       +-----+-----+
                             |
                             v
                 +-----------------------+
                 | QUALITY / EVALUATION  |
                 +-----------+-----------+
                             |
                             v
                 +-----------------------+
                 | OPTIMIZATION ENGINE   |
                 +-----------+-----------+
                             |
                             +----> future policies / routing / harnesses
```

## 3. Core Subsystems

### 3.1 Task Gateway

Responsibilities:

- validate canonical task contracts;
- attach tenant/context metadata;
- assign trace/run identities;
- normalize application-specific input into Rasputin contracts;
- reject malformed or unsupported requests before model/tool expenditure occurs.

Future support:

- REST/HTTP;
- local IPC;
- Python SDK;
- CLI;
- MCP/A2A-compatible entry adapters.

### 3.2 Policy Engine

Policy Engine is authoritative for what may happen.

It evaluates:

```text
Task
+ Tenant Policy
+ Data Classification
+ Runtime Context
+ Operator Rules
```

against constraints including:

- max total cost;
- allowed/denied models;
- allowed/denied tools;
- local-only / cloud-allowed modes;
- privacy classes;
- verification levels;
- retry ceilings;
- execution time limits;
- human approval gates;
- domain compliance profiles.

The Policy Engine never chooses a plan merely because it is cheaper; it defines the feasible execution space.

### 3.3 Agent Economics Engine

This is a principal Rasputin differentiator.

It evaluates candidate strategies over dimensions such as:

```text
Model
Harness
Agent topology
Tool set
Memory strategy
Local/cloud compute
Cache strategy
Verification intensity
```

Conceptual objective:

```text
argmax StrategyUtility
```

where utility can incorporate quality, expected success, latency, monetary cost, verification burden and risk.

P0 begins with deterministic rules and experimental comparisons. Later versions may use learned routing, bandits, Bayesian optimization or offline policy learning.

### 3.4 Gateway & Model Abstraction

Initial implementation may integrate LiteLLM or equivalent adapters.

Core requirements:

- provider-independent request abstraction;
- provider capability registry;
- normalized usage/cost accounting;
- retries/fallbacks controlled by policy;
- local model adapter support;
- semantic cache interface;
- model health/circuit-breaker signals.

Vendor gateway code is replaceable infrastructure, not Rasputin's identity.

### 3.5 Agent Runtime

Agent Runtime supports increasing execution sophistication:

**Level 0:** direct single-model task.  
**Level 1:** model + tools.  
**Level 2:** planner/executor.  
**Level 3:** planner/executor/reviewer.  
**Level 4:** adaptive multi-agent workflows.

Important rule:

> Multi-agent execution is selected only when its measured marginal utility justifies its marginal economic and reliability cost.

Possible orchestration adapters include LangGraph or other compatible runtimes, but Rasputin contracts must remain independent from a specific orchestration library.

### 3.6 MCP / Tool Bus

Responsibilities:

- tool discovery and registration;
- capability metadata;
- schema validation;
- permission enforcement;
- invocation tracing;
- normalized success/failure results;
- tool cost and latency tracking.

Future vertical packs:

- Financial MCP Pack;
- Legal MCP Pack;
- Supply-chain MCP Pack;
- Research/Data MCP Pack.

### 3.7 Memory System

Memory is layered rather than one vector database:

```text
L0 Run Context
L1 Working Memory
L2 Episodic Execution Memory
L3 Semantic Knowledge / RAG
L4 SOP / Procedural Memory
```

Memory writes are governed by explicit retention policy. Sensitive payloads must not automatically become long-term memory.

### 3.8 Execution Supervisor

The Supervisor owns runtime lifecycle:

```text
prepare -> execute -> observe -> retry/abort -> finalize
```

It must support:

- cancellation;
- timeout;
- retry budgets;
- idempotency keys where applicable;
- tool/model failure isolation;
- circuit breakers;
- parent/child run relationships;
- structured event emission.

### 3.9 Telemetry & Observability

Rasputin records normalized execution economics and reliability signals:

```text
input/output tokens
provider/model
cache hits
cost
latency
retry count
failure class
tool calls
quality signal
policy decision
verification level
```

The telemetry layer serves both operations and future academic/economic analysis.

### 3.10 Evidence & Provenance

Rasputin is evidence-first.

Initial chain:

```text
Canonical Execution Record
        -> Content Hash
        -> Parent-linked Hash Chain
        -> Merkle Batch
        -> Optional External Anchor
```

Evidence may commit to:

- input/output references;
- model/runtime identity;
- policy version;
- execution plan;
- tool invocations;
- telemetry digest;
- quality result;
- timestamps;
- parent execution evidence.

Later adapters may provide hardware attestation, enterprise ledgers or L2 anchoring.

### 3.11 Quality & Evaluation

Quality must be explicit enough to compare strategies.

Possible evaluators:

- deterministic checks;
- reference-based scoring;
- domain rules;
- reviewer models;
- human labels;
- task success signals;
- downstream business metrics.

No optimization loop may optimize an undefined quality metric.

### 3.12 Optimization Engine

Stages:

**v0:** experiment registry + baseline comparison.  
**v1:** historical telemetry-assisted routing.  
**v2:** harness/routing recommendations.  
**v3:** guarded automatic optimization with rollback.  
**v4:** cross-workload learned execution policies.

Automatic mutation must never bypass policy, evaluation or rollback gates.

## 4. Security Architecture

Security principles:

- secrets never stored in source;
- least-privilege tool access;
- data classification before external transmission;
- sandboxed code execution;
- explicit local-only execution policies;
- signed/versioned policy artifacts in mature stages;
- no raw chain-of-thought requirement;
- sensitive evidence uses commitments/hashes rather than payload duplication;
- dependency pinning and supply-chain scanning;
- audit trails for administrative actions.

## 5. Zero-Knowledge Strategy

Rasputin will not claim to prove hidden model reasoning.

The R&D objective is to prove statements such as:

```text
execution used an approved model
execution stayed inside approved tool set
private risk score satisfied threshold
required policy version was enforced
required environment/attestation was present
```

without revealing protected business data.

This is **Zero-Knowledge Compliance**, not chain-of-thought proof.

## 6. Cross-Organization / A2A Strategy

Long-term Rasputin treats A2A as an interoperability surface around which it can provide:

- identity;
- policy;
- permissions;
- economics;
- evidence;
- settlement hooks.

It should adopt interoperable standards rather than create a closed protocol unless a concrete unmet requirement proves necessary.

## 7. Application Surfaces

Rasputin Core must support multiple consumers without domain coupling.

### FlowTracer

Real recurring information workload for routing/cost/cache experiments.

### Möbius

Harness and engineering-workflow laboratory.

### FinTerminal

Finance vertical integrating research, allocation, risk, audit and financial data tools.

### Future terminals

LawTerminal, SupplyTerminal and other domain packs are plugin/application layers.

## 8. Repository Target

```text
rasputin/
  core/
    contracts/
    policy/
    economics/
    routing/
    runtime/
    telemetry/
    evidence/
    evaluation/
    optimization/
  adapters/
    models/
    mcp/
    storage/
    attestation/
    anchoring/
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
  fixtures/
  docs/
  scripts/
  infra/
```

Exact language/framework layout may evolve during backend baseline selection, but architectural boundaries must remain recognizable.

## 9. Strength Targets

Rasputin should become powerful through depth, not uncontrolled feature count.

Target characteristics:

- provider-agnostic;
- framework-agnostic contracts;
- local/private capable;
- multi-agent capable;
- measurable economics;
- strong policy enforcement;
- cryptographic provenance;
- rich observability;
- reproducible evaluation;
- extensible adapters;
- safe optimization;
- cross-domain applicability;
- future-ready verification and A2A support.

## 10. Implementation Law

The complete vision is preserved, but implementation proceeds in strict dependency order.

```text
strong foundation
before broad surface area
before autonomous optimization
before protocol-level ambition
```

Rasputin should eventually be extremely capable; it must not become fragile in the process.

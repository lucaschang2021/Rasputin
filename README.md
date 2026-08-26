# Rasputin

> **Agent Economics & Execution Governance Infrastructure**  
> 面向 Agent 时代的资源配置、可信执行与跨域协作基础设施。

**Status:** Pre-Development / Architecture Locked for v6.0-alpha  
**Runtime:** Local-first · Model-agnostic · MCP-native  
**Architecture:** Policy-first · Evidence-first · Economics-driven  
**License:** TBD

---

## What is Rasputin?

Rasputin 不再被定义为“堆叠多 Agent、区块链、RAG 与 zk 的超级应用”。

它的核心问题是：

> 在质量、风险、隐私、审计与预算约束下，如何为一个 Agent 任务选择最优的模型、Harness、工具、记忆、算力与验证等级，并产生可追溯的执行证据？

Rasputin 的核心抽象：

```text
maximize   Expected Task Utility
subject to Cost <= Budget
           Quality >= Q*
           Risk <= R*
           Verifiability >= V*
```

其中执行策略：

```text
π = (Model, Agent, Harness, Tools, Memory, Compute, Verification)
```

因此：

**Rasputin = Agent Resource Allocation + Execution Governance.**

---

## Core Principles

- **Tasks declare constraints.**
- **Policies govern execution.**
- **Rasputin allocates resources.**
- **Agents execute.**
- **Telemetry measures economics.**
- **Evidence proves execution.**
- **Optimization improves the next run.**

---

## v6 Architecture

```text
Application / User
        |
        v
+-------------------+
|       TASK        |
+---------+---------+
          |
          v
+-----------------------------+
|      POLICY ENGINE          |
| cost / quality / risk       |
| privacy / audit / SLA       |
+-------------+---------------+
              |
              v
+-----------------------------+
|   AGENT ECONOMICS ENGINE    |
| model / agent / harness     |
| tools / memory / compute    |
| verification                |
+-------------+---------------+
              |
              v
+-----------------------------+
|      EXECUTION PLANE        |
| MCP / tools / code / agents |
+-------------+---------------+
              |
       +------+------+
       |             |
       v             v
 TELEMETRY        EVIDENCE
 cost             provenance
 latency          hashes
 quality          attestation
 failure          policy record
       |             |
       +------+------+
              |
              v
+-----------------------------+
|      OPTIMIZATION LOOP      |
| routing / harness / policy  |
+-----------------------------+
```

---

## The Seven Core Layers

### 1. Execution Schema

Every execution is represented by a common schema containing at minimum:

- task_id / run_id
- policy_id / policy_version
- model / agent / harness
- tools / memory references
- input_hash / output_hash
- token usage / monetary cost
- latency
- status / error
- quality signals
- verification level
- evidence references

The schema is the contract connecting routing, metering, governance, audit and research telemetry.

### 2. Policy Engine

Policy is evaluated before execution.

Initial constraints include:

- max_cost
- allowed_models
- allowed_tools
- minimum_quality
- privacy_level
- verification_level
- timeout / retry limits
- human-approval requirements

### 3. Agent Economics Engine

The economics engine selects an execution strategy rather than simply selecting the strongest model.

Optimization dimensions include:

- model selection
- local vs cloud execution
- semantic cache
- harness strategy
- tool allocation
- memory allocation
- verification intensity

LiteLLM and compatible gateways are infrastructure dependencies, not Rasputin's moat.

### 4. Execution Plane

MCP-native execution layer supporting heterogeneous tools, local runtimes, APIs and future cross-agent protocols.

Initial execution can be single-agent. Multi-agent orchestration is introduced only where measurable utility exceeds its added economic cost.

### 5. Telemetry & Observability

Every run produces structured telemetry:

```text
Task
Model
Harness
Tools
Tokens
Cost
Latency
Quality
Failure
Verification
```

This dataset is a first-class Rasputin asset and enables empirical Agent Economics research.

### 6. Evidence Layer

Rasputin is evidence-first rather than blockchain-first.

```text
Execution
   -> Structured Evidence
   -> Local Hash Chain
   -> Merkle Aggregation
   -> Optional External Anchoring
```

L0 — local provenance and hash chain  
L1 — Merkle aggregation  
L1.5 — optional private synchronization  
L2 — optional public-chain anchoring  
L3 — optional enterprise approval / smart-contract controls

Blockchain is one possible settlement and anchoring backend, not a mandatory execution dependency.

### 7. Optimization Loop

Execution telemetry feeds routing, policy and harness improvement.

The long-term target is not merely self-reflection, but measurable optimization of:

```text
Utility / Total Economic Cost
```

under explicit governance constraints.

---

## Trust, Verification & Zero Knowledge

The v5 concept of proving an Agent's complete “reasoning process” is replaced by a narrower and more defensible objective:

> Prove that an execution satisfied defined policy and compliance constraints without revealing protected inputs or business data.

Future zk research therefore focuses on **Zero-Knowledge Compliance Proofs** and verifiable execution claims such as:

- approved model was used
- approved tool set was respected
- policy version was enforced
- required execution environment was used
- a private risk/compliance condition was satisfied

zk-SNARK/STARK integration remains an R&D track until the execution/evidence schema is stable.

---

## A2A / Cross-Domain Collaboration

Cross-organization Agent collaboration remains a long-term strategic layer.

Rasputin will not invent a closed communication ecosystem where interoperable standards exist. It will instead provide policy, identity, economics and evidence around compatible A2A/MCP-style communication.

Target flow:

```text
Organization A Agent
       |
 policy + identity + evidence
       |
       v
Cross-domain Agent Protocol
       |
       v
Organization B Agent
```

---

## Product Testbeds

### FlowTracer — Workload Testbed #001

FlowTracer provides recurring, measurable real-world workloads for routing, cache, model selection, cost and quality experiments.

### Möbius — Harness Laboratory

Möbius provides structured AI-engineering workflows and a natural environment for harness, orchestration, review-gate and self-improvement experiments.

### Terminal Applications

Future vertical applications can include FinTerminal, LawTerminal and SupplyTerminal. They consume Rasputin Core rather than defining it.

---

## Obsidian: Human–Agent Environment

Obsidian remains the preferred knowledge and human interaction surface, but is not part of the P0 kernel.

Long-term capabilities:

- automatic execution/audit notes
- research telemetry summaries
- SOP and memory persistence
- executable Markdown commands
- context-aware Agent invocation

---

## Pre-Development Roadmap

Rasputin follows a controller-first, stage-gated development model inspired by Möbius.

```text
Discover -> Read -> Dispatch -> Execute -> Observe -> Accept -> Decide -> Archive
```

### Phase P0 — Rasputin Core

| Phase | Objective | Gate |
|---|---|---|
| CORE-0 | Repository + architecture + contracts | docs accepted |
| CORE-1 | Execution Schema | schema tests pass |
| CORE-2 | Metering & Telemetry | deterministic telemetry |
| CORE-3 | Gateway / Resource Router | multi-model routing demonstrated |
| CORE-4 | Policy Engine | constraints enforced |
| CORE-5 | Evidence Chain | hash-chain + Merkle verification passes |
| CORE-6 | Economics Evaluator | cost/quality comparison reproducible |
| CORE-7 | Optimization Loop v0 | policy/routing experiment demonstrated |

### Phase P1 — Agent Runtime

- MCP execution adapters
- Planner / Executor / Reviewer where economically justified
- semantic cache
- local/private model support
- local memory / RAG
- sandboxed code execution

### Phase P2 — Trust Infrastructure

- identity and attestation adapters
- private evidence synchronization
- optional L2 anchoring
- HITL / enterprise approval controls
- multi-tenant governance

### Phase P3 — Protocol R&D

- cross-domain A2A collaboration
- Zero-Knowledge Compliance Proofs
- executable Obsidian environment
- advanced self-optimizing harnesses

---

## Development Rule

No feature enters implementation merely because it is technically impressive.

A feature must improve at least one of:

1. task utility,
2. total economic cost,
3. execution risk,
4. verifiability,
5. interoperability.

New ideas default to backlog until they satisfy this rule and the current phase gate is complete.

---

## Research Thesis

Rasputin is also an experimental infrastructure for **Agent Economics**.

A future dataset can take the form:

```text
D = {Task, Model, Harness, Tools, Cost, Latency, Quality, Failure, Verification}
```

This supports research into model/harness substitution, constrained resource allocation, verification capital, AI production functions and optimal AI capital allocation.

---

## Current State

**v5.0:** frozen as the original full-domain vision.  
**v6.0-alpha:** pre-development architecture.  
**Current priority:** define and validate Rasputin Core before expanding vertical applications or protocol-level R&D.

Rasputin is not trying to own every model, tool, blockchain or Agent framework.

It aims to become the layer that decides **how intelligent work should be allocated, governed, measured and proven.**

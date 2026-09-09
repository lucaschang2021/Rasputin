# Rasputin

> **Sovereign Computational Capital Control Plane**  
> 面向 Agent 时代的计算资本配置、执行主权、对抗保证与自适应恢复基础设施。

**Status:** v7.0 Strategic Migration / Pre-Implementation  
**Runtime:** Local-first · Vendor-neutral · MCP/A2A-compatible  
**Architecture:** Portfolio-first · Authority-first · Economics-driven · Evidence-backed · Adversarially tested  
**License:** TBD

---

## What is Rasputin?

Rasputin 不与 frontier model 竞争智能，也不把自己定义成通用 Multi-Agent、RAG、LLM Gateway、审计或区块链产品。

它回答一个更高层的问题：

> **在预算、算力、quota、时间、权限、隐私、验证、风险与不可逆性约束下，有限的 intelligence / compute / tools / memory / verification / human attention 应该被配置到哪些工作负载，如何被授权执行，并如何依据真实 outcome 在故障与对抗中持续恢复和重新配置？**

核心对象：

```text
Principal / Organization
        ↓
Workload Portfolio
        ↓
Computational Capital Allocation
        ↓
Execution Strategy
        ↓
Authorized Execution
        ↓
Outcome / Evidence / Failure
        ↓
Learning + Recovery + Reallocation
```

Rasputin 的原子经济对象仍然是 **Execution**；v7 在其上增加 **Workload Portfolio** 与 **Computational Capital** 两个组织级抽象。

---

## Core Thesis

### Intelligence is capital

AI execution 消耗的不只是 API money：

```text
Money
Tokens / inference compute
Provider quota
Time / latency
Tools
Memory / context
Verification capacity
Human attention
Risk capacity
Irreversibility capacity
Recovery capacity
Opportunity cost
```

因此 Rasputin 以有效计算资本成本而不是名义 token 价格做决策。

### Portfolio before routing

普通 router 问：

```text
Prompt -> Which model?
```

Rasputin 先问：

```text
Which workloads deserve capital now?
How much capital should each receive?
Which admissible strategy should spend it?
```

`DO_NOT_EXECUTE`, `DEFER` 和 `WAIT_FOR_INFORMATION` 都是合法策略。

### Outcome before output

```text
Model Output
 -> Technical Success
 -> Task Success
 -> Workflow Outcome
 -> Business / Research Outcome
 -> Economic / Strategic Value
```

Rasputin 优化真实 outcome，不把 LLM judge 分数当最终价值。

### Authority before autonomy

Rasputin 必须能够：

```text
AUTHORIZE · ALLOCATE · DISPATCH · LIMIT · SUSPEND
REVOKE · REROUTE · RECOVER · ESCALATE · TERMINATE
```

真正的 control plane 不只是推荐。

---

## v7 Architecture

```text
                    PRINCIPAL / ORGANIZATION
                             |
                             v
+-----------------------------------------------------------+
| 1. WORKLOAD & PORTFOLIO PLANE                             |
+-----------------------------------------------------------+
| 2. AUTHORITY & POLICY PLANE                               |
+-----------------------------------------------------------+
| 3. RESOURCE INTELLIGENCE PLANE                            |
+-----------------------------------------------------------+
| 4. COMPUTATIONAL CAPITAL ALLOCATOR                        |
+-----------------------------------------------------------+
| 5. EXECUTION STRATEGY COMPILER                            |
+-----------------------------------------------------------+
| 6. SOVEREIGN EXECUTION CONTROL PLANE                      |
+-----------------------------------------------------------+
| 7. OUTCOME / TELEMETRY / EVIDENCE / FAILURE INTELLIGENCE  |
+-----------------------------------------------------------+
| 8. LEARNING & REALLOCATION ENGINE                         |
+-----------------------------------------------------------+
         ^                                   |
         |                                   v
+-------------------------+       +-------------------------+
| RED-BLUE ADVERSARIAL    |       | ADAPTIVE RECOVERY      |
| ASSURANCE LOOP          |       | & SELF-HEALING LOOP     |
+-------------------------+       +-------------------------+
         |                                   |
         +----------------+------------------+
                          v
                 POLICY / CAPITAL UPDATE
```

Red-Blue 与 Adaptive Recovery 是跨层永久控制循环，不是附属安全插件。

---

## The v7 Core

### 1. Workload & Portfolio Plane

描述 objective、priority、deadline、expected value、uncertainty、quality floor、risk tolerance、privacy、irreversibility 和 dependencies。

### 2. Authority & Policy Plane

定义允许发生什么，并在 runtime 强制执行：identity、authorization、data classification、budget、risk、tool/model permissions、HITL、recovery ceiling 与 irreversibility constraints。

### 3. Resource Intelligence Plane

统一描述可配置生产要素：

```text
Models · Agents · Harnesses · MCP Tools · A2A Agents
Memory · Retrievers · Verifiers · Human Reviewers
GPU / Runtime · API Quota · Sandboxes · Attested Environments
```

资源具有 capability、nominal price、shadow price、health、availability、historical outcome、risk、privacy 与 attestation metadata。

### 4. Computational Capital Allocator

核心目标从单请求 routing 升级为 portfolio optimization：

```text
maximize Risk-Adjusted Outcome Value
subject to money / compute / quota / time / risk /
verification / human-attention / irreversibility / recovery budgets
```

算法路线：deterministic rules → Lagrangian allocation → constrained contextual bandits / bandits-with-knapsacks → offline policy learning → constrained sequential control。

### 5. Execution Strategy Compiler

将 allocation 转化为具体策略：

```text
pi = (
  model,
  harness,
  agent_topology,
  tools,
  memory,
  test_time_compute,
  verification,
  runtime,
  recovery_policy
)
```

Multi-Agent 是可选 Execution Strategy；只有边际效用高于边际经济与可靠性成本时才启用。

### 6. Sovereign Execution Control Plane

负责 prepare → authorize → execute → observe → limit → recover / abort → finalize。MCP、A2A、OpenRouter、LiteLLM、LangGraph 等属于标准或 adapter，不定义 Rasputin。

### 7. Outcome / Telemetry / Evidence / Failure Intelligence

记录的不只是 token、cost 和 latency，而是：

```text
Workload
Strategy
ResourceState
NominalCost
ShadowCost
RiskConsumed
IrreversibilityConsumed
Failure
Recovery
Outcome
EconomicValue
Evidence
```

核心长期数据资产：

```text
D = {Workload, Context, ResourceState, Strategy,
     Cost, Risk, Attack, Failure, Recovery, Outcome, Value}
```

### 8. Learning & Reallocation Engine

```text
Outcome
 -> Credit Assignment
 -> Counterfactual / Offline Evaluation
 -> Policy Learning
 -> Safe Deployment
 -> Online Exploration
 -> Capital Reallocation
```

自动优化永远不得绕过 policy、evaluation、rollback 和 recovery gates。

---

## Shadow Price of Intelligence

名义价格不是真实价格。

概念上：

```text
Effective Computational Cost =
    Monetary Cost
  + Quota Scarcity Cost
  + Latency Scarcity Cost
  + Risk Cost
  + Verification Cost
  + Human Attention Cost
  + Opportunity Cost
  + Recovery Reserve Cost
```

Rasputin 可以因为 quota 极度稀缺而把某个 nominally cheap resource 视为昂贵资源，并将其保留给更高价值 workload。

---

## Red-Blue Adversarial Assurance

Red Team 必须攻击整个 execution economy，而不仅是 prompt：

```text
Allocator manipulation
Fake value / urgency / scarcity
Policy bypass
Prompt/tool injection
Poisoned memory/context
Compromised resource
Verifier failure
Telemetry manipulation
Outcome manipulation
Quota / latency / provider shocks
Recovery-engine abuse
```

Blue Team 可以采取：

```text
policy tightening
privilege reduction
quarantine
sandbox escalation
extra verification
human approval
resource replacement
memory rollback
execution cancellation
rate/budget reduction
```

目标是持续验证 **Computational Capital Integrity**。

---

## Adaptive Recovery & Economic Self-Healing

永久恢复协议：

```text
DETECT
 -> DIAGNOSE
 -> CONTAIN
 -> RECOVER
 -> VERIFY
 -> REALLOCATE
 -> LEARN
```

恢复不是无限 retry。若：

```text
Expected Remaining Outcome Value < Expected Recovery Cost
```

则必须允许 `ABORT / DEFER / HUMAN ESCALATION`。

Provider outage 等事故会更新 Resource Intelligence 与 shadow prices，然后触发 portfolio-level reallocation，而非仅对单个请求 fallback。

---

## Capital & Safety Budgets

v7 预算模型至少支持：

```text
Money Budget
Compute Budget
Token / Quota Budget
Latency Budget
Verification Budget
Human Attention Budget
Risk Budget
Irreversibility Budget
Recovery Budget
```

这些预算可以作用于 principal、tenant、portfolio、workload、execution 和 agent/tool scope。

---

## Verification & Trust

Verification 是可购买、可配置的 execution resource：

```text
Deterministic Test
Schema Validation
Reference / Domain Rule
LLM / Cross-Model Judge
Human Review
Runtime Attestation
Cryptographic Evidence
Business Outcome
```

Evidence 默认路径：

```text
Structured Execution Record
 -> Content Commitment
 -> Hash Chain
 -> Merkle Batch
 -> Optional Signature / Transparency / Attestation
 -> Optional External Anchor
 -> Future Zero-Knowledge Compliance
```

Rasputin 不证明 hidden chain-of-thought。ZK 仅用于未来 compliance predicates。

---

## Standards & Adapter Principle

永久规则：

```text
Frontier Theory      -> Rasputin Core
Frontier Technology  -> Standard / Adapter by default
```

优先复用并治理：

- MCP — tool/data interoperability;
- A2A — agent-to-agent interoperability;
- OpenTelemetry — raw observability transport;
- OPA/Rego / Cedar — policy backends where useful;
- SPIFFE/SPIRE — workload identity where useful;
- OpenRouter / LiteLLM / direct APIs — execution venues;
- LangGraph and other runtimes — orchestration adapters;
- Semantica / provenance systems — optional context/evidence adapters;
- TEE / attestation / transparency / anchoring systems — trust adapters.

Rasputin 的 moat 不应该是重复实现这些基础设施，而是决定何时、为何、以何种资本和权限使用它们。

---

## Product Testbeds

### FlowTracer — Workload Testbed #001

真实 recurring workload，用于 allocation、routing、cost、cache、quality、recovery 与 downstream business outcome 实验。

### Möbius — Harness Laboratory

测试 coding harness、review gates、agent topology、verification、recovery 和工程 outcome。

### FinTerminal — High-Responsibility Vertical

用于测试金融场景 policy、risk、evidence、human approval、privacy 和 outcome value。

### Clovis Bray — Measurement / Market Intelligence Layer

长期承担 computational capital measurement / pricing intelligence；Rasputin 负责 allocation / governance / control。

---

## Benchmarks

### Rasputin Capital Benchmark — RCB

至少对比：frontier-model-only、cheapest-model、static router、external auto-router、rule router、Rasputin。

核心指标：

```text
Success Rate
Verified Success
Total Effective Cost
Latency / SLA
Policy Violations
Risk / Irreversibility Consumption
Human Intervention
Portfolio Utility
Utility / $
Utility / Token
Utility / Compute
ROCC — Return on Computational Capital
```

### Rasputin Adversarial & Resilience Benchmark — RARB

```text
Attack Detection Rate
Policy Bypass Rate
Unauthorized Action Rate
MTTD / MTTR
Recovery Success Rate
Recovery Economic Cost
Blast Radius
Portfolio Utility Under Failure / Attack
Quarantine Success
Rollback Integrity
Capital Reallocation Efficiency
```

---

## v7 Roadmap

| Stage | Objective |
|---|---|
| R0 | Strategic Constitution + Threat/Economic Model + contract migration |
| R1 | Canonical Workload / Execution / Resource / Capital schemas |
| R2 | OpenTelemetry-compatible telemetry + Computational Capital Ledger |
| R3 | Resource Intelligence Registry |
| R4 | Authority / Policy / Runtime Enforcement |
| R5 | Provider + MCP + execution adapters + supervisor |
| R6 | Adaptive Recovery Engine v0 |
| R7 | Outcome / Quality / Failure Intelligence |
| R8 | Capital Allocator v0 — deterministic / Lagrangian |
| R9 | Rasputin Capital Benchmark v0 |
| R10 | Red-Blue Adversarial Assurance v0 |
| R11 | Offline learning + recovery learning |
| R12 | Contextual bandit / online allocation |
| R13 | Portfolio allocation + shadow pricing |
| R14 | Risk + Irreversibility + Recovery Budgets |
| R15 | MCP/A2A governance + enterprise attestation / multi-tenant authority |
| R16 | Inter-org markets / settlement / Zero-Knowledge Compliance R&D |

---

## Version Boundary

- **v5.0** — historical full-domain vision; frozen.
- **v6.0-alpha** — execution-economics migration baseline; superseded as strategic target but retained for migration history.
- **v7.0** — active strategic and technical target.

Current priority is **R0 architecture/contract migration**. Production backend implementation that would freeze v6 semantics must pause until v7 R0 is accepted.

---

## Permanent Development Law

A new capability enters Rasputin Core only if it materially improves at least one of:

1. risk-adjusted outcome value;
2. capital allocation efficiency;
3. execution authority or safety;
4. resilience / recovery efficiency;
5. verifiability;
6. interoperability;
7. learning quality.

Otherwise it is an adapter, experiment, backlog item or external dependency.

> **Rasputin decides where intelligence is worth spending — and keeps that decision governable, survivable and learnable.**

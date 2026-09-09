# Rasputin v7 — Delivery Board

> **Purpose:** Master implementation sequence for the v7 Sovereign Computational Capital Control Plane.  
> **Rule:** No stage skipping. Architecture/contract gates precede backend implementation.

## R0 — Strategic Constitution & Contract Migration

### R0-0 Constitution
- freeze v7 strategic definition;
- record v5 historical / v6 migration / v7 target boundaries;
- define core moat and adapter boundary;
- define red-blue and recovery as permanent cross-cutting loops.

### R0-1 Threat / Failure / Economic Model
- workload portfolio model;
- resource/capital model;
- shadow price semantics;
- risk / irreversibility / recovery budgets;
- adversarial threat classes;
- failure taxonomy;
- economic recovery stop rule.

### R0-2 Contract Migration
- Workload / Portfolio;
- Resource / ResourceState;
- BudgetEnvelope / BudgetLedger;
- PolicyDecision / AuthorityEnvelope;
- CapitalAllocation;
- ExecutionPlan / Run;
- Telemetry / Evidence;
- FailureRecord / RecoveryEpisode;
- QualityEvaluation / OutcomeRecord;
- RedBlueScenario / AssuranceResult.

### GATE-V7-R0

Acceptance requires:

```text
Architecture consistent
Contracts versioned
No unresolved v6/v7 semantic conflict
Migration notes explicit
Red-blue scope explicit
Recovery scope explicit
R1-R16 measurable
```

No production backend implementation that freezes v6 semantics may proceed before this gate.

---

## R1 — Canonical Workload / Execution / Resource Schemas

- executable schemas;
- deterministic serialization where required;
- golden fixtures;
- versioning / migration tests;
- valid `DO_NOT_EXECUTE / DEFER` decisions;
- resource health/state fixtures.

**Gate R1:** contract and round-trip tests pass with representative portfolio fixtures.

---

## R2 — Telemetry + Computational Capital Ledger

- OpenTelemetry-compatible raw events where practical;
- normalized money/token/compute/quota/latency measurements;
- reserve / consume / release / settle ledger operations;
- risk / irreversibility / recovery ledger representation;
- traceability by portfolio/workload/run/resource/allocation IDs.

**Gate R2:** deterministic ledger accounting and replay tests pass.

---

## R3 — Resource Intelligence Registry

- canonical resource registry;
- capability metadata;
- health / availability / quota state;
- nominal pricing;
- task-affinity history interface;
- shadow-price inputs;
- quarantine state.

**Gate R3:** at least two heterogeneous resources can be compared and invalidated by live state changes.

---

## R4 — Authority / Policy / Runtime Enforcement

- principal / tenant / workload authority scopes;
- model/tool/harness/resource allow/deny;
- budget constraints;
- privacy and data-egress controls;
- risk / irreversibility constraints;
- human approval artifacts;
- runtime deny / suspend / revoke controls.

**Gate R4:** denied or exhausted-capital actions cannot execute, including during fallback/recovery.

---

## R5 — Execution Adapters + Supervisor

- direct provider adapters;
- external router/gateway adapter boundary;
- local runtime adapter;
- MCP tool execution;
- A2A-compatible future boundary;
- run lifecycle;
- timeout / cancellation / circuit breakers;
- structured event emission.

**Gate R5:** policy-safe execution and provider/tool failure isolation demonstrated.

---

## R6 — Adaptive Recovery Engine v0

- failure detection;
- deterministic diagnosis taxonomy;
- containment;
- retry/reroute/substitute/abort/human escalation;
- resource quarantine;
- Recovery Budget;
- post-recovery verification;
- portfolio-level incident signal.

**Gate R6:** injected failures produce bounded recovery without policy bypass or unbounded retry.

---

## R7 — Outcome / Quality / Failure Intelligence

- evaluator interface;
- deterministic quality baseline;
- delayed OutcomeRecord attachment;
- technical/task/workflow/business outcome hierarchy;
- FailureRecord and RecoveryEpisode analytics;
- realized value and attribution confidence.

**Gate R7:** same workload can compare strategies using outcome and recovery data, not only LLM score.

---

## R8 — Capital Allocator v0

- workload admission;
- explicit utility/value estimates;
- deterministic portfolio budget allocation;
- Lagrangian / shadow-price baseline;
- `DO_NOT_EXECUTE / DEFER`;
- allocation reason codes;
- policy-safe Strategy Compiler.

**Gate R8:** constrained portfolio allocation is reproducible and beats or matches naive baseline without violating hard constraints.

---

## R9 — Rasputin Capital Benchmark v0

Baselines:

```text
frontier-model-only
cheapest-model
static rules
external auto-router where available
Rasputin allocator
```

Metrics:

```text
success
verified success
effective cost
latency / SLA
policy violations
risk / irreversibility consumption
human intervention
portfolio utility
utility / $
utility / token
utility / compute
ROCC
```

**Gate R9:** benchmark harness is reproducible and publishes raw result artifacts.

---

## R10 — Red-Blue Adversarial Assurance v0

- prompt/tool injection;
- policy bypass;
- fake value/urgency/scarcity;
- allocator gaming;
- poisoned context/memory;
- verifier manipulation;
- telemetry/outcome manipulation;
- quota/latency/provider shocks;
- recovery abuse;
- Blue containment controls;
- Shadow Mode / Controlled Chaos fixtures.

**Gate R10:** defined attack suite executes safely and produces measurable assurance results.

---

## R11 — Offline Learning + Recovery Learning

- historical strategy outcome models;
- recovery outcome models;
- offline policy evaluation;
- counterfactual comparison where defensible;
- shadow deployment;
- rollback metadata.

**Gate R11:** candidate learned policy cannot ship without offline evidence and baseline comparison.

---

## R12 — Contextual Bandit / Online Allocation

- bounded exploration;
- constrained contextual bandit interface;
- exploration budgets;
- non-stationary resource state handling;
- safety fallback to deterministic allocator.

**Gate R12:** online learning improves measured utility under fixed safety/budget envelopes in controlled benchmark.

---

## R13 — Portfolio Allocation + Shadow Pricing

- dynamic quota scarcity;
- opportunity cost;
- resource shadow prices;
- portfolio scheduling;
- capital reservation for high-value future work;
- Value-of-Information experiments.

**Gate R13:** portfolio-level decisions outperform independent per-request routing on at least one representative workload family.

---

## R14 — Risk / Irreversibility / Recovery Budget

- shared portfolio risk accounting;
- irreversible action admission control;
- recovery reserve accounting;
- human approval escalation;
- tail-risk / CVaR research adapter where justified.

**Gate R14:** cumulative risk/irreversibility cannot exceed authorized portfolio budget through individually legal actions.

---

## R15 — MCP/A2A Governance + Enterprise Authority

- governed MCP discovery/invocation;
- identity and capability scopes;
- A2A authority/economics/evidence wrappers;
- multi-tenant policy isolation;
- workload identity adapters;
- remote/runtime attestation adapters;
- enterprise audit surface.

**Gate R15:** cross-resource and cross-tenant authority remains isolated and evidence-backed.

---

## R16 — Inter-Organization Markets / Settlement / ZK Compliance R&D

Research scope only after prior gates:

- market-assisted allocation / auctions;
- inter-org execution contracts;
- settlement hooks;
- transparency / external anchoring;
- Zero-Knowledge Compliance predicates;
- advanced attestation.

No R16 technology may become a dependency of the core before its value is demonstrated.

---

## Frontend Activation Rule

Frontend production implementation begins only after the backend contracts needed for a surface are accepted. Early surfaces should focus on:

- portfolio / workload state;
- capital allocation decisions;
- resource health / shadow prices;
- execution authority state;
- recovery timeline;
- red-blue assurance results;
- outcome / ROCC dashboards;
- evidence verification.

Frontend never invents backend semantics.

---

## Integration & Release Law

Every release candidate must include, where applicable:

```text
contract tests
unit/integration/e2e tests
failure injection
security tests
red-blue scenarios
recovery scenarios
RCB / RARB evidence
performance data
migration notes
known limitations
Controller decision
```

A later stage may be researched early but cannot become an implementation dependency of an earlier stage without explicit Controller approval.

# Rasputin — Pre-Development Control Plan

> Mode: Möbius-style controller-first pre-development  
> Rule: no uncontrolled implementation before contracts and gates are accepted.

## 1. Operating Model

```text
Discover -> Read -> Dispatch -> Execute -> Observe -> Accept -> Decide -> Archive
```

Roles are separated conceptually even if one developer/agent performs several roles.

- **Controller** — owns scope, phase state, dispatch and final acceptance.
- **Backend** — implements kernel contracts and runtime components.
- **Frontend** — begins only when a stable user-facing contract exists.
- **Integration** — verifies cross-component behavior and repairs integration failures.
- **GitHub/Release** — maintains branch/PR/release/documentation hygiene.

Default engineering order:

```text
Controller -> Backend -> Frontend -> Integration/Test -> GitHub/Release
```

## 2. Task Identity

Every implementation task receives a stable ID.

Examples:

```text
CORE-1-T1
CORE-1-T2
CORE-2-T1
POLICY-1-T1
EVID-1-T1
```

Every task must state:

```text
ID
Objective
Inputs
Allowed scope
Forbidden scope
Deliverables
Tests
Acceptance evidence
Dependencies
Rollback note
Status
```

## 3. Evidence Standard

A task is not complete because an Agent says it is complete.

Acceptance may require:

- code diff
- unit/integration tests
- build output
- benchmark/performance output
- security/static checks where relevant
- schema/example artifacts
- Controller decision

Canonical principle:

> Agents execute. Git records. Evidence proves. The Controller governs.

## 4. P0 Phase Board

### CORE-0 — Architecture & Contracts

**Objective:** freeze P0 boundaries before kernel implementation.

Deliverables:

- README positioning
- architecture specification
- pre-development control plan
- execution schema specification
- policy contract specification
- evidence contract specification

Gate: `GATE-CORE-0`

Acceptance:

- no unresolved contradiction between contracts
- P0 non-goals explicitly recorded
- every next phase has measurable output

### CORE-1 — Execution Schema

Objective: create provider-independent canonical task/run/execution-plan schemas.

Gate requires:

- schema validation tests
- serialization stability tests
- representative example fixtures
- versioning rule

### CORE-2 — Metering & Telemetry

Objective: capture reproducible cost/latency/token/status telemetry.

Gate requires:

- deterministic normalized record
- provider adapter tests
- failure/retry representation
- joinability by task/run IDs

### CORE-3 — Gateway / Router

Objective: select between at least two execution resources according to declared constraints.

Gate requires:

- routing decision record
- fallback behavior
- budget constraint test
- reproducible comparison workload

### CORE-4 — Policy Engine

Objective: enforce execution constraints before dispatch.

Gate requires:

- allowed/denied model test
- allowed/denied tool test
- cost constraint test
- privacy/verification policy representation
- immutable policy version reference in evidence

### CORE-5 — Evidence Chain

Objective: produce tamper-evident local execution evidence.

Gate requires:

- canonical hashing
- chain verification
- mutation detection
- Merkle batch generation/verification
- evidence references to policy and execution plan

### CORE-6 — Economics Evaluator

Objective: compare strategies using total economic cost and quality signals.

Gate requires:

- common workload
- >=2 strategies
- normalized metrics
- reproducible report

### CORE-7 — Optimization Loop v0

Objective: use historical telemetry to recommend or select an improved strategy under constraints.

Gate requires:

- baseline vs optimized strategy
- no policy bypass
- measurable result
- rollback path

## 5. Pre-Development Backlog Classification

Every proposed capability is classified before implementation:

- **BUILD NOW** — necessary for current phase gate.
- **KEEP** — strategic capability with future phase.
- **INTEGRATE** — use an external standard/component rather than rebuild.
- **COMMODITIZED** — required infrastructure but not a moat.
- **DEFER** — does not justify current complexity.
- **RESEARCH** — requires technical/market validation before product commitment.

Current examples:

```text
Agent Economics Engine       BUILD NOW
Policy Engine                BUILD NOW
Execution Evidence           BUILD NOW
Metering/Telemetry           BUILD NOW
LiteLLM                      INTEGRATE
MCP                          INTEGRATE
LangGraph                    INTEGRATE / conditional
Vector DB / generic RAG      COMMODITIZED
Generic multi-agent UI       DEFER
L2 anchoring                 DEFER
A2A cross-domain layer       KEEP / RESEARCH
Zero-Knowledge Compliance    KEEP / RESEARCH
Obsidian executable mode     KEEP
Vision-to-Data               DEFER
```

## 6. Scope Firewall

During P0:

1. new ideas enter backlog by default;
2. no feature may bypass the Controller phase board;
3. no P1/P2/P3 capability may become a dependency of a P0 gate without an explicit architecture decision;
4. external standards are preferred over proprietary reinvention when they satisfy the contract;
5. optimization claims require measurement;
6. trust claims require evidence.

## 7. Branch / Worktree Recommendation

When implementation begins, preserve the established isolated workflow pattern:

```text
main                  accepted state
feat/backend-*        kernel/backend work
feat/frontend-*       UI work when activated
fix/integration-*     integration/test repair
ops/github-*          release/repository operations
```

Exact worktree creation is intentionally deferred until CORE-0 contracts are accepted.

## 8. First Dispatch Queue

No production implementation is authorized by this document alone.

The first Controller dispatch after CORE-0 acceptance should be:

```text
CORE-1-T1  Draft canonical Task schema
CORE-1-T2  Draft ExecutionPlan schema
CORE-1-T3  Draft Run/Telemetry schema
CORE-1-T4  Draft schema versioning rules
CORE-1-T5  Build schema validation fixtures/tests
```

Only after `GATE-CORE-1` passes should metering implementation begin.

## 9. Definition of Pre-Development Complete

Pre-development is complete when:

- core contracts are documented;
- P0 scope is frozen;
- non-goals are explicit;
- phase/task IDs exist;
- acceptance gates are measurable;
- first backend dispatch can be issued without architecture invention inside the coding task.

At that point Rasputin moves from **PRE-DEVELOPMENT** to **ACTIVE ALPHA DEVELOPMENT**.

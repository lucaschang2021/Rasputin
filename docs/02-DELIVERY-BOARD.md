# Rasputin — Delivery Board

> **Purpose:** Master implementation sequence.  
> **Rule:** Backend → Frontend → Integration/Test → GitHub/Release. No stage skipping.

## Release R0 — Core Foundation

### Backend Lane — P0

#### BE-0 Engineering Baseline
- repository/package layout
- runtime/configuration baseline
- logging/error model
- test harness
- CI-ready commands

**Gate BE-0:** project installs, starts, tests and lint/type checks are reproducible.

#### BE-1 Contracts
- canonical Task schema
- PolicyDecision schema
- ExecutionPlan schema
- Run / Telemetry schema
- QualityEvaluation schema
- EvidenceEnvelope references
- versioning and golden fixtures

**Gate BE-1:** contract tests + serialization stability + fixtures pass.

#### BE-2 Policy Kernel
- policy registry
- constraint validation
- allow/deny model rules
- allow/deny tool rules
- budget/privacy/verification constraints
- HITL gate representation

**Gate BE-2:** denied actions cannot reach execution; policy version is traceable.

#### BE-3 Model Gateway & Router
- provider abstraction
- >=2 model/resource adapters
- normalized token/cost accounting
- fallback/circuit-breaker baseline
- local/provider capability registry
- routing decision record

**Gate BE-3:** reproducible routing tests show constraint-aware selection and fallback.

#### BE-4 Execution Supervisor
- run lifecycle
- cancellation/timeouts
- retry budget
- structured events
- parent/child execution references
- idempotency strategy

**Gate BE-4:** failure injection demonstrates controlled retry/abort/finalization.

#### BE-5 MCP / Tool Bus
- tool registry
- schema validation
- permission check
- normalized invocation result
- telemetry/evidence hooks

**Gate BE-5:** allowed tool executes; denied/malformed tool invocation is blocked and recorded.

#### BE-6 Telemetry & Economics
- normalized tokens/cost/latency/status
- cost registry
- strategy metrics
- experiment record
- baseline economics evaluator

**Gate BE-6:** same workload can compare >=2 execution strategies reproducibly.

#### BE-7 Evidence Chain
- canonical serialization
- content commitments
- local hash chain
- mutation detection
- Merkle batch creation/verification

**Gate BE-7:** post-hoc mutation is detected and Merkle proof verifies.

#### BE-8 Quality Evaluation
- evaluator interface
- deterministic evaluator baseline
- model/human evaluator adapter interfaces
- quality record linked to run

**Gate BE-8:** strategy comparisons cannot report optimization without quality evidence.

#### BE-9 Optimization Loop v0
- baseline strategy registry
- historical metric query
- constrained recommendation
- policy-safe selection
- rollback metadata

**Gate BE-9:** optimized recommendation demonstrates measurable improvement without policy bypass.

### BACKEND RELEASE GATE — GATE-BE-R0

Backend R0 is accepted only when BE-0 through BE-9 pass as an integrated headless system.

Required demo:

```text
Task
 -> Policy
 -> Strategy candidates
 -> Routing
 -> Execution
 -> Tool invocation
 -> Telemetry
 -> Quality
 -> Evidence
 -> Economics comparison
 -> Recommended next strategy
```

No frontend production implementation begins before this gate.

---

## Frontend Lane — R0 Console

### FE-0 UI Contract Admission
- consume accepted backend API/contracts
- define frontend state model
- no backend contract invention

### FE-1 Task Console
- submit task
- show policy constraints
- show execution state

### FE-2 Execution Trace
- human-readable execution timeline
- agent/tool/model events
- errors/retries
- no hidden chain-of-thought requirement

### FE-3 Economics Dashboard
- tokens/cost/latency
- strategy comparison
- cache/model/tool economics

### FE-4 Evidence Viewer
- run/evidence identity
- hash-chain status
- Merkle verification result
- policy/execution-plan references

### FE-5 Policy Control Surface
- view/edit permitted policy fields
- validation errors
- human approval workflow baseline

### FRONTEND RELEASE GATE — GATE-FE-R0

Required:

- frontend builds reproducibly;
- accepted backend contracts are consumed without drift;
- critical error/loading/empty states exist;
- no secret/private payload is exposed by default;
- core user journey works against backend R0.

---

## Integration & Test Lane — R0

### INT-0 Contract Compatibility
- backend/frontend contract consistency
- schema/version mismatch handling

### INT-1 End-to-End Golden Flow
- task to final evidence/economics UI

### INT-2 Failure Matrix
Inject and verify:
- model timeout
- model provider failure
- tool failure
- malformed output
- policy rejection
- budget exhaustion
- retry exhaustion
- evidence write failure
- frontend reconnect/reload

### INT-3 Security Baseline
- secret scanning
- authorization boundary checks
- prompt/tool injection test cases
- unsafe tool invocation prevention
- local/private execution policy checks
- dependency scan baseline

### INT-4 Performance Baseline
Measure:
- routing overhead
- telemetry overhead
- evidence hashing overhead
- API latency
- sustained representative workload

### INT-5 Recovery & Determinism
- restart recovery behavior
- idempotent operations where required
- duplicate request handling
- evidence consistency

### SYSTEM RELEASE GATE — GATE-INT-R0

Integration must publish an explicit ACCEPT/REJECT report. Any P0 defect returns to Backend or Frontend owner; Integration does not hide architecture defects with local patches.

---

## GitHub / Release Lane — R0

### OPS-0 Repository Audit
- clean branch history
- no generated junk/secrets
- docs match implementation

### OPS-1 CI / Checks
- required build/test/lint/type/security commands

### OPS-2 Release Documentation
- README status
- architecture/version notes
- known limitations
- migration notes if applicable

### OPS-3 Release Candidate
- tag/version plan
- changelog
- acceptance evidence references

### RELEASE GATE — GATE-REL-R0

Only Integration-accepted state may be merged/released.

---

## R1 — Advanced Runtime

After R0:
- semantic cache
- working/episodic/SOP memory
- local RAG
- sandboxed code execution
- Planner/Executor/Reviewer strategies
- richer local-model execution
- deeper quality evaluators

## R2 — Enterprise Trust

- identity/attestation adapters
- private evidence synchronization
- multi-tenant governance
- optional L2 anchoring
- HITL/multi-signature controls
- enterprise policy packs

## R3 — Protocol & Research

- interoperable A2A governance
- Zero-Knowledge Compliance Proofs
- guarded auto-harness optimization
- executable Obsidian environment
- cross-workload learned policies

## Board Rule

A later release may be designed in advance but cannot become an implementation dependency of an earlier gate without Controller approval.

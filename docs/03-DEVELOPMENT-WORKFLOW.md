# Rasputin v7 — Development Workflow

> **Immutable execution order:** Controller/Architecture Gate → Backend → Frontend → Integration/Test/Red-Blue/Recovery → GitHub/Release.

## 1. Five-Role Operating Model

Rasputin uses five persistent development roles:

1. **Controller / 总控**
2. **Backend / 后端**
3. **Frontend / 前端**
4. **Integration, Test & Assurance / 整合、测试、红蓝与恢复验证**
5. **GitHub & Release / 上传与发布**

The Controller is always active. All implementation lanes are stage-gated.

## 2. Controller Loop

```text
READ CURRENT STATE
   ↓
CHECK ACTIVE ARCHITECTURE / CONTRACT GATE
   ↓
FREEZE SCOPE
   ↓
DISPATCH OWNER
   ↓
OWNER IMPLEMENTS
   ↓
OWNER RETURNS EVIDENCE
   ↓
TEST / FAILURE INJECTION / ASSURANCE AS REQUIRED
   ↓
CONTROLLER REVIEWS
   ↓
ACCEPT / REJECT / REWORK
   ↓
UPDATE PROJECT STATE
   ↓
UNLOCK NEXT LANE
```

The Controller owns strategic and contract decisions; implementation agents do not silently redefine them.

## 3. Architecture / Contract Gate

Before a release train can implement semantics, the active architecture and required contracts must be accepted.

For v7 migration this is `GATE-V7-R0`.

If a coding task discovers a strategic contradiction:

```text
STOP
 -> record conflict
 -> return to Controller
 -> update architecture/contracts
 -> re-run gate
 -> resume
```

No feature code may become the accidental source of truth.

## 4. Backend Stage

Backend receives:

- accepted architecture;
- frozen contracts for the active stage;
- exact work package;
- tests/gate conditions;
- explicit forbidden scope.

Backend returns:

```text
Summary
Changed files
API/schema changes
Capital / authority impact
Tests run
Failure cases
Security / recovery observations
Performance notes
Known limitations
Commit/branch state
Gate evidence
```

Backend cannot ask Frontend or Integration to compensate for unstable contracts or authority leaks.

## 5. Frontend Stage

Frontend begins only against accepted user-facing backend contracts.

Rules:

- backend contracts remain source of truth;
- mock data must conform to accepted schemas;
- distinguish measured, inferred, authorized and proven facts;
- expose allocation reason codes without inventing explanations;
- surface resource health, recovery and assurance state where relevant;
- never expose hidden chain-of-thought;
- design denied, deferred, exhausted-budget, quarantined and recovery states.

## 6. Integration, Test & Assurance Stage

Integration owns system behavior across components.

Required test families may include:

```text
contract compatibility
end-to-end workload / portfolio flows
budget concurrency
provider / tool / runtime failures
resource-state staleness
policy denial
risk / irreversibility exhaustion
recovery-budget exhaustion
quarantine
restarts / idempotency
telemetry/evidence corruption attempts
red-blue scenarios
controlled chaos
shadow-mode safety
frontend reconnect / reload
```

### Red-Blue Rule

Security-sensitive releases must include bounded adversarial scenarios targeting the relevant planes. Red-team components use explicit test authority and cannot inherit production privilege by default.

### Recovery Rule

Any feature claiming resilience must demonstrate:

```text
DETECT -> DIAGNOSE -> CONTAIN -> RECOVER -> VERIFY
```

and, where systemic, portfolio reallocation behavior.

Successful recovery does not erase failure evidence.

## 7. Benchmark Rule

Optimization, capital-allocation, recovery or safety claims require reproducible evidence.

Use as applicable:

- **RCB** — Rasputin Capital Benchmark;
- **RARB** — Rasputin Adversarial & Resilience Benchmark.

A benchmark result must include workload definition, baseline, allocator/policy versions, resource-state snapshot or reproducible fixture, raw metrics and known limitations.

## 8. GitHub / Release Stage

GitHub/Release begins only after the relevant system gate is accepted.

Responsibilities:

- repository hygiene;
- final diff audit;
- branch/PR management;
- CI/check status;
- documentation synchronization;
- migration notes;
- changelog/release notes;
- tags/releases when authorized;
- final main synchronization.

Release does not redesign architecture or hide known defects.

## 9. Branch / Worktree Pattern

Recommended pattern:

```text
main                               accepted state
feat/v7-*                          architecture / strategic migration
feat/r1-*                          executable contracts
feat/r2-*                          capital ledger / telemetry
feat/rN-*                          stage implementation
fix/integration-*                  integration/test repair
fix/assurance-*                    red-blue/recovery repair
ops/release-*                      release operations
```

Stage branches should start from the latest accepted main baseline unless Controller explicitly authorizes otherwise.

## 10. Codex / Coding-Agent Window Prompt

Every implementation window should read at minimum:

```text
README.md
docs/00-PROJECT-CONTROL.md
docs/01-MASTER-TECHNICAL-DESIGN.md
docs/02-DELIVERY-BOARD.md
docs/03-DEVELOPMENT-WORKFLOW.md
docs/04-PROJECT-STATE.md
active gate document
relevant contracts
active work package
role document
```

Before implementation it reports:

```text
understood scope
current branch/worktree
active gate and admission state
dependencies
planned files
planned tests
failure / security risks
contract questions
```

## 11. No-Drift Rule

No implementation agent may silently:

- widen policy;
- change a hard budget semantic;
- collapse CapitalAllocation into routing;
- convert Recovery into unbounded retry;
- treat Multi-Agent as mandatory architecture;
- add provider-specific fields to canonical contracts outside extensions;
- weaken evidence strength labels;
- remove failure history after recovery.

Any such need returns to Controller.

## 12. Strong-System Rule

A major subsystem is strong only when it has:

```text
contract
implementation
tests
failure handling
authority boundary
capital / cost accounting
observability
evidence
security / assurance coverage
recovery behavior where applicable
performance understanding
documentation
integration proof
```

Rasputin's power must come from reliable depth, not feature count.

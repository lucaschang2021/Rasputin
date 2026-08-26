# Rasputin — Development Workflow

> **Immutable execution order:** Backend → Frontend → Integration/Test → GitHub/Release.

## 1. Five-Role Operating Model

Rasputin uses five persistent development roles:

1. **Controller / 总控**
2. **Backend / 后端**
3. **Frontend / 前端**
4. **Integration & Test / 前后端整合与检测修复**
5. **GitHub & Release / 上传与发布**

The Controller is always active. The other four lanes are stage-gated.

## 2. Controller Loop

For each work package:

```text
READ CURRENT STATE
   ↓
FREEZE SCOPE
   ↓
DISPATCH OWNER
   ↓
OWNER IMPLEMENTS
   ↓
OWNER RETURNS EVIDENCE
   ↓
CONTROLLER REVIEWS
   ↓
ACCEPT / REJECT / REWORK
   ↓
UPDATE PROJECT STATE
   ↓
UNLOCK NEXT LANE
```

The Controller does not casually edit implementation while reviewing. It should preserve role separation and use evidence to make decisions.

## 3. Backend Stage

Backend receives:

- accepted architecture;
- frozen contracts;
- exact work package;
- tests/gate conditions;
- explicit forbidden scope.

Backend returns:

```text
Summary
Changed files
API/schema changes
Tests run
Results
Performance notes
Security notes
Known limitations
Commit/branch state
Gate evidence
```

Backend may not ask Frontend to compensate for unstable contracts.

### Backend completion rule

Backend stage is not complete when individual modules pass. It is complete when the **headless system path** works end-to-end and `GATE-BE-*` is accepted.

## 4. Frontend Stage

Frontend starts only against an accepted backend baseline.

Frontend rules:

- treat backend contracts as source of truth;
- no fake endpoint shapes that later become de facto backend requirements;
- mock data must conform to accepted schemas;
- all loading/error/denied/timeout states are designed;
- do not expose raw hidden reasoning traces;
- economics/evidence displays must distinguish measured facts from estimates.

Frontend returns the same evidence structure plus screenshots or interaction proof where useful.

## 5. Integration & Test Stage

Integration owns the whole system rather than one code area.

Responsibilities:

- merge/assemble accepted backend and frontend states;
- run contract tests;
- run E2E flows;
- inject failures;
- identify ownership of defects;
- repair only genuine integration glue locally;
- route backend defects back to Backend;
- route frontend defects back to Frontend;
- repeat until system gate passes.

Integration must test not only the happy path but:

```text
provider failure
network timeout
tool failure
policy denial
budget exhaustion
bad schema
retries
restart/recovery
duplicate requests
evidence corruption attempts
frontend disconnect/reload
```

## 6. GitHub / Release Stage

GitHub/Release begins after Integration ACCEPT.

Responsibilities:

- repository hygiene;
- final diff audit;
- branch/PR management;
- CI status;
- documentation synchronization;
- changelog/release notes;
- tags/releases when authorized;
- final main synchronization.

GitHub role does not redesign features and does not merge known P0 defects.

## 7. Branch / Worktree Pattern

Recommended pattern, matching the proven isolated workflow:

```text
Rasputin/                    main
Rasputin-wt/backend/         feat/be-<release>
Rasputin-wt/frontend/        feat/fe-<release>
Rasputin-wt/integration/     fix/integration-<release>
Rasputin-wt/github/          ops/github-<release>
```

Controller can operate from main/docs and review all lanes.

Suggested branch lifecycle:

```text
main
  ↓ branch
feat/be-r0
  ↓ accepted + merged
main
  ↓ sync frontend base
feat/fe-r0
  ↓ accepted + merged
main
  ↓ integration branch
fix/integration-r0
  ↓ accepted + merged
main
  ↓ release audit
ops/github-r0
  ↓ final release
main
```

This serial merge discipline intentionally prioritizes correctness over maximum parallelism.

## 8. Codex Window Prompts

Each Codex window should begin by reading:

```text
README.md
docs/00-PROJECT-CONTROL.md
docs/01-MASTER-TECHNICAL-DESIGN.md
docs/02-DELIVERY-BOARD.md
docs/03-DEVELOPMENT-WORKFLOW.md
relevant contracts
its role document
current admission/work-package document
```

Then it must report:

```text
understood scope
current branch/worktree
dependencies
planned files
planned tests
risks
```

before implementation.

## 9. No-Drift Rule

If implementation discovers a contract/architecture problem:

1. stop the affected change;
2. record the conflict;
3. return to Controller;
4. Controller issues an architecture decision;
5. update docs/contracts;
6. resume implementation.

Do not silently evolve contracts inside feature code.

## 10. Strong-System Rule

Rasputin's power must come from reliable capabilities, not demos.

A feature is considered strong only when it has:

```text
contract
implementation
tests
failure handling
observability
security boundary
performance understanding
documentation
integration proof
```

This is the standard for every important subsystem.

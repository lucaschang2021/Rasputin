# Backend Role — Rasputin

## Mission
Build the headless Rasputin kernel first and make every core capability contract-driven, observable, testable and failure-aware.

## Owns
- contracts and runtime implementations after Controller approval
- policy engine
- routing/gateway
- execution supervisor
- MCP/tool bus
- telemetry/economics
- evidence chain
- quality/evaluation
- optimization loop
- backend APIs/SDK/CLI boundaries

## Must not
- redesign product scope without Controller decision
- invent frontend-specific API shortcuts
- bypass policy for convenience
- hide provider-specific behavior inside core contracts
- mark a task complete without tests and evidence

## Required return format
```text
Task ID
Summary
Changed files
Contract/API impact
Tests run + results
Failure cases covered
Performance notes
Security notes
Known limitations
Recommended next action
```

## Backend Gate
The backend release must demonstrate the full headless chain:

```text
Task -> Policy -> Plan -> Route -> Execute -> Tool -> Telemetry -> Quality -> Evidence -> Economics -> Optimization
```

Frontend remains blocked until Controller accepts this gate.

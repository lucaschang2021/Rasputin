# Integration & Test Role — Rasputin

## Mission
Prove the assembled system works under normal, degraded and adversarial conditions before release.

## Entry condition
Backend and Frontend release gates must both be accepted.

## Owns
- backend/frontend contract compatibility
- end-to-end system assembly
- regression suites
- failure injection
- performance baseline
- security baseline
- restart/recovery behavior
- defect ownership routing
- final system ACCEPT / REJECT recommendation

## Failure Matrix
At minimum test:

```text
model timeout
model provider outage
invalid model output
tool timeout/failure
policy rejection
budget exhaustion
retry exhaustion
schema mismatch
evidence mutation/corruption
storage failure
frontend disconnect/reload
restart during active work
duplicate request
```

## Repair rule
Integration may repair integration glue. Architecture/backend defects return to Backend; frontend defects return to Frontend. Do not conceal structural problems with brittle local patches.

## Acceptance output
```text
System version
Integrated commits
Test matrix
Pass/fail counts
Performance results
Security results
Known limitations
Open defects by severity
ACCEPT / REJECT
```

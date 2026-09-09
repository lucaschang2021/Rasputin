# Integration, Test & Assurance Role — Rasputin v7

## Mission

Prove the assembled system works under normal, degraded, adversarial and recovery conditions before release.

## Entry condition

The backend/frontend components under test must have passed their prerequisite gates. A headless stage may be integration-tested before a frontend exists when the roadmap explicitly allows it.

## Owns

- contract compatibility;
- end-to-end portfolio/workload assembly;
- budget and ledger consistency tests;
- regression suites;
- failure injection and controlled chaos;
- Red-Blue adversarial scenarios;
- recovery and quarantine verification;
- performance baseline;
- security / authority baseline;
- restart / idempotency behavior;
- evidence-integrity tests;
- RCB / RARB execution where applicable;
- defect ownership routing;
- final system ACCEPT / REJECT recommendation.

## Minimum Failure / Adversarial Matrix

```text
provider timeout / outage / degradation
quota exhaustion
stale ResourceState
invalid model output
tool timeout / malformed result
policy rejection
hard budget exhaustion
risk / irreversibility exhaustion
recovery budget exhaustion
policy-unsafe fallback
quarantined resource selection attempt
prompt / tool injection
allocator value / urgency / scarcity manipulation
poisoned context / memory
verifier disagreement / manipulation
telemetry or outcome integrity failure
schema mismatch
evidence mutation / corruption
storage / telemetry sink failure
restart during active work
duplicate request
frontend disconnect / reload
```

## Red-Blue Rule

Red-team execution must use explicit bounded test authority. It may not inherit broader production permissions by default. Any forbidden unauthorized or irreversible effect is a failed assurance result.

## Recovery Rule

A resilience claim requires evidence for:

```text
DETECT
 -> DIAGNOSE
 -> CONTAIN
 -> RECOVER
 -> VERIFY
```

and, for systemic incidents, the emitted portfolio reallocation request or reason why reallocation was unnecessary.

Successful recovery never erases the original FailureRecord.

## Repair Rule

Integration may repair genuine integration glue. Architecture, contract, backend, frontend, allocator or authority defects return to the owning lane. Do not conceal structural problems with brittle local patches.

## Acceptance Output

```text
System / Stage Version
Integrated Commits
Contract Matrix
Test Matrix
Pass / Fail Counts
Failure Injection Results
Red-Blue / RARB Results if applicable
Recovery Results
RCB Results if applicable
Performance Results
Security / Authority Results
Known Limitations
Open Defects by Severity
ACCEPT / REJECT Recommendation
```

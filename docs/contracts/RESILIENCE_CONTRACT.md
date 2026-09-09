# Rasputin v7 — Adversarial Assurance & Adaptive Recovery Contract

> **Status:** R0 MIGRATION DRAFT  
> **Contract ID:** V7-CONTRACT-RESILIENCE  
> **Version:** 1.0.0-alpha

## 1. Purpose

Defines the canonical semantics for Red-Blue adversarial assurance, controlled failure injection, bounded containment, adaptive recovery, post-recovery verification and learning.

Red-Blue and Recovery are permanent cross-cutting control loops, not optional plugins.

## 2. Recovery State Machine

```text
NORMAL
  -> DETECT
  -> DIAGNOSE
  -> CONTAIN
  -> RECOVER
  -> VERIFY
  -> REALLOCATE
  -> LEARN
  -> CLOSED
```

A transition may terminate at `ABORTED` or `HUMAN_ESCALATION` when no admissible automated recovery remains.

## 3. Failure Taxonomy

At minimum:

```text
provider_unavailable
provider_degraded
model_degraded
runtime_failure
tool_failure
malformed_output
policy_violation
budget_exhaustion
quota_exhaustion
latency_degradation
quality_failure
verifier_disagreement
memory_corruption
context_poisoning
resource_identity_failure
telemetry_integrity_failure
security_incident
outcome_failure
unknown
```

## 4. FailureRecord

```yaml
schema_version: "1.0.0"
failure_id: "fail_..."
run_id: "run_..."
workload_id: "wl_..."
detected_at: "..."
failure_class: "..."
severity: "low|medium|high|critical"
detector_ref: "..."
suspected_causes: []
resource_refs: []
blast_radius_refs: []
policy_impact: null
budget_impact: null
security_impact: null
evidence_refs: []
extensions: {}
```

## 5. RecoveryPolicy

```yaml
schema_version: "1.0.0"
recovery_policy_id: "recpol_..."
version: "..."
allowed_actions:
  - retry
  - reroute
  - substitute_resource
  - restore_checkpoint
  - rollback_memory
  - reduce_privilege
  - escalate_verification
  - human_escalation
  - defer
  - abort
retry_ceiling: 0
recovery_budget_ref: null
max_additional_risk: null
max_additional_irreversibility: null
require_post_recovery_verification: true
extensions: {}
```

## 6. RecoveryEpisode

```yaml
schema_version: "1.0.0"
recovery_id: "rec_..."
failure_id: "fail_..."
run_id: "run_..."
workload_id: "wl_..."
started_at: "..."
ended_at: null
state: "detect|diagnose|contain|recover|verify|reallocate|learn|closed"
actions: []
resource_quarantine_refs: []
new_plan_id: null
recovery_budget_ref: null
cost_consumed: null
risk_consumed: null
irreversibility_consumed: null
portfolio_reallocation_ref: null
result: "recovered|degraded|aborted|escalated|failed|pending"
verification_refs: []
evidence_refs: []
extensions: {}
```

## 7. Economic Recovery Rule

Automated recovery may continue only while all of the following remain true:

```text
recovery action is authorized
recovery budget remains
risk / irreversibility limits remain
expected remaining value justifies recovery cost
post-recovery verification can satisfy policy
```

If any hard condition fails, automated recovery stops.

## 8. Resource Quarantine

Quarantine is a first-class resource state transition.

```yaml
resource_id: "res_..."
state: "quarantined"
reason_code: "..."
started_at: "..."
release_requires: []
evidence_refs: []
```

Quarantined resources cannot be selected by allocator, strategy compiler, fallback or recovery until explicitly released.

## 9. Portfolio-Level Reallocation

Systemic failures may invalidate many queued/planned workloads.

Examples:

- provider outage;
- quota shock;
- compromised MCP service;
- verifier fleet failure;
- shared runtime degradation.

The recovery engine MAY emit a portfolio reallocation request that updates ResourceState and triggers a new allocator decision for affected workloads.

## 10. Red-Blue Scenario

```yaml
schema_version: "1.0.0"
scenario_id: "scenario_..."
name: "..."
mode: "shadow|controlled_chaos|staging|authorized_production"
attack_class: "..."
target_planes: []
preconditions: []
attack_steps: []
expected_blue_controls: []
forbidden_effects: []
test_authority_ref: "..."
stop_conditions: []
extensions: {}
```

## 11. Attack Classes

At minimum:

```text
allocator_value_manipulation
fake_urgency
fake_scarcity_or_price
policy_bypass
prompt_injection
tool_injection
poisoned_context
poisoned_memory
resource_impersonation
verifier_manipulation
telemetry_manipulation
outcome_manipulation
quota_shock
latency_shock
provider_outage
recovery_abuse
cross_agent_authority_confusion
```

## 12. Blue Controls

Potential responses:

```text
deny
require_human_approval
tighten_policy
reduce_budget
reduce_privilege
quarantine_resource
revoke_capability
sanitize_context
rollback_memory
increase_verification
substitute_resource
block_egress
rate_limit
cancel_run
terminate_children
```

## 13. AssuranceResult

```yaml
schema_version: "1.0.0"
assurance_result_id: "assure_..."
scenario_id: "scenario_..."
started_at: "..."
ended_at: "..."
attack_detected: null
bypass_detected: false
unauthorized_effect: false
irreversible_effect: false
blue_controls_observed: []
recovery_refs: []
blast_radius_refs: []
metrics:
  detection_latency_ms: null
  recovery_latency_ms: null
  recovery_cost: null
  portfolio_utility_delta: null
  risk_consumed: null
  irreversibility_consumed: null
verdict: "pass|fail|inconclusive"
evidence_refs: []
extensions: {}
```

## 14. Shadow Mode

Shadow execution may evaluate strategy / defense alternatives without producing external side effects.

A shadow run MUST be clearly labeled and must not silently call irreversible production tools.

## 15. Controlled Chaos

Allowed bounded injections may include:

```text
provider unavailable
provider slow
quota exhausted
tool timeout
tool malformed response
stale resource state
verifier failure
telemetry sink unavailable
memory read failure
partial result
```

Chaos tests require explicit test scope and stop conditions.

## 16. Safety Invariants

1. Red-team components do not receive production privilege by default.
2. Test authority is explicit and narrower than or equal to production authority.
3. Recovery cannot widen policy.
4. Recovery cannot exceed Recovery Budget.
5. Quarantined resources cannot re-enter execution automatically.
6. Failure history is append-only and cannot be hidden by successful recovery.
7. An assurance scenario fails if it causes forbidden unauthorized/irreversible effects.
8. Chaos experiments must be bounded by explicit blast-radius constraints.
9. Post-recovery verification is mandatory when policy requires it.
10. Portfolio reallocation is an allocator decision, not an implicit side effect of the recovery engine.

## 17. RARB Metrics

The Rasputin Adversarial & Resilience Benchmark may include:

```text
Attack Detection Rate
False Positive Rate
Policy Bypass Rate
Unauthorized Action Rate
MTTD
MTTR
Recovery Success Rate
Recovery Economic Cost
Blast Radius
Portfolio Utility Under Failure
Portfolio Utility Under Attack
Quarantine Success Rate
Rollback Integrity
Post-Recovery Quality
Capital Reallocation Efficiency
```

## 18. Required Tests

- bounded retry terminates at ceiling;
- recovery budget exhaustion blocks further automated action;
- policy-safe reroute succeeds;
- policy-unsafe fallback is denied;
- quarantine blocks selection;
- provider outage triggers portfolio reallocation request;
- successful recovery preserves original failure evidence;
- red scenario cannot exceed test authority;
- shadow mode cannot produce irreversible production effect;
- assurance result records detection/recovery metrics deterministically.

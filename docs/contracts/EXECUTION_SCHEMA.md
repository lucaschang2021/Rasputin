# Rasputin v7 — Canonical Workload / Execution Contract

> **Status:** R0 MIGRATION DRAFT  
> **Contract ID:** V7-CONTRACT-EXECUTION  
> **Version:** 1.0.0-alpha

## 1. Purpose

Defines provider-independent canonical objects connecting portfolio intake, authority, capital allocation, execution, telemetry, failure, recovery, outcome, evidence and learning.

No runtime may introduce a parallel semantic execution model without an explicit architecture decision.

## 2. Design Rules

1. Every schema has explicit `schema_version`.
2. IDs are stable and globally unique within a deployment.
3. Provider-specific data lives under `extensions`.
4. Sensitive payloads should be references or commitments where practical.
5. Monetary values use explicit currency and implementation MUST avoid economically material floating-point ambiguity.
6. Timestamps use UTC RFC 3339.
7. Finalized immutable records are append-only; corrections create successor records.
8. Every material execution is attributable to a PolicyDecision, CapitalAllocation and ExecutionPlan.
9. Every recovery action is attributable to a RecoveryEpisode and remains policy-safe.
10. Unknown major versions fail explicitly.

## 3. Canonical Object Graph

```text
Principal
  -> Portfolio
      -> Workload[*]
          -> PolicyDecision
          -> CapitalAllocation
          -> ExecutionPlan
          -> Run[*]
              +-> TelemetryRecord[*]
              +-> FailureRecord[*]
              +-> RecoveryEpisode[*]
              +-> QualityEvaluation[*]
              +-> OutcomeRecord[*]
              +-> EvidenceRecord[*]
  -> BudgetLedger[*]
  -> ResourceState[*]
```

## 4. Portfolio

```yaml
schema_version: "1.0.0"
portfolio_id: "port_..."
principal_ref: "principal_..."
created_at: "..."
name: "string"
objective: "string|null"
shared_budget_refs: []
policy_refs: []
workload_ids: []
priority_model_ref: null
metadata: {}
extensions: {}
```

A portfolio is the resource competition domain. Shared budgets and scarcity may apply across all member workloads.

## 5. Workload

```yaml
schema_version: "1.0.0"
workload_id: "wl_..."
portfolio_id: "port_..."
principal_ref: "principal_..."
created_at: "..."
objective: "string"
input_refs: []
requested_capabilities: []
value:
  expected: null
  unit: null
  value_model_ref: null
  uncertainty: null
priority: null
deadline_at: null
dependencies: []
constraints:
  budget_envelope_refs: []
  quality:
    min_score: null
    evaluator_ref: null
  risk_level: "low|medium|high|critical"
  privacy_level: "public|internal|confidential|restricted"
  irreversibility_level: "none|low|medium|high|critical"
  verification_level: "none|basic|enhanced|attested|zk"
  timeout_ms: null
admission_state: "pending|admitted|deferred|rejected|cancelled|completed"
metadata: {}
extensions: {}
```

`objective` states desired outcome, not implementation.

## 6. Resource

```yaml
schema_version: "1.0.0"
resource_id: "res_..."
resource_type: "model|agent|harness|tool|memory|retriever|verifier|human|runtime|compute|quota|router|other"
provider_ref: null
capabilities: []
privacy_class: null
risk_class: null
verification_support: []
metadata: {}
extensions: {}
```

## 7. ResourceState

```yaml
schema_version: "1.0.0"
resource_state_id: "rs_..."
resource_id: "res_..."
observed_at: "..."
availability: "available|degraded|unavailable|quarantined"
health_score: null
quota_remaining: null
quota_unit: null
nominal_price: null
currency: null
latency_estimate_ms: null
failure_rate: null
shadow_price:
  effective: null
  components: {}
attestation_ref: null
metadata: {}
extensions: {}
```

ResourceState is time-dependent. A plan selected under stale state MAY require revalidation before execution.

## 8. CapitalAllocation

```yaml
schema_version: "1.0.0"
allocation_id: "alloc_..."
portfolio_id: "port_..."
workload_id: "wl_..."
policy_decision_id: "poldec_..."
created_at: "..."
decision: "execute|defer|do_not_execute|wait_for_information|require_human_approval"
allocator_id: "..."
allocator_version: "..."
resource_state_refs: []
allocated_budget_refs: []
expected:
  outcome_value: null
  effective_cost: null
  risk_adjusted_utility: null
selection:
  strategy_class: null
  score: null
  rationale_codes: []
  uncertainty: null
allocation_hash: "sha256:..."
extensions: {}
```

Allocation is the explicit economic admission decision. `execute` is not assumed by default.

## 9. ExecutionPlan

```yaml
schema_version: "1.0.0"
execution_plan_id: "plan_..."
workload_id: "wl_..."
allocation_id: "alloc_..."
policy_decision_id: "poldec_..."
created_at: "..."
strategy:
  venue_ref: null
  model_ref: null
  agent_topology: null
  harness_ref: null
  tool_refs: []
  memory:
    mode: "none|read|read_write"
    refs: []
  compute:
    runtime_ref: null
    reasoning_effort: null
    sampling_budget: null
  verification:
    level: "basic"
    mechanism_refs: []
  recovery_policy_ref: null
fallbacks: []
expected:
  nominal_cost: null
  effective_cost: null
  latency_ms: null
  quality_score: null
  outcome_value: null
plan_hash: "sha256:..."
extensions: {}
```

Fallbacks remain inside the same or stricter authority and budget envelope unless a new explicit decision is produced.

## 10. Run

```yaml
schema_version: "1.0.0"
run_id: "run_..."
workload_id: "wl_..."
execution_plan_id: "plan_..."
allocation_id: "alloc_..."
parent_run_id: null
started_at: "..."
ended_at: null
status: "queued|running|succeeded|failed|cancelled|blocked|recovering|quarantined"
observed_resource_state_refs: []
result_ref: null
error:
  type: null
  code: null
  retryable: null
finalization:
  finalized_at: null
  final_record_hash: null
extensions: {}
```

## 11. TelemetryRecord

```yaml
schema_version: "1.0.0"
telemetry_id: "tel_..."
run_id: "run_..."
observed_at: "..."
type: "model_call|tool_call|runtime|ledger|quality|security|recovery|custom"
metrics:
  tokens_in: null
  tokens_out: null
  estimated_money_cost: null
  effective_cost: null
  latency_ms: null
  retry_count: 0
  success: null
  risk_consumed: null
  irreversibility_consumed: null
  recovery_cost: null
dimensions: {}
source:
  adapter_id: "..."
  adapter_version: "..."
extensions: {}
```

## 12. FailureRecord

```yaml
schema_version: "1.0.0"
failure_id: "fail_..."
run_id: "run_..."
detected_at: "..."
failure_class: "provider_unavailable|model_degraded|tool_failure|runtime_failure|policy_violation|quality_failure|verifier_disagreement|memory_corruption|context_poisoning|quota_exhaustion|latency_degradation|security_incident|outcome_failure|unknown"
severity: "low|medium|high|critical"
suspected_causes: []
resource_refs: []
blast_radius_refs: []
evidence_refs: []
extensions: {}
```

## 13. RecoveryEpisode

```yaml
schema_version: "1.0.0"
recovery_id: "rec_..."
failure_id: "fail_..."
run_id: "run_..."
started_at: "..."
ended_at: null
state: "detect|diagnose|contain|recover|verify|reallocate|learn|closed"
actions: []
recovery_budget_ref: null
cost_consumed: null
result: "recovered|degraded|aborted|escalated|failed|pending"
new_plan_id: null
portfolio_reallocation_ref: null
verification_refs: []
extensions: {}
```

A recovery plan MUST NOT widen policy authority by itself.

## 14. QualityEvaluation

```yaml
schema_version: "1.0.0"
quality_evaluation_id: "qual_..."
run_id: "run_..."
evaluator_ref: "..."
created_at: "..."
score: null
scale: {min: 0, max: 1}
passed: null
signals: {}
evidence_refs: []
extensions: {}
```

A model-generated confidence score is not ground truth.

## 15. OutcomeRecord

```yaml
schema_version: "1.0.0"
outcome_id: "out_..."
workload_id: "wl_..."
run_refs: []
observed_at: "..."
technical_success: null
task_success: null
workflow_outcome: null
downstream_event_refs: []
realized_value:
  amount: null
  unit: null
risk_adjustment: null
attribution_confidence: null
source_refs: []
extensions: {}
```

OutcomeRecord MAY be appended long after Run finalization.

## 16. Canonical Final Reconstruction

A finalized workload history MUST permit reconstruction of:

```text
what outcome was requested
what authority governed it
why capital was or was not allocated
which resources were selected
what actually executed
what it cost nominally and effectively
what failed / recovered
what risk / irreversibility was consumed
how quality was evaluated
what downstream outcome occurred
what evidence supports the record
```

## 17. Migration from v6

```text
v6 Task              -> v7 Workload
v6 ExecutionPlan     -> v7 ExecutionPlan + CapitalAllocation
v6 Run               -> v7 Run
v6 TelemetryRecord   -> v7 TelemetryRecord
v6 QualityEvaluation -> v7 QualityEvaluation
v6 evidence refs     -> retained
```

New required v7 concepts are Portfolio, ResourceState, BudgetLedger, CapitalAllocation, FailureRecord, RecoveryEpisode and OutcomeRecord.

## 18. R1 Acceptance Fixtures

At minimum:

1. portfolio with competing workloads;
2. execute decision;
3. do-not-execute decision;
4. deferred workload due to scarce quota;
5. allowed cloud execution;
6. local/private execution;
7. denied-by-policy workload;
8. failed run with bounded recovery;
9. quarantined resource and reallocation;
10. delayed business outcome attached after finalization.

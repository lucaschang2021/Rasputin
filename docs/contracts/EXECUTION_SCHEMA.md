# Rasputin CORE-0 — Canonical Execution Schema Contract

> Status: PRE-DEVELOPMENT / DRAFT FOR GATE-CORE-0  
> Contract ID: CORE-0-CONTRACT-EXECUTION  
> Version: 0.1.0-alpha

## 1. Purpose

This contract defines the provider-independent canonical objects that connect Task intake, Policy evaluation, Economics routing, Execution, Telemetry, Evidence and Optimization.

No runtime implementation may introduce a parallel execution schema without an explicit architecture decision.

## 2. Design Rules

1. IDs are globally unique within a Rasputin deployment.
2. Provider-specific payloads live under extension namespaces; they do not replace canonical fields.
3. Sensitive payloads SHOULD be referenced by content-addressed hashes or secure references rather than duplicated.
4. Every material decision MUST be attributable to a policy version and execution plan.
5. Every schema has an explicit `schema_version`.
6. Timestamps use UTC RFC 3339.
7. Monetary amounts include currency.
8. Immutable finalized records MUST NOT be edited in place; corrections create a successor record.

## 3. Canonical Object Graph

```text
Task
  |
  v
PolicyDecision
  |
  v
ExecutionPlan
  |
  v
Run
  +--> TelemetryRecord[*]
  +--> EvidenceRecord[*]
  +--> QualityEvaluation[*]
```

## 4. Task

Minimum canonical fields:

```yaml
schema_version: "0.1.0"
task_id: "task_..."
created_at: "2026-08-26T00:00:00Z"
objective: "string"
input_refs: []
requested_capabilities: []
constraints:
  budget:
    max_amount: 0.0
    currency: "USD"
  quality:
    min_score: null
    evaluator: null
  risk_level: "low|medium|high|critical"
  privacy_level: "public|internal|confidential|restricted"
  verification_level: "none|basic|enhanced|attested|zk"
  timeout_ms: null
metadata: {}
extensions: {}
```

Semantics:

- `objective` describes desired outcome, not implementation.
- `input_refs` point to payloads, documents, data or context.
- `requested_capabilities` describe capability needs such as `web.search`, `code.python`, `finance.market_data`.
- constraints are declarative and MUST NOT encode provider-specific logic.

## 5. PolicyDecision

```yaml
schema_version: "0.1.0"
policy_decision_id: "poldec_..."
task_id: "task_..."
policy_id: "policy_..."
policy_version: "1.0.0"
decided_at: "..."
result: "allow|deny|allow_with_conditions|require_human_approval"
allowed_models: []
allowed_tools: []
allowed_harnesses: []
required_controls: []
normalized_constraints: {}
reason_codes: []
policy_hash: "sha256:..."
extensions: {}
```

Rules:

- Policy is evaluated before final routing.
- A denied task MUST NOT reach execution.
- `reason_codes` are machine-readable.
- Final evidence MUST reference `policy_decision_id` and `policy_hash`.

## 6. ExecutionPlan

```yaml
schema_version: "0.1.0"
execution_plan_id: "plan_..."
task_id: "task_..."
policy_decision_id: "poldec_..."
created_at: "..."
strategy:
  model:
    provider: "..."
    model_id: "..."
  agent: null
  harness:
    harness_id: "..."
    harness_version: "..."
  tools: []
  memory:
    mode: "none|read|read_write"
    refs: []
  compute:
    target: "local|cloud|hybrid"
    runtime_id: null
  verification:
    level: "basic"
    mechanism: []
expected:
  cost:
    amount: null
    currency: "USD"
  latency_ms: null
  quality_score: null
fallbacks: []
selection:
  strategy_id: "..."
  selector_version: "..."
  score: null
  rationale_codes: []
plan_hash: "sha256:..."
extensions: {}
```

Rules:

- An execution plan is a concrete allocation decision.
- Fallbacks MUST remain inside the allowed policy space.
- Changing model, harness, tool set or verification level after execution starts creates a new plan revision or child run.

## 7. Run

```yaml
schema_version: "0.1.0"
run_id: "run_..."
task_id: "task_..."
execution_plan_id: "plan_..."
parent_run_id: null
started_at: "..."
ended_at: null
status: "queued|running|succeeded|failed|cancelled|blocked"
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

## 8. TelemetryRecord

Telemetry records are append-only measurements.

```yaml
schema_version: "0.1.0"
telemetry_id: "tel_..."
run_id: "run_..."
observed_at: "..."
type: "model_call|tool_call|cache|runtime|quality|custom"
metrics:
  tokens_in: null
  tokens_out: null
  cached_tokens: null
  estimated_cost:
    amount: null
    currency: "USD"
  latency_ms: null
  retry_count: 0
  cache_hit: null
  success: null
dimensions: {}
source:
  adapter_id: "..."
  adapter_version: "..."
extensions: {}
```

## 9. QualityEvaluation

```yaml
schema_version: "0.1.0"
quality_evaluation_id: "qual_..."
run_id: "run_..."
evaluator_id: "..."
evaluator_version: "..."
created_at: "..."
score: null
scale:
  min: 0
  max: 1
passed: null
signals: {}
evidence_refs: []
extensions: {}
```

Quality signals MUST identify their evaluator. Rasputin MUST NOT treat a model-generated confidence score as ground truth.

## 10. Canonical Final Run Summary

A finalized run MUST permit reconstruction of:

```text
what task was requested
which policy governed it
which strategy was selected
what actually executed
what it cost
how long it took
whether it succeeded
how quality was evaluated
what evidence proves the record was not silently changed
```

## 11. Versioning

- Additive optional fields: minor version.
- New required fields or changed semantics: major version.
- Clarifications with no serialized impact: patch version.
- Readers SHOULD reject unknown major versions.
- Writers MUST write exactly one schema version per canonical object.

## 12. CORE-1 Acceptance Fixtures

CORE-1 implementation MUST include at least:

1. simple cloud model run;
2. local-model run;
3. tool-using run;
4. denied-by-policy task;
5. budget-constrained fallback run;
6. failed run with retry;
7. finalized run with evidence references.

These fixtures are required before `GATE-CORE-1` can pass.

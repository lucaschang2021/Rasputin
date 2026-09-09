# Rasputin v7 — Authority & Policy Contract

> **Status:** R0 MIGRATION DRAFT  
> **Contract ID:** V7-CONTRACT-AUTHORITY  
> **Version:** 1.0.0-alpha

## 1. Purpose

The Authority & Policy Plane defines the admissible execution space before capital allocation and remains authoritative throughout execution and recovery.

It is not a recommendation engine.

## 2. Inputs

```text
Principal / Tenant Identity
Portfolio / Workload
Tenant / Workspace Policy
Environment Policy
Data Classification
Resource State
Budget State
Risk / Irreversibility State
Human Approval State
Runtime Context
```

## 3. Outputs

```text
PolicyDecision
AuthorityEnvelope
Normalized Constraints
Allowed Resource Set
Required Controls
Budget Ceilings
Approval Requirement
Reason Codes
```

## 4. Policy Domains

v7 domains include:

```text
money / compute / quota budget
model / resource allow-deny
tool / capability allow-deny
harness / runtime allow-deny
privacy / data classification
data egress / locality
verification minimum
latency / timeout
retry ceiling
recovery ceiling
risk budget
irreversibility budget
human attention / approval
identity assurance
quarantine constraints
```

Future domains may include jurisdiction, segregation of duties, regulatory profiles and inter-org contract constraints.

## 5. AuthorityEnvelope

```yaml
schema_version: "1.0.0"
authority_envelope_id: "auth_..."
workload_id: "wl_..."
policy_decision_id: "poldec_..."
principal_ref: "principal_..."
created_at: "..."
valid_until: null
allowed_resources: []
denied_resources: []
allowed_capabilities: []
denied_capabilities: []
required_controls: []
budget_limits:
  money: null
  compute: null
  quota: null
  latency: null
  verification: null
  human_attention: null
  risk: null
  irreversibility: null
  recovery: null
approval_requirement: null
data_rules: {}
recovery_rules: {}
authority_hash: "sha256:..."
extensions: {}
```

## 6. PolicyDecision

```yaml
schema_version: "1.0.0"
policy_decision_id: "poldec_..."
workload_id: "wl_..."
policy_id: "policy_..."
policy_version: "..."
decided_at: "..."
result: "allow|deny|allow_with_conditions|require_human_approval"
authority_envelope_id: "auth_..."
reason_codes: []
policy_hash: "sha256:..."
extensions: {}
```

## 7. Evaluation Order

Default order:

```text
1. Validate workload / identity
2. Apply hard deny rules
3. Apply data / privacy / locality restrictions
4. Apply capability / resource allowlists
5. Apply monetary / compute / quota limits
6. Apply risk / irreversibility limits
7. Apply verification requirements
8. Apply retry / recovery ceilings
9. Determine human approval requirement
10. Normalize constraints
11. Emit PolicyDecision + AuthorityEnvelope
```

Hard constraints dominate economic optimization.

## 8. Budget Semantics

Budgets are authority limits, not merely accounting targets.

If a budget is hard, exhaustion MUST block additional consumption unless a new authorized budget artifact is produced.

Applicable scopes may include:

```text
principal
tenant
portfolio
workload
run
resource
recovery episode
```

More restrictive overlapping hard budgets dominate.

## 9. Risk and Irreversibility

`risk` and `irreversibility` are distinct.

- **Risk Budget** captures bounded uncertain loss exposure.
- **Irreversibility Budget** captures actions whose effects cannot be cheaply or reliably rolled back.

An individually permitted action MUST still be denied if cumulative shared portfolio/tenant irreversibility would exceed the authorized limit.

## 10. Recovery Authority

Recovery does not create new authority.

Rules:

1. retry must remain inside retry and recovery budgets;
2. alternate model/tool/harness must be inside the AuthorityEnvelope;
3. privilege escalation requires a new approval or policy decision;
4. degraded quality may occur only if policy explicitly permits a lower floor;
5. resource quarantine may make an existing plan invalid;
6. if no admissible recovery remains, the run must abort, defer or escalate.

## 11. Human Approval Contract

Approval is first-class:

```yaml
schema_version: "1.0.0"
approval_id: "approval_..."
workload_id: "wl_..."
policy_decision_id: "poldec_..."
approver_ref: "..."
decision: "approve|reject"
created_at: "..."
scope: []
budget_delta: null
expires_at: null
approval_hash: "sha256:..."
extensions: {}
```

An approval MUST have explicit scope and cannot be interpreted as blanket authority.

## 12. Reason Codes

At minimum:

```text
POLICY_OK
WORKLOAD_INVALID
IDENTITY_UNVERIFIED
BUDGET_EXCEEDED
COMPUTE_BUDGET_EXCEEDED
QUOTA_BUDGET_EXCEEDED
RISK_BUDGET_EXCEEDED
IRREVERSIBILITY_BUDGET_EXCEEDED
RECOVERY_BUDGET_EXCEEDED
RESOURCE_NOT_ALLOWED
RESOURCE_QUARANTINED
TOOL_NOT_ALLOWED
CAPABILITY_NOT_ALLOWED
HARNESS_NOT_ALLOWED
PRIVACY_CONSTRAINT
DATA_EGRESS_CONSTRAINT
VERIFICATION_INSUFFICIENT
APPROVAL_REQUIRED
NO_ADMISSIBLE_STRATEGY
TIMEOUT_CONSTRAINT
RETRY_CONSTRAINT
RECOVERY_CONSTRAINT
```

## 13. External Policy Backends

Rasputin MAY compile or delegate subsets of authorization logic to OPA/Rego, Cedar or future standards.

External engines are adapters. Rasputin owns the normalized authority semantics for computational capital, budgets, risk, irreversibility and recovery.

## 14. Security Invariants

1. Allocator MUST NOT widen policy constraints.
2. Strategy Compiler MUST NOT widen policy constraints.
3. Fallback and recovery MUST remain in the same or stricter authority envelope.
4. Tool/MCP/A2A adapters receive effective restrictions where technically applicable.
5. Budget exhaustion is an execution control event, not just telemetry.
6. Policy and AuthorityEnvelope hashes bind into final evidence.
7. Unknown policy major versions fail closed.
8. Quarantined resources cannot be selected until explicitly released.
9. Human approval must be explicit and scoped.
10. Red-team execution obeys a dedicated test authority envelope and cannot inherit production privilege by default.

## 15. Required Tests

Before R4 acceptance:

- allowed resource executes;
- denied resource cannot execute;
- denied tool/capability cannot execute;
- budget exhaustion blocks dispatch;
- cumulative irreversibility exhaustion blocks an otherwise legal action;
- recovery cannot bypass original policy;
- resource quarantine invalidates selection;
- human approval blocks then permits only authorized scope;
- overlapping policies normalize conservatively;
- policy/authority hashes change on material change;
- unknown major version fails closed.

## 16. Separation of Concerns

```text
Policy / Authority: what may happen?
Capital Allocator: what is worth funding among admissible options?
Strategy Compiler: how should admitted capital be spent?
Execution Control: carry out and enforce.
Recovery: restore within authorized bounds.
Evidence: what can be reconstructed/proven?
Outcome: what value resulted?
```

These roles must not collapse into an unreviewable monolith.

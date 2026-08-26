# Rasputin CORE-0 — Policy Engine Contract

> Status: PRE-DEVELOPMENT / DRAFT FOR GATE-CORE-0  
> Contract ID: CORE-0-CONTRACT-POLICY  
> Version: 0.1.0-alpha

## 1. Purpose

The Policy Engine defines the admissible execution space before Economics routing and execution. It is a governance boundary, not a recommendation system.

## 2. Inputs

```text
Task
Tenant / Workspace Policy
Environment Policy
Runtime Capability State
Human Approval State (optional)
```

## 3. Outputs

```text
PolicyDecision
Normalized Constraints
Allowed Resource Set
Required Controls
Approval Requirement
Reason Codes
```

## 4. Policy Domains

P0 policy domains:

- budget
- model allow/deny
- tool allow/deny
- harness allow/deny
- privacy
- verification
- timeout
- retry
- human approval

Future policy domains MAY include jurisdiction, data residency, identity assurance, regulatory classification and segregation-of-duties.

## 5. Evaluation Order

```text
1. Validate task
2. Apply hard deny rules
3. Apply privacy restrictions
4. Apply resource allowlists
5. Apply budget limits
6. Apply verification requirements
7. Determine approval requirement
8. Normalize constraints
9. Emit PolicyDecision
```

Hard constraints MUST dominate optimization preferences.

## 6. Decision Semantics

### allow
Task may proceed inside the normalized execution space.

### deny
Task MUST NOT execute.

### allow_with_conditions
Task may execute only if specified controls are satisfied.

### require_human_approval
Task is blocked pending an explicit approval artifact.

## 7. Example Policy

```yaml
policy_id: "policy_finance_research"
version: "1.0.0"
rules:
  budget:
    max_amount: 0.50
    currency: "USD"
  models:
    allow: ["provider/model-a", "local/model-b"]
  tools:
    deny: ["trade.execute"]
  privacy:
    max_external_data_level: "internal"
  verification:
    minimum: "enhanced"
  retries:
    max: 2
  human_approval:
    required_for: ["trade.execute", "payment.send"]
```

## 8. Constraint Normalization

Policies from multiple scopes are combined conservatively.

Examples:

- maximum budget = minimum of applicable maxima;
- allowed models = intersection of applicable allowlists;
- denied tools = union of applicable deny sets;
- verification requirement = strongest applicable level;
- approval requirement = required if any applicable rule requires it.

If normalization produces an empty admissible resource set, the decision is `deny` with an explicit reason code.

## 9. Reason Codes

P0 reason codes SHOULD include:

```text
POLICY_OK
TASK_INVALID
BUDGET_EXCEEDED
MODEL_NOT_ALLOWED
TOOL_NOT_ALLOWED
HARNESS_NOT_ALLOWED
PRIVACY_CONSTRAINT
VERIFICATION_INSUFFICIENT
APPROVAL_REQUIRED
NO_ADMISSIBLE_STRATEGY
TIMEOUT_CONSTRAINT
RETRY_CONSTRAINT
```

## 10. Policy Hashing

The canonical serialized policy used for a decision MUST be hashed.

Evidence MUST be able to prove which policy version governed a run.

```text
policy_hash = SHA-256(canonical_policy_bytes)
```

## 11. Human Approval Contract

Approval is a first-class artifact and MUST NOT be represented as an informal log message.

Minimum conceptual fields:

```yaml
approval_id: "approval_..."
task_id: "task_..."
policy_decision_id: "poldec_..."
approver_ref: "..."
decision: "approve|reject"
created_at: "..."
scope: []
approval_hash: "sha256:..."
```

P0 may use a local trusted approver identity. Strong identity/attestation is future work.

## 12. Security Invariants

1. Router MUST NOT widen policy constraints.
2. Fallback execution MUST remain inside the same or stricter policy space.
3. Tool adapters MUST receive effective policy restrictions where technically applicable.
4. Policy version and hash MUST be bound into final evidence.
5. A policy failure is not converted into a retry unless policy explicitly allows reevaluation.
6. Unknown policy major versions fail closed.

## 13. Separation of Concerns

Policy answers:

> What is allowed?

Economics answers:

> Among allowed options, what is preferable?

Execution answers:

> Carry out the selected admissible plan.

Evidence answers:

> What can be reconstructed or verified afterward?

No component may collapse these four roles into an unreviewable monolith.

## 14. CORE-1/4 Required Tests

Before policy functionality is accepted, tests MUST include:

- allowed model succeeds;
- denied model cannot execute;
- denied tool cannot execute;
- overlapping policies normalize conservatively;
- empty allowed set produces deny;
- enhanced verification requirement excludes basic-only strategy;
- human approval blocks then permits execution;
- policy hash changes when material policy changes;
- fallback cannot bypass original policy.

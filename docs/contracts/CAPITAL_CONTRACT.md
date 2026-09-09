# Rasputin v7 — Computational Capital Contract

> **Status:** R0 MIGRATION DRAFT  
> **Contract ID:** V7-CONTRACT-CAPITAL  
> **Version:** 1.0.0-alpha

## 1. Purpose

Defines the canonical economic objects used to price, reserve, consume and reallocate computational capital across workloads.

## 2. Capital Dimensions

At minimum Rasputin recognizes:

```text
money
compute
tokens / quota
latency
verification
human attention
risk
irreversibility
recovery
```

A deployment MAY add dimensions through versioned extensions.

## 3. BudgetEnvelope

```yaml
schema_version: "1.0.0"
budget_envelope_id: "budget_..."
scope:
  type: "principal|tenant|portfolio|workload|run|resource|recovery"
  ref: "..."
created_at: "..."
valid_until: null
limits:
  money: null
  compute: null
  quota: null
  latency: null
  verification: null
  human_attention: null
  risk: null
  irreversibility: null
  recovery: null
hardness:
  money: "hard|soft"
  compute: "hard|soft"
  quota: "hard|soft"
  latency: "hard|soft"
  verification: "hard|soft"
  human_attention: "hard|soft"
  risk: "hard|soft"
  irreversibility: "hard|soft"
  recovery: "hard|soft"
policy_ref: null
metadata: {}
extensions: {}
```

## 4. BudgetLedgerEntry

```yaml
schema_version: "1.0.0"
ledger_entry_id: "led_..."
budget_envelope_id: "budget_..."
created_at: "..."
operation: "reserve|consume|release|adjust|expire|settle"
dimension: "money|compute|quota|latency|verification|human_attention|risk|irreversibility|recovery"
amount: null
unit: null
portfolio_id: null
workload_id: null
run_id: null
allocation_id: null
recovery_id: null
resource_id: null
reason_code: null
parent_entry_id: null
entry_hash: null
extensions: {}
```

Ledger entries are append-only.

## 5. Cost Model

Rasputin distinguishes:

```text
NominalCost
EffectiveCost
ShadowCost Components
OpportunityCost
RecoveryReserveCost
```

Conceptually:

```text
EffectiveCost =
    MonetaryCost
  + QuotaScarcityCost
  + LatencyScarcityCost
  + RiskCost
  + VerificationCost
  + HumanAttentionCost
  + OpportunityCost
  + RecoveryReserveCost
```

Implementations may use normalized dimensionless utility instead of converting every component into currency, but the mapping MUST be explicit and versioned.

## 6. ShadowPrice

```yaml
schema_version: "1.0.0"
shadow_price_id: "sp_..."
resource_id: "res_..."
observed_at: "..."
allocator_version: "..."
nominal_price: null
effective_price: null
components:
  quota_scarcity: null
  latency_scarcity: null
  risk: null
  verification: null
  human_attention: null
  opportunity_cost: null
  recovery_reserve: null
confidence: null
reason_codes: []
extensions: {}
```

Shadow prices are decision inputs, not immutable facts.

## 7. Allocation Semantics

A CapitalAllocation may reserve capital before execution. Execution then consumes or releases reserved amounts.

```text
allocate
 -> reserve
 -> execute
 -> consume / release
 -> recover if needed
 -> settle
```

The system must prevent double-spending of hard shared budgets under concurrent workloads.

## 8. Portfolio Competition

When multiple workloads compete for a shared budget, the allocator may consider:

```text
expected outcome value
uncertainty
priority
deadline
resource affinity
marginal cost
marginal risk
marginal irreversibility
future opportunity cost
```

Independent per-request optimization is not sufficient when budgets are shared.

## 9. Admission Actions

Valid capital decisions include:

```text
EXECUTE
DEFER
DO_NOT_EXECUTE
WAIT_FOR_INFORMATION
REQUIRE_HUMAN_APPROVAL
```

The absence of execution is a valid economic decision and must have reason codes.

## 10. Recovery Budget

Recovery is a separate budget dimension because retries, reroutes, extra verification and human escalation consume additional capital.

Conceptual stop rule:

```text
ExpectedRemainingRiskAdjustedValue
  < ExpectedRecoveryCost + ExpectedAdditionalRisk
=> ABORT / DEFER / ESCALATE
```

## 11. Irreversibility Budget

Irreversibility limits cumulative non-cheaply-reversible effects across a scope.

An action can be individually allowed yet still denied when aggregate authorized irreversibility is exhausted.

## 12. Concurrency Invariants

1. Hard budgets cannot be oversubscribed by race conditions.
2. Reservations have explicit expiry/release semantics.
3. Ledger writes are idempotent where retryable.
4. Recovery consumption uses recovery-specific accounting.
5. Resource quarantine can invalidate future reservations but cannot silently rewrite consumed ledger history.
6. Budget adjustments require explicit authority.

## 13. Algorithm Boundary

The contract does not require one allocator algorithm.

Supported evolution:

```text
deterministic scoring
Lagrangian / dual allocation
contextual bandits
budgeted / knapsack-style online learning
offline policy learning
robust / risk-sensitive sequential control
```

All algorithms must emit the same canonical allocation and ledger objects.

## 14. Required Tests

- deterministic reserve/consume/release sequence;
- concurrent workloads cannot exceed a hard shared budget;
- reservation expiry releases capacity;
- recovery budget exhaustion blocks further automated recovery;
- irreversibility budget blocks cumulative irreversible action;
- shadow-price change can alter allocation without changing nominal price;
- `DO_NOT_EXECUTE` produces valid allocation evidence;
- budget adjustment requires authorized artifact.

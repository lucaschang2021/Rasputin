# Rasputin v7 — Evidence & Assurance Contract

> **Status:** R0 MIGRATION DRAFT  
> **Contract ID:** V7-CONTRACT-EVIDENCE  
> **Version:** 1.0.0-alpha

## 1. Purpose

Defines the minimum semantic and cryptographic record required to make a Rasputin allocation/execution/recovery/assurance history reconstructable, tamper-evident and extensible to signatures, transparency, attestation and future Zero-Knowledge Compliance.

Evidence is not equivalent to logging.

```text
Telemetry: what was measured?
Evidence: what claims are bound together and integrity-checkable?
Outcome: what happened downstream?
Assurance: what adversarial / recovery condition was tested and with what result?
```

## 2. Trust Boundary

Initial v7 evidence provides tamper-evident provenance under a trusted-enough local control-plane assumption.

It does NOT by itself prove:

- trusted hardware execution;
- provider honesty;
- semantic truth of model output;
- hidden chain-of-thought;
- public-chain finality;
- ZK policy proof.

Those capabilities attach through stronger adapters and explicit verification levels.

## 3. EvidenceRecord

```yaml
schema_version: "1.0.0"
evidence_id: "ev_..."
created_at: "..."
evidence_type: "portfolio|policy|authority|allocation|plan|run_start|model_call|tool_call|runtime|ledger|failure|recovery|quality|outcome|assurance|run_final|portfolio_reallocation"
portfolio_id: null
workload_id: null
run_id: null
claims:
  policy_decision_id: null
  authority_envelope_id: null
  allocation_id: null
  execution_plan_id: null
  resource_state_refs: []
  failure_id: null
  recovery_id: null
  outcome_id: null
  assurance_result_id: null
commitments:
  input_hashes: []
  output_hashes: []
  policy_hash: null
  authority_hash: null
  allocation_hash: null
  plan_hash: null
  telemetry_hash: null
  ledger_hash: null
  result_hash: null
lineage:
  previous_evidence_hash: null
  parent_evidence_ids: []
verification:
  level: "basic"
  mechanisms: ["canonical_hash_chain"]
extensions: {}
evidence_hash: "sha256:..."
```

## 4. Canonical Serialization

Hashing requires deterministic bytes:

1. stable canonical field ordering;
2. normalized UTF-8;
3. normalized RFC3339 timestamps;
4. explicit null semantics;
5. deterministic numeric representation;
6. `evidence_hash` excluded from its own digest;
7. golden vectors for each major contract version.

## 5. Hash Chain

```text
H_0 = SHA256(canonical(E_0))
H_n = SHA256(canonical(E_n with previous_evidence_hash = H_(n-1)))
```

Deletion, reordering or mutation should be detectable against a known chain head / anchor.

## 6. Merkle Aggregation

Finalized evidence MAY be batched.

```yaml
schema_version: "1.0.0"
batch_id: "batch_..."
created_at: "..."
leaf_count: 0
leaf_hashes: []
merkle_root: "sha256:..."
algorithm: "sha256-binary-v1"
signature_refs: []
attestation_refs: []
external_anchor: null
```

Leaf ordering, odd-leaf behavior, proof format and verification function must be deterministic.

## 7. Evidence Lifecycle

```text
Portfolio admitted
 -> Workload / policy / authority evidence
 -> Capital allocation evidence
 -> Execution plan evidence
 -> Run / tool / model / runtime evidence
 -> Ledger commitments
 -> Failure / recovery evidence when applicable
 -> Quality evidence
 -> Outcome evidence (possibly delayed)
 -> Final run evidence
 -> Portfolio reallocation evidence when applicable
 -> Optional Merkle / signature / attestation / external anchor
```

## 8. Capital Evidence

Every material CapitalAllocation should be able to bind:

```text
allocator identity/version
workload / portfolio
resource-state snapshot refs
policy / authority refs
budget refs
expected value
expected effective cost
selection / deferral reason codes
allocation hash
```

This allows later reconstruction of **why intelligence was or was not funded**.

## 9. Recovery Evidence

Recovery evidence binds:

```text
failure
failure severity / suspected cause
containment action
recovery strategy
recovery budget consumed
new plan / reroute if any
verification result
final recovery outcome
portfolio reallocation if triggered
```

Recovery evidence MUST distinguish:

- original declared plan;
- observed failure;
- containment action;
- modified execution path.

## 10. Red-Blue / Assurance Evidence

Assurance runs are first-class evidence.

Conceptual object:

```yaml
schema_version: "1.0.0"
assurance_result_id: "assure_..."
scenario_id: "scenario_..."
created_at: "..."
mode: "shadow|controlled_chaos|staging|authorized_production"
targets: []
attack_class: null
expected_controls: []
observed_controls: []
bypass_detected: false
unauthorized_effect: false
blast_radius_refs: []
recovery_refs: []
metrics: {}
evidence_refs: []
extensions: {}
```

Red-team tooling MUST have its own bounded test authority and evidence must prove which environment and permissions were used.

## 11. Outcome Evidence

Outcome may be delayed and external to the runtime. Evidence should record source and attribution strength rather than pretending all value is directly caused by one execution.

```text
OutcomeRecord
 -> source refs / business event refs
 -> attribution confidence
 -> realized value
 -> risk adjustment
 -> execution / workload lineage
```

## 12. Data Minimization

Evidence should prefer commitments/references over sensitive plaintext.

```text
Sensitive Payload
  -> secure/local reference
  -> stable commitment
  -> evidence includes reference + commitment
```

The evidence plane must not become an uncontrolled confidential-data replica.

## 13. Verification Levels

### none
No cryptographic integrity requirement.

### basic
Canonical hashes and execution provenance.

### enhanced
Hash chain + policy/authority/allocation/plan binding + Merkle or equivalent stronger controls.

### attested
Evidence additionally bound to external workload/runtime/hardware identity or attestation.

### zk
Future compliance proof over selected predicates without revealing protected data.

Reports must never overstate proof strength.

## 14. Future Trust Adapters

Future adapters may bind:

- workload identity;
- runtime image digest;
- tool/harness digest;
- TEE / confidential-compute attestation;
- provider identity where verifiable;
- transparency-log inclusion;
- supply-chain provenance;
- external timestamp / ledger anchor.

These extend the evidence plane rather than create parallel audit systems.

## 15. Zero-Knowledge Compliance

Future ZK scope is limited to predicates such as:

```text
approved resource set was respected
cost <= authorized budget
risk / irreversibility metric <= threshold
required policy version was enforced
required attestation was present
private compliance condition evaluated true
```

Rasputin does not attempt to prove hidden model reasoning.

## 16. Security Invariants

1. Finalized evidence is append-only.
2. `run_final` binds effective policy, authority, allocation and execution plan.
3. Evidence distinguishes declared plan from observed execution.
4. Missing required evidence causes verification failure, never silent downgrade.
5. Unknown verification mechanisms fail explicitly.
6. Sensitive plaintext is not required when a stable commitment suffices.
7. External anchoring is not semantic correctness.
8. Deterministic integrity verification must not require an LLM.
9. Recovery cannot rewrite failure history.
10. Assurance results cannot be marked successful if an unauthorized irreversible effect occurred.
11. Delayed outcome records append; they do not mutate finalized run evidence.

## 17. Required Tests

At minimum:

- deterministic hash golden vectors;
- one-byte material mutation changes hash;
- canonical field reordering is stable;
- broken chain detected;
- removed/reordered evidence detected against known head;
- Merkle proof success/failure vectors;
- final evidence binds policy/authority/allocation/plan;
- recovery evidence preserves original failure and modified plan lineage;
- assurance evidence records mode and bounded authority;
- verifier runs deterministically without model calls.

## 18. Core Principle

Rasputin must always distinguish:

> **what was observed, what was inferred, what was authorized, and what can actually be proven.**

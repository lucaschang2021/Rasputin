# Rasputin CORE-0 — Execution Evidence Contract

> Status: PRE-DEVELOPMENT / DRAFT FOR GATE-CORE-0  
> Contract ID: CORE-0-CONTRACT-EVIDENCE  
> Version: 0.1.0-alpha

## 1. Purpose

The Evidence Contract defines the minimum cryptographic and semantic record required to make an Agent execution reconstructable, tamper-evident and suitable for later attestation, anchoring and zero-knowledge compliance proofs.

Evidence is not equivalent to logging.

Logs answer:

> What did the runtime report?

Evidence aims to answer:

> What execution claims are bound together, which artifacts support those claims, and can silent post-hoc mutation be detected?

## 2. P0 Trust Boundary

P0 provides tamper-evident provenance under a local-runtime trust assumption.

P0 DOES NOT claim:

- trusted hardware execution;
- remote attestation;
- semantic correctness of model output;
- proof of hidden chain-of-thought;
- public-chain finality;
- zero-knowledge policy proof.

These are future layers that attach to the same evidence model.

## 3. Evidence Object

Minimum conceptual schema:

```yaml
schema_version: "0.1.0"
evidence_id: "ev_..."
run_id: "run_..."
task_id: "task_..."
created_at: "..."
evidence_type: "run_start|policy|plan|model_call|tool_call|runtime|quality|run_final"
claims:
  policy_decision_id: null
  policy_hash: null
  execution_plan_id: null
  plan_hash: null
  model_ref: null
  harness_ref: null
  tool_refs: []
  runtime_ref: null
commitments:
  input_hashes: []
  output_hashes: []
  telemetry_hash: null
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

Hashing MUST operate on deterministic canonical bytes.

P0 requirements:

1. stable field ordering;
2. normalized UTF-8;
3. normalized timestamp representation;
4. explicit null handling;
5. deterministic number representation;
6. `evidence_hash` excluded from the payload being hashed.

Implementation may use canonical JSON or another deterministic format, but the format MUST be documented and covered by golden-vector tests.

## 5. Hash Chain

Each evidence record binds the prior accepted record for a run or evidence stream.

```text
H_0 = SHA256(E_0)
H_n = SHA256(canonical(E_n with previous_evidence_hash = H_(n-1)))
```

Mutation, deletion or reordering SHOULD be detectable when the verifier has the expected chain head or a trusted anchor.

## 6. Merkle Aggregation

Finalized evidence records MAY be batched into a Merkle tree.

P0 MUST define:

- deterministic leaf construction;
- deterministic leaf ordering;
- tree construction rule;
- odd-leaf rule;
- root encoding;
- inclusion proof format;
- verification function.

Conceptual batch object:

```yaml
batch_id: "batch_..."
created_at: "..."
leaf_count: 0
leaf_hashes: []
merkle_root: "sha256:..."
algorithm: "sha256-binary-v1"
external_anchor: null
```

## 7. Evidence Lifecycle

```text
Task accepted
  -> policy evidence
  -> plan evidence
  -> execution event evidence
  -> telemetry commitment
  -> quality commitment
  -> final result commitment
  -> final run evidence
  -> optional Merkle batch
```

The exact number of intermediate evidence records may vary by execution mode, but final evidence MUST bind the policy, plan, result and relevant telemetry commitments.

## 8. Data Minimization

Evidence SHOULD contain commitments and references rather than sensitive raw payloads.

Preferred pattern:

```text
Sensitive Input
   |
   +--> secure/local storage reference
   |
   +--> SHA-256 commitment included in evidence
```

Rasputin must not turn its audit subsystem into an uncontrolled secondary copy of confidential data.

## 9. Evidence Claims vs Proof Strength

Verification levels are intentionally explicit.

### none
No cryptographic evidence requirement.

### basic
Canonical local hashes and execution provenance.

### enhanced
Hash chain + policy/plan binding + Merkle aggregation or equivalent stronger local controls.

### attested
Future: evidence additionally bound to external runtime/hardware identity or attestation.

### zk
Future: selected policy/compliance predicates proven without revealing protected underlying data.

A UI or report MUST NOT describe `basic` evidence as remote attestation or zero-knowledge proof.

## 10. External Anchoring Interface

Public-chain or private-network anchoring is optional and downstream.

Future anchor record:

```yaml
anchor_id: "anchor_..."
batch_id: "batch_..."
merkle_root: "sha256:..."
anchor_type: "l2|private_ledger|timestamp_service|other"
network_ref: "..."
transaction_ref: "..."
anchored_at: "..."
```

Anchoring proves existence/commitment relationships under the backend's trust model. It does not establish the semantic truth of Agent output.

## 11. Future Attestation Adapter

The evidence model reserves space for runtime identity and attestation artifacts.

Future adapters may bind:

- runtime image digest;
- hardware/TEE identity;
- software measurement;
- policy engine version;
- tool adapter digest;
- model/provider identity where verifiable.

Attestation MUST extend the evidence plane rather than require a parallel audit system.

## 12. Future Zero-Knowledge Compliance

Rasputin's zk target is a verifiable compliance statement, not proof of hidden model reasoning.

Examples:

```text
"Execution used only approved resources."
"Private risk metric was below threshold T."
"Required policy P was satisfied."
"A computation over confidential data produced a result satisfying predicate R."
```

The P0 evidence schema must preserve stable commitments that future circuits or proof systems can reference.

## 13. Security Invariants

1. Finalized evidence is append-only.
2. `run_final` evidence MUST bind the effective policy and execution plan.
3. Evidence MUST distinguish declared plan from observed execution where possible.
4. Missing required evidence causes verification failure, not silent downgrade.
5. Unknown verification mechanisms fail explicitly.
6. Sensitive plaintext is not required for integrity verification when a stable commitment/reference suffices.
7. External anchoring is never treated as proof of correctness.
8. Evidence verification MUST be possible without invoking an LLM.

## 14. P0 Required Verification Tests

`GATE-CORE-5` will require:

- same canonical object produces same hash;
- one-byte material mutation changes hash;
- changed field ordering before canonicalization does not change hash;
- broken previous hash is detected;
- removed/reordered record is detected against known chain head;
- Merkle inclusion proof verifies;
- modified Merkle leaf fails verification;
- final evidence references policy and plan hashes;
- verifier runs deterministically without model calls.

## 15. Core Principle

Rasputin should be able to say precisely:

> This is what we can prove cryptographically.

and separately:

> This is what we merely observed or inferred.

That separation is mandatory for every later trust claim.

# Frontend Role — Rasputin v7

## Mission

Expose the accepted Rasputin control plane as a precise operational console without inventing runtime, capital, policy or evidence truth in the UI.

## Entry condition

A frontend surface begins only after the backend contracts it consumes are accepted. Frontend production work remains blocked during v7 R0 migration.

## Owns

- portfolio / workload submission and state surfaces;
- capital allocation and reason-code views;
- resource health / availability / shadow-price views;
- policy / authority / approval controls;
- execution trace and lifecycle visualization;
- budget / cost / quota / risk / irreversibility / recovery dashboards;
- recovery timeline and quarantine state;
- Red-Blue / assurance result views;
- quality / outcome / ROCC views;
- evidence / provenance verification surfaces;
- denied / deferred / do-not-execute / exhausted-budget states;
- safe operator and HITL interfaces.

## Must not

- change backend contracts implicitly;
- infer new authority from UI state;
- label allocator estimates as realized outcomes;
- label telemetry as cryptographic proof;
- expose secrets or protected payloads by default;
- display hidden chain-of-thought as a product requirement;
- hide failure, quarantine or degraded state behind optimistic UI;
- silently turn `DEFER` or `DO_NOT_EXECUTE` into execution.

## Truth Labels

Where relevant the UI must distinguish:

```text
MEASURED
INFERRED / ESTIMATED
AUTHORIZED
PROVEN / VERIFIED
REALIZED OUTCOME
```

## Acceptance Standard

- accepted backend schemas consumed without drift;
- portfolio and workload state remain internally consistent;
- allocation / authority reason codes render faithfully;
- recovery and assurance state is visible where relevant;
- critical user journeys pass;
- error/empty/loading/denied/deferred/quarantined states are complete;
- no sensitive-data leakage in common views;
- UI build/test/interaction evidence returned to Controller.

# Frontend Role — Rasputin

## Mission
Expose the accepted Rasputin backend as a precise operational console without inventing runtime truth in the UI.

## Entry condition
Frontend implementation starts only after `GATE-BE-*` acceptance.

## Owns
- task submission and status surfaces
- policy control surfaces
- execution trace visualization
- economics/cost/latency dashboards
- evidence/provenance verification surfaces
- error/loading/denied/retry states
- safe operator controls and HITL interfaces

## Must not
- change backend contracts implicitly
- expose secrets or protected payloads by default
- display hidden chain-of-thought as a product requirement
- label estimates as measured facts
- hide backend failures behind optimistic UI

## Acceptance standard
- accepted backend schemas consumed without drift
- critical user journeys pass
- error/empty/loading states are complete
- accessibility and usability baseline
- no sensitive-data leakage in common views
- UI build/test evidence returned to Controller

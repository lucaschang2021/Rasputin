# Rasputin — Project State

> **Updated:** 2026-08-26  
> **Architecture:** v6.0-alpha  
> **Development mode:** ACTIVE ALPHA / Backend lane

## Control State

```text
CORE-0 Architecture/Contracts     ACCEPTED
Master development workflow       FROZEN
Backend lane                      OPEN
Frontend lane                     BLOCKED
Integration/Test lane             BLOCKED
GitHub/Release lane               BLOCKED
```

## Accepted Documents

- README.md
- docs/ARCHITECTURE.md
- docs/PRE_DEVELOPMENT.md
- docs/GATE_CORE_0.md
- docs/contracts/EXECUTION_SCHEMA.md
- docs/contracts/POLICY_CONTRACT.md
- docs/contracts/EVIDENCE_CONTRACT.md
- docs/00-PROJECT-CONTROL.md
- docs/01-MASTER-TECHNICAL-DESIGN.md
- docs/02-DELIVERY-BOARD.md
- docs/03-DEVELOPMENT-WORKFLOW.md
- docs/roles/BACKEND.md
- docs/roles/FRONTEND.md
- docs/roles/INTEGRATION.md
- docs/roles/GITHUB_RELEASE.md

## Current Objective

Build R0 as a strong headless Rasputin Core before UI work.

Target R0 chain:

```text
Task
 -> Policy
 -> Candidate Strategies
 -> Economics/Router
 -> Execution
 -> Tool Invocation
 -> Telemetry
 -> Quality
 -> Evidence
 -> Strategy Comparison
 -> Optimization Recommendation
```

## Current Admission

**Admitted:** `BE-0 Engineering Baseline`.

Frontend must not start production implementation until `GATE-BE-R0` passes.

## Strategic Strength Standard

Rasputin is explicitly optimized for infrastructure depth:

- reliable contracts;
- economic routing;
- enforceable governance;
- failure-aware execution;
- cryptographic provenance;
- measurable quality;
- provider/framework independence;
- local/private operation;
- extensible MCP/tool boundaries;
- safe optimization;
- future attestation/A2A/zk-compliance compatibility.

The project will preserve the complete v5/v6 vision but implement it by dependency order rather than feature spectacle.

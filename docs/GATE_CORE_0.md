# Rasputin — GATE-CORE-0 Historical Record

> **Gate:** GATE-CORE-0  
> **Original scope:** v6.0-alpha Architecture & Contracts  
> **Original decision:** PASS WITH CONTROLLED ASSUMPTIONS  
> **Original date:** 2026-08-26  
> **Current status:** HISTORICAL / SUPERSEDED BY `GATE-V7-R0`

## 1. Historical Purpose

This document records the acceptance decision that authorized the original v6.0-alpha execution-economics architecture.

The original v6 kernel was organized around:

```text
Execution Schema
Policy
Economics / Routing
Execution
Telemetry
Evidence
Quality
Optimization
```

That work remains useful as migration history, but it is no longer the active architecture gate.

## 2. Why It Was Superseded

Rasputin v7 raises the strategic abstraction from per-task resource routing to a **Sovereign Computational Capital Control Plane** with:

```text
Workload Portfolio
Resource Intelligence
Computational Capital Allocation
Shadow Pricing
Execution Authority
Outcome / Failure Intelligence
Adaptive Recovery
Red-Blue Adversarial Assurance
Risk / Irreversibility / Recovery Budgets
Portfolio Reallocation
```

The active gate is therefore:

```text
GATE-V7-R0
```

## 3. Migration Rule

The original `GATE-CORE-0 = PASS` decision is not revoked; it remains a truthful historical record of the v6 baseline.

However:

- it does **not** authorize new implementation against superseded v6-only contracts;
- it does **not** override v7 authority, capital, recovery or assurance contracts;
- old CORE-1 dispatch language is historical only;
- the next executable implementation stage is v7 `R1`, after `GATE-V7-R0` acceptance.

## 4. Historical Controlled Assumptions

The following unresolved implementation choices remain valid as implementation-level questions unless v7 contracts further constrain them:

1. programming language / schema library;
2. canonical serialization implementation;
3. persistent store choice;
4. concrete provider/gateway adapters;
5. evaluator implementation;
6. allocator objective calibration;
7. runtime attestation adapters.

## 5. Active Source of Truth

For current work, read:

```text
README.md
docs/00-PROJECT-CONTROL.md
docs/01-MASTER-TECHNICAL-DESIGN.md
docs/02-DELIVERY-BOARD.md
docs/03-DEVELOPMENT-WORKFLOW.md
docs/04-PROJECT-STATE.md
docs/ARCHITECTURE.md
docs/GATE_V7_R0.md
docs/contracts/*
```

> **Historical decision preserved; implementation authority superseded.**

# Rasputin — Backend Work Package R0

> **Owner:** Backend  
> **Entry:** OPEN  
> **Sequence:** BE-0 → BE-1 → BE-2 ... → BE-9  
> **Rule:** Do not skip gates.

## BE-0 — Engineering Baseline

### Objective
Create the reproducible backend foundation on which all Rasputin Core modules will be implemented.

### Required outputs

- backend package/project structure;
- runtime configuration system;
- typed settings/config boundary;
- structured logging baseline;
- canonical error taxonomy;
- test harness;
- lint/type/static-check commands;
- local development command;
- environment/secrets example without real secrets;
- minimal health/version endpoint or CLI health command;
- CI-compatible command surface.

### Architecture constraints

The baseline must leave clean module boundaries for:

```text
contracts
policy
economics
routing
runtime
tools
telemetry
evidence
evaluation
optimization
adapters
```

Do not implement speculative P1/P2 functionality during BE-0.

### Acceptance

`GATE-BE-0` requires:

1. fresh checkout/setup works from documented commands;
2. test suite executes successfully;
3. lint/type/static checks execute successfully;
4. configuration rejects missing required secrets/settings safely;
5. logs are structured and contain trace-friendly fields;
6. errors use an explicit taxonomy rather than arbitrary strings;
7. external providers are behind adapter boundaries;
8. no secret is committed;
9. repository layout matches the master architecture closely enough for BE-1 without restructuring.

### Forbidden scope

- frontend implementation;
- full model routing;
- full MCP integration;
- blockchain/L2;
- zk circuits;
- multi-agent UI;
- Obsidian integration;
- autonomous optimization.

---

## BE-1 — Contract Implementation

### Objective
Turn the accepted Markdown contracts into executable, versioned, tested schemas.

### Tasks

```text
BE-1-T1 Task schema
BE-1-T2 PolicyDecision schema
BE-1-T3 ExecutionPlan schema
BE-1-T4 Run + Telemetry + QualityEvaluation schemas
BE-1-T5 Evidence references/envelopes
BE-1-T6 versioning rules
BE-1-T7 golden fixtures + serialization stability tests
```

### Contract principles

- provider independent;
- deterministic serialization where required by evidence;
- explicit versions;
- forward evolution strategy;
- unknown/invalid states fail predictably;
- money/cost representation avoids floating-point ambiguity where economically material;
- timestamps/time zones are unambiguous;
- identifiers are globally collision-resistant enough for distributed future use;
- sensitive payloads can be referenced/committed rather than copied.

### Gate

`GATE-BE-1` requires passing schema validation, round-trip serialization and golden fixture tests.

---

## Later Backend Packages

The Controller will issue detailed packages sequentially after the preceding gate passes:

```text
BE-2 Policy Kernel
BE-3 Gateway / Router
BE-4 Execution Supervisor
BE-5 MCP / Tool Bus
BE-6 Telemetry / Economics
BE-7 Evidence Chain
BE-8 Quality Evaluation
BE-9 Optimization Loop v0
```

Backend must not preemptively implement later packages in ways that couple or freeze unreviewed design decisions.

## Required Backend Return

After each package:

```text
Task/package ID
Summary
Changed files
Architecture/contract impact
Commands executed
Test results
Failure cases tested
Performance observations
Security observations
Known limitations
Unresolved questions
Recommended gate decision
```

The Controller, not Backend, records final ACCEPT / REJECT.

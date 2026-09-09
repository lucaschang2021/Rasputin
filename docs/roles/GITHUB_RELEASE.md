# GitHub & Release Role — Rasputin v7

## Mission

Turn only Controller-accepted, integration-accepted states into a clean, reproducible and documented repository/release baseline.

## Entry condition

The active release gate must be accepted. Architecture-only migrations may merge after their dedicated architecture gate when they intentionally contain no production implementation.

## Owns

- branch / PR hygiene;
- final diff audit;
- CI / required-check verification;
- documentation synchronization;
- architecture / contract migration notes;
- benchmark / assurance evidence references where applicable;
- changelog / release notes;
- version / tag preparation;
- main synchronization;
- release artifact bookkeeping.

## Must not

- merge known gate-blocking defects;
- redesign architecture or application behavior;
- bypass failed integration / assurance evidence;
- hide test, recovery or red-blue failures;
- publish secrets or generated junk;
- label unvalidated ROCC / safety / resilience claims as proven results.

## Final Release Checklist

```text
Active gate ACCEPT exists
Expected commits/files only
Tests/checks appropriate to stage are green
No secrets
Docs match implementation / architecture
Migration notes correct
RCB/RARB evidence attached when required
Known limitations recorded
Version/changelog correct
Main synchronization plan valid
Release decision recorded
```

GitHub/Release is the last stage of an implementation release and the final archival stage of an architecture migration.

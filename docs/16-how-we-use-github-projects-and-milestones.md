# How We Use GitHub Projects and Milestones

## Purpose

Define the governance model used to track the Neutrosophic Lab hardening roadmap in the public repository.

## Scope

This document applies to:

- public milestones
- public epic issues
- public GitHub Project
- public roadmap documents

This document does not replace private operational tracking.

## Source-of-Truth Policy

- Private repository: exhaustive operational tracking (all micro-actions and run-level details).
- Public repository: summarized phase-level tracking for transparency and external readability.

If private and public tracking disagree, private operational truth is authoritative until public docs are updated.

## Tracking Model

The public tracking model uses:

- 10 milestones (`M0` to `M9`)
- 10 epic issues (one per milestone)
- 1 GitHub Project for progress visualization
- 1 public roadmap document aligned with milestones

## Artifact Responsibilities

### Milestones

Milestones define:

- phase boundaries
- target closure conditions
- expected sequence of delivery

### Epic Issues

Epic issues define:

- milestone intent
- current phase status
- major blockers and gating decisions

### GitHub Project

The project visualizes:

- active work
- blocked work
- validation flow
- readiness toward daily test launch

### Public Documentation

Public docs provide:

- stable reader-facing explanation
- current constraints and limits
- rationale for roadmap structure

## Required Project Fields

- `Status`: Backlog / Ready / In Progress / Blocked / Validation / Done
- `Milestone`: M0 to M9
- `Workstream`: Infra / Runtime / Persona / Routine / Evidence / NSS / Observability / Docs / Public Guide / Governance
- `Priority`: P0 / P1 / P2 / P3
- `Gate`: Baseline / Daily / Weekly / Shareability / Public
- `Proof`: doc / script / test / report / screenshot / API check
- `Target Week`
- `Blocked By`
- `Owner`

## Required Project Views

- `Master Table`
- `Status Board`
- `Milestone Roadmap`
- `Daily Test Readiness`
- `Blocked Items`
- `Public Shareability`

## Update Rules

- Update public milestones and epics when phase truth changes.
- Keep public project cards aligned with current operational reality.
- Keep roadmap docs synchronized with milestone and epic status.
- Do not expose private operational details, secrets, or non-public paths.

## Quality Gate

This document is valid only if:

- terminology is stable and non-internal
- no private prompt language appears
- public and private tracking boundaries remain explicit

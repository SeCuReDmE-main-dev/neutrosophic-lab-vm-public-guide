# How We Use GitHub Projects and Milestones

This guide explains how the lab is tracked publicly.

## Short Answer

Yes, GitHub Projects is worth using even for a solo developer, but only if it is treated as a cockpit, not as the only source of truth.

## Roles of Each Surface

### 1. Milestones

Milestones answer:

- Which major phase are we in?
- What must be true before that phase closes?
- Which epic issue belongs to that phase?

In this lab, milestones are phase-level containers.

### 2. GitHub Project

The Project answers:

- What is in progress right now?
- What is blocked?
- Which workstream is getting attention?
- What is the path toward daily test launch?

It is a visual operations surface:

- table view
- board view
- roadmap view
- blocked-items view
- shareability view

### 3. Public Docs

The docs answer:

- What the lab is
- What the lab is not
- How it works
- What remains to be hardened
- Why the roadmap exists

Docs are the durable human-readable layer.

## Why Not Use 250 Public Issues?

For a single developer, 250 individual public issues is usually more overhead than value.

The chosen model is:

- 10 milestones
- 10 epic issues
- 1 GitHub Project
- 1 complete public roadmap document

This keeps the public surface readable while preserving full transparency.

## Recommended Project Fields

The Project should use:

- `Status`: Backlog / Ready / In Progress / Blocked / Validation / Done
- `Milestone`: M0 through M9
- `Workstream`: Infra / Runtime / Persona / Routine / Evidence / NSS / Observability / Docs / Public Guide / Governance
- `Priority`: P0 / P1 / P2 / P3
- `Gate`: Baseline / Daily / Weekly / Shareability / Public
- `Proof`: doc / script / test / report / screenshot / API check
- `Target Week`
- `Blocked By`
- `Owner`

## Recommended Views

The Project should expose:

- `Master Table`
- `Status Board`
- `Milestone Roadmap`
- `Daily Test Readiness`
- `Blocked Items`
- `Public Shareability`

## Important Constraint

The public Project is not the same as the private operational source of truth.

The private implementation repository owns the exhaustive action list. The public repository explains and visualizes progress.

## Practical Recommendation for Solo Use

If the work becomes noisy:

- keep the 250 micro-actions in the private TODO source;
- keep milestones and epic issues public;
- keep the Project curated and readable;
- update the public docs when phase truth changes.

That gives the best balance between transparency and maintainability.

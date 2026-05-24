

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

---

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


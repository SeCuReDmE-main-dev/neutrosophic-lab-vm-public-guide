# Daily and Weekly Routine Contracts

This page explains how the public VM lab now treats daily and weekly work as **app contracts**, not as generic shell smoke tests.

The key principle is simple:

- the app must prove it is present
- the app must prove a minimal working state
- only then may the agent attempt delegated analysis

This keeps the lab anchored in real application behavior instead of turning everything into prompt theater.

## Why app behavior comes first

The lab contains four public case-study workspaces plus one orchestrator workspace:

- Agent Squad
- Aden/Hive
- Haystack
- Ragas
- lab-orchestrator-public

Each of the first four corresponds to a real upstream project with its own structure, semantics, and failure patterns.

If the lab delegated first and checked the app later, it would weaken the value of the traces. The system could produce analysis text without proving the upstream app surface was actually healthy.

So the contract is:

1. presence and integrity
2. minimal app-native behavior
3. bounded secondary app behavior
4. optional delegated analysis
5. alternate or retry pass

## Daily routine structure

The daily routine is intentionally stronger than a basic smoke run.

Each public app lane receives **five focused blocks**:

1. bootstrap and presence integrity
2. upstream app working-state smoke
3. secondary app-native behavior
4. delegated analysis of the produced trace
5. alternate or retry behavior

Each block is given a **10-minute budget** and each block is followed by a **10-second cooldown**.

The lab still enforces a one-heavy-process-at-a-time policy, so these lanes run sequentially.

Important detail: the block budget is a maximum. A block may complete faster. The contract is about bounded intensity, not artificial waiting.

## Why delegation happens after health

OpenClaw delegation is used here as a bounded analysis mechanism.

It is not used as a substitute for proving that:

- the app exists
- the app is on the expected branch
- the app-specific command surface works
- the app can produce a real trace

If health has not been proven by the end of the third block, the delegation block abstains rather than inventing confidence.

## Daily role by app

## `agent-squad-public`

This lane watches:

- response-merging
- inter-agent disagreement
- ambiguity that should remain visible

Its daily contract is meant to show whether the multi-agent surface is present and whether its orchestrator-related code paths remain structurally healthy enough to support comparison.

Delegated analysis in this lane focuses on:

- disagreement quality
- merge quality
- unresolved ambiguity

It does not produce cross-hub conclusions.

## `aden-public`

This lane watches:

- worker state transitions
- blocked execution
- retry discipline
- partial success

Its daily contract focuses on whether the worker/governance surface remains structurally healthy and whether execution-state signals remain visible.

Delegated analysis in this lane focuses on:

- blocked versus complete state
- retries that may conceal failure
- partial success that should not be mislabeled as full completion

## `haystack-public`

This lane watches:

- evaluator uncertainty
- retrieval ambiguity
- HITL clarification paths

Its daily contract focuses on whether the pipeline surface remains structurally valid and whether the lab can still expose uncertainty and clarification behavior honestly.

Delegated analysis in this lane focuses on:

- insufficient evidence
- evaluator hesitation
- clarification versus forced binary closure

## `ragas-public`

This lane watches:

- support
- insufficiency
- contradiction
- metric discipline

Its daily contract focuses on whether the evaluation surface remains structurally valid and whether evidence interpretation can still be discussed without collapsing uncertainty too early.

Delegated analysis in this lane focuses on:

- metric overclaiming
- support versus insufficiency
- contradiction versus absence of evidence

## `lab-orchestrator-public`

The orchestrator does not behave like a fifth study-case lane, but in M4 it does run as a fifth contract subject.

Its role is to:

- collect the four lane outputs
- normalize evidence
- compose daily reports
- keep the reporting cadence honest

It may delegate bounded cross-lane review work, but it remains the only workspace allowed to produce final consolidated daily and weekly outputs.

It is still deliberately **not** framed as a general adaptive engine.

## Daily outputs

The daily routine produces:

- `daily_lab_report.json`
- `daily_lab_report.md`
- `daily_contract_matrix.json`
- `daily_delegation_log.json`
- `daily_failure_register.md`

These are evidence-oriented operational artifacts, not marketing summaries.

M4 also fixes a key counting boundary:

- the contract surface covers five workspaces
- the public evidence index still covers four public case-study lanes only

## Weekly routine

The weekly routine is stronger than the daily routine.

It does not merely summarize the last daily run. It re-tests the lanes with a broader evaluation shape:

- a weekly pass through all four public app lanes
- at least one alternate scenario per lane
- a variance or stability comparison pass
- a cross-lane contradiction review
- a reproducibility audit

This makes the weekly cycle the lab's heavier, more research-oriented package.

## NSS package outputs

The weekly package is built from structured source data first and then rendered into delivery formats.

The expected outputs are:

- `weekly_nss_lab_report.json`
- `weekly_nss_lab_report.md`
- `weekly_nss_lab_report.doc`
- `weekly_nss_lab_report.pdf`
- `reproducibility_appendix.md`
- `weekly_package_index.json`

The `.doc` template used by the project is treated as a structural reference, not as the binary source of truth. The canonical weekly content remains structured and auditable before document rendering.

## Prompt governance (M3.5)

The lab includes a prompt-governance layer that defines what each case-study lane evaluates during delegated analysis. This layer sits between persona contract integrity (M3) and daily routine readiness (M4).

### What M3.5 changed

Before M3.5, the public routine contract explained when delegation was allowed, but not how delegated analysis should be rotated, compared, or governed across lanes.

M3.5 added:

- one orchestrator-owned master prompt registry
- four derived lane catalogs
- one-prompt-per-lane daily assignment rules
- a seven-day anti-repeat rule
- a ten-day lane-coverage rule
- a defined signal path from prompt execution into weekly and monthly synthesis

### Ownership

The orchestrator owns prompt assignment across all four lanes. No lane assigns its own prompts. No lane modifies prompt content or assignment rules. Lanes consume prompts as read-only consumers.

### Catalog structure

Each lane draws from a catalog of ten prompts:

- seven shared-family prompts (health smoke, working-state deep-dive, delegation boundary, uncertainty and ambiguity, failure-mode simulation, reproducibility check, NSS readiness)
- three lane-specific prompts that exercise the lane's unique upstream identity

The full catalog contains forty prompts across four lanes. The orchestrator maintains one canonical master registry. Each lane receives a filtered view containing only its ten prompts.

### Daily assignment

Each lane receives one prompt per day. Assignment uses round-robin selection with a seven-day anti-repeat rule: no prompt may be reused for the same lane within seven days. Each lane covers its full ten-prompt catalog across a ten-day cycle.

When the runtime assignment engine is enabled, prompt governance replaces the old static delegated-analysis prompt source. It does not replace the five-block daily routine itself. Presence, health, and app-native proof still come first.

### Signal flow

Prompt-execution records feed into weekly trend analysis (improved, degraded, no-impact, or inconclusive per lane) and monthly twenty-eight-day recomposition. Prompt-governance signals are integrated into the weekly NSS package.

This signal flow is a closed contract surface in M3.5, not a claim that the public runtime already emits all of these artifacts today.

### Boundaries

Lane outputs remain lane-local. Cross-lane synthesis belongs exclusively to the orchestrator. Prompt governance does not change the VM runtime model policy, the default model, or the escalation model.

### Maturity

M3.5 closes design and contract hardening. M4 now makes the daily prompt-governance subset operational: live daily assignment, execution logging, lane-local provenance, and orchestrator-only daily synthesis. The orchestrator runtime observer, weekly trend analysis, and operational ten-day/twenty-eight-day cycles remain later work.

### Public-safe interpretation

Public readers should interpret M3.5 this way:

- the lab now has a documented governance model for delegated analysis
- the orchestrator is the only cross-lane authority
- lane-local execution boundaries are explicit
- the daily runtime implementation now exists
- the heavier weekly and monthly prompt-governance automation still belongs to later milestones

## Why the public repo remains codeless

This guide repository stays documentation-only.

That means:

- it does not contain the scheduler code
- it does not contain the contract runner
- it does not contain the renderer implementation
- it does not contain runtime artifacts

It explains the routine logic and its boundaries so the public architecture remains understandable without exposing the full implementation surface here.

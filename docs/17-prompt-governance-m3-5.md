# Prompt Governance (M3.5)

This page explains why the lab added an M3.5 milestone between persona contract integrity (M3) and daily routine readiness (M4).

The short answer is simple: the lab needed a public-safe governance layer for delegated analysis before it could honestly claim that daily routines were fully ready.

## Why M3.5 Exists

Before M3.5, the lab already had:

- public workspaces
- persona files
- daily and weekly routine structure
- evidence bundle design
- orchestrator reporting responsibilities

What it did not yet have was a closed answer to these questions:

- who owns prompt assignment across the four lanes
- how delegated analysis should rotate instead of repeating the same prompt shape
- how to prevent one lane from inventing its own cross-lane authority
- how daily prompt execution should later feed weekly and monthly synthesis

M3.5 was added to close that gap.

## What M3.5 Added

M3.5 adds a prompt-governance contract layer with the following properties:

- one orchestrator-owned master prompt registry
- four derived lane catalogs, one per public lane
- ten prompts per lane
- seven shared prompt families per lane
- three lane-specific prompts per lane
- one rotating prompt per lane per day
- a seven-day anti-repeat rule
- a ten-day full-coverage rule per lane

This means delegated analysis is no longer described as generic free-form prompting. It is now governed as a structured lab surface.

## Authority Model

The orchestrator is the only workspace allowed to:

- own the master registry
- assign prompts across lanes
- interpret prompt-governance signals across lanes
- produce final cross-lane synthesis

The four public lanes:

- consume prompts as read-only inputs
- execute lane-local delegated analysis
- emit lane-local outputs only

No lane assigns its own prompts. No lane claims cross-lane governance authority.

## Relationship to the Daily Routine

M3.5 does not replace the daily five-block app contract.

The order remains:

1. presence and integrity
2. app-native working-state proof
3. secondary app-native proof
4. delegated analysis
5. alternate or retry pass

What M3.5 changes is block 4. It defines how delegated analysis is governed once rotating prompt assignment is active.

## Relationship to Weekly and Monthly Work

M3.5 also defines the intended signal path after prompt execution:

- daily prompt execution produces structured prompt-governance signals
- weekly synthesis interprets those signals per lane
- monthly twenty-eight-day recomposition reviews the prompt pool and its usefulness

This design matters because the lab is not trying to run isolated daily prompts. It is building a comparable research cadence over time.

## What Is Closed Now

M3.5 is closed at the design and contract layer.

That means the public and internal documentation now agree on:

- the authority model
- the prompt catalog shape
- the anti-repeat and coverage rules
- the daily, weekly, and monthly signal-flow design
- the integration boundary with the routine contracts

## What Is Not Yet Live

M3.5 does **not** mean the full runtime implementation is already operating.

The following remain later implementation work:

- live prompt-assignment engine
- prompt-execution logging infrastructure
- orchestrator runtime observer for prompt-governance flows
- real ten-day operational trial
- real twenty-eight-day recomposition cycle
- weekly prompt-governance trend outputs generated from live runs

Public readers should therefore understand M3.5 as a governance milestone, not as proof that the full automation loop has already launched.

## Why This Matters Publicly

Without M3.5, the public guide could describe routines but not govern delegated analysis honestly.

With M3.5, the guide can now say:

- delegated analysis is bounded
- delegated analysis rotates through a defined catalog
- delegated analysis remains lane-local
- cross-lane synthesis is orchestrator-only
- later runtime work has a stable contract surface to implement against

This is what makes M3.5 a bridge milestone between M3 and M4 rather than just another note in the roadmap.

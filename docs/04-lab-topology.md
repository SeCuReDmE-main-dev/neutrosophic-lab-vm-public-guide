# Lab Topology

The VM root is:

```text
/home/ubuntu/openclaw-lab
```

## Five Public Workspaces

Workspace roots:

```text
/home/ubuntu/openclaw-lab/workspaces/agent-squad-public
/home/ubuntu/openclaw-lab/workspaces/aden-public
/home/ubuntu/openclaw-lab/workspaces/haystack-public
/home/ubuntu/openclaw-lab/workspaces/ragas-public
/home/ubuntu/openclaw-lab/workspaces/lab-orchestrator-public
```

## Full Topology With Source Contracts

| Workspace | Origin | Branch | Source mode | Agent role |
| --- | --- | --- | --- | --- |
| `agent-squad-public` | `SeCuReDmE-main-dev/agent-squad_case_study` | `lab/integrated-neutrosophic-build` | git-clone | public-case-study |
| `aden-public` | `SeCuReDmE-main-dev/aden_case_study` | `lab/integrated-neutrosophic-build` | git-clone | public-case-study |
| `haystack-public` | `SeCuReDmE-main-dev/haystack_case_study` | `lab/integrated-neutrosophic-build` | git-clone | public-case-study |
| `ragas-public` | `SeCuReDmE-main-dev/ragas_case_study` | `lab/integrated-neutrosophic-build` | git-clone | public-case-study |
| `lab-orchestrator-public` | `SeCuReDmE-main-dev/moteur-neutrosophique-adaptable` | `PaQBoT` | public-host-sync | public-lab-orchestrator |

The first four workspaces are `git-clone` from public fork repositories. The orchestrator is `public-host-sync` — synced from the host rather than cloned with Git credentials inside the VM. This avoids injecting secrets into the VM.

## Worker Workspaces

The four case-study workers each run under the `public-case-study` agent role. Their purpose:

- **Agent Squad**: routine public traces for response-merging and orchestration analysis
- **Aden**: routine public traces for worker-report and partial-success analysis
- **Haystack**: routine public traces for HITL and evaluator uncertainty analysis
- **Ragas**: routine public traces for metric confidence and triplet-aware evaluation analysis

## Orchestrator Workspace

The fifth workspace is the public lab orchestrator with four responsibilities:

1. orchestration — sequencing workspace routines
2. collection — gathering public traces from the four study-case lanes
3. evaluation — normalizing and cross-referencing evidence, including prompt-governance signals from delegated analysis
4. reporting — producing daily, weekly, and reproducibility reports

It is not a private hub and not a general adaptive engine. It does not write back into public repo source trees.

The orchestrator also owns prompt governance: it maintains the master prompt catalog, assigns one rotating prompt per lane per day, and is the sole authority for cross-lane synthesis. Lanes consume prompts as read-only consumers and produce lane-local outputs only.

## Rerun Policy

The lab intentionally recreates the five lab agents on rerun (deterministic-reset). Exact workspace bindings and model policy matter more than preserving transient agent-local state. Exported traces and public evidence bundles are the continuity mechanism for research, not the transient OpenClaw agent state.

## Runtime Constraints

- Only one active heavy workspace process at a time.
- Max runtime per worker: 3600 seconds.
- Node.js pinned to `22.22.3`.
- Default model: `ollama/gemma4:31b-cloud`.
- Escalation model: `ollama/kimi-k2.6:cloud`.

## Export Paths

```text
/home/ubuntu/openclaw-lab/exports/public/<repo>/<run-id>/
/home/ubuntu/openclaw-lab/exports/evidence/<run-id>/
```

## Runtime State

```text
/home/ubuntu/openclaw-lab/runtime/active-process.json
/home/ubuntu/openclaw-lab/runtime/*.log
```

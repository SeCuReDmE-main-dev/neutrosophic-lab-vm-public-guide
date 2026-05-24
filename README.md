# Neutrosophic Public VM Lab Guide

This is a public documentation repository for sharing the neutrosophic VM lab design, installation flow, topology, and reproducibility outputs.

**Important:** this repository is documentation-only. It is not a software contribution venue, not an upstream development repo, and not a support channel. Pull requests will not be evaluated. GitHub issues will not be triaged as support tickets. Code changes are not accepted or maintained through this public guide.

## What This Lab Does

The lab packages a reproducible public research environment for applied neutrosophic AI case studies.

It uses:

- one Multipass Ubuntu VM
- one OpenClaw gateway
- five public workspaces
- four case-study worker workspaces
- one public orchestrator workspace
- daily and weekly evidence reports
- a reproducibility appendix for audit and NSS-facing review

The four case-study workers are:

- Agent Squad: multi-agent response merging and orchestration analysis
- Aden/Hive: worker-report and partial-success analysis
- Ragas: evidence-triplet metric and RAG evaluation analysis
- Haystack: evaluator uncertainty, retrieval confidence, and HITL status analysis

The fifth workspace is:

- `lab-orchestrator-public`: orchestration, collection, evaluation, and reporting

## What This Lab Does Not Do

This repository and VM guide do not:

- change upstream/mainstream repositories
- review pull requests
- evaluate GitHub issues as support requests
- promise code maintenance
- copy secrets into the VM
- write reports to Windows user folders
- provide operational guarantees
- act as a general-purpose autonomous coding agent

## Current Integrated Workspace Branches

Each case-study workspace uses the fork-only lab branch:

```text
lab/integrated-neutrosophic-build
```

The orchestrator workspace uses the `PaQBoT` branch.

Full topology with source contracts:

| Workspace | Public fork | Branch | Source mode | Agent role |
| --- | --- | --- | --- | --- |
| Agent Squad | `SeCuReDmE-main-dev/agent-squad_case_study` | `lab/integrated-neutrosophic-build` | git-clone | public-case-study |
| Aden | `SeCuReDmE-main-dev/aden_case_study` | `lab/integrated-neutrosophic-build` | git-clone | public-case-study |
| Ragas | `SeCuReDmE-main-dev/ragas_case_study` | `lab/integrated-neutrosophic-build` | git-clone | public-case-study |
| Haystack | `SeCuReDmE-main-dev/haystack_case_study` | `lab/integrated-neutrosophic-build` | git-clone | public-case-study |
| Orchestrator | `SeCuReDmE-main-dev/moteur-neutrosophique-adaptable` | `PaQBoT` | public-host-sync | public-lab-orchestrator |

These branches are public lab builds in forks. They are not claims of upstream approval.

## Canonical VM Paths

All runtime outputs must stay inside the VM under:

```text
/home/ubuntu/openclaw-lab
```

Expected paths:

```text
/home/ubuntu/openclaw-lab/workspaces/
/home/ubuntu/openclaw-lab/exports/public/
/home/ubuntu/openclaw-lab/exports/evidence/
/home/ubuntu/openclaw-lab/reports/
/home/ubuntu/openclaw-lab/logs/scheduler/
```

## Forbidden Paths

Scheduled work and reports must not target:

```text
C:\...
/mnt/c/...
C:\Users\jeans\${workspace}
C:\Users\jeans\.82123456789
${workspace}
any unresolved ${...} path
random dot directories under a user profile
```

Windows is an operator surface only. The VM owns the runtime and reports.

## Basic Install And Run Flow

The implementation source is the orchestrator repository:

```text
https://github.com/SeCuReDmE-main-dev/moteur-neutrosophique-adaptable
```

Typical flow:

1. Install Multipass on the host.
2. Use WSL/Ubuntu as the host execution surface.
3. Clone the orchestrator repository.
4. Spawn the VM.
5. Set up the lab.
6. Validate the lab.
7. Run the public routine.
8. Collect the evidence report.

Example commands from WSL:

```bash
git clone https://github.com/SeCuReDmE-main-dev/moteur-neutrosophique-adaptable.git
cd "moteur-neutrosophique-adaptable"
git checkout PaQBoT

bash ./04_VALIDATION_LAB/pipeline/spawn_openclaw_lab.sh openclaw-e2e-test
bash ./04_VALIDATION_LAB/pipeline/setup_openclaw_multi_agent_lab.sh openclaw-e2e-test
bash ./04_VALIDATION_LAB/pipeline/validate_openclaw_multi_agent_lab.sh openclaw-e2e-test
bash ./04_VALIDATION_LAB/pipeline/run_public_workspace_routine.sh openclaw-e2e-test daily
```

## Operational Command Reference

All commands run from WSL inside the orchestrator repo checkout.

| Purpose | Command |
| --- | --- |
| Static audit (no VM needed) | `bash ./04_VALIDATION_LAB/pipeline/audit_static_lab.sh` |
| Spawn VM | `bash ./04_VALIDATION_LAB/pipeline/spawn_openclaw_lab.sh openclaw-e2e-test` |
| Setup lab inside VM | `bash ./04_VALIDATION_LAB/pipeline/setup_openclaw_multi_agent_lab.sh openclaw-e2e-test` |
| Validate VM topology | `bash ./04_VALIDATION_LAB/pipeline/validate_openclaw_multi_agent_lab.sh openclaw-e2e-test` |
| Daily routine | `bash ./04_VALIDATION_LAB/pipeline/run_public_workspace_routine.sh openclaw-e2e-test daily` |
| Weekly routine | `bash ./04_VALIDATION_LAB/pipeline/run_public_workspace_routine.sh openclaw-e2e-test weekly` |
| Full acceptance | `bash ./04_VALIDATION_LAB/pipeline/run_lab_acceptance.sh openclaw-e2e-test` |
| Scheduler status | `bash ./04_VALIDATION_LAB/pipeline/scheduler_status.sh openclaw-e2e-test` |
| Active process status | `bash ./04_VALIDATION_LAB/pipeline/active_workspace_process_status.sh openclaw-e2e-test` |
| Smoke dashboard | `bash ./04_VALIDATION_LAB/pipeline/smoke_dashboard.sh openclaw-e2e-test` |
| Smoke model policy | `bash ./04_VALIDATION_LAB/pipeline/smoke_model_policy.sh openclaw-e2e-test` |
| Smoke export/ingest | `bash ./04_VALIDATION_LAB/pipeline/smoke_export_ingest.sh openclaw-e2e-test` |

## Scheduler

The lab uses VM-side systemd user timers, not raw cron. Install the scheduler infrastructure first:

```bash
bash ./04_VALIDATION_LAB/pipeline/install_lab_scheduler.sh openclaw-e2e-test
```

Timer names:

- `openclaw-lab-daily.timer` — daily public routine
- `openclaw-lab-weekly.timer` — weekly NSS report
- `run_manual_acceptance_worker.sh` — manual acceptance trigger

## Evidence Outputs

Public evidence bundles are written to:

```text
/home/ubuntu/openclaw-lab/exports/evidence/<run-id>/
```

Each complete bundle contains:

```text
evidence-index.json
evidence-summary.md
orchestrator_reports/daily_lab_report.json
orchestrator_reports/daily_lab_report.md
orchestrator_reports/weekly_nss_lab_report.md
orchestrator_reports/reproducibility_appendix.md
```

The evidence index records repository, branch, commit, model, routine type, artifact path, and timestamp for each public workspace run. A complete routine produces exactly four public case-study entries in `evidence-index.json`.

The orchestrator summarizes evidence with:

```bash
python -m neutro_engine summarize-evidence <bundle_path> --output <target_dir>
```

## Runtime Constraints

- Only one active heavy workspace process at a time (semi-autonomous limit: 1 concurrent worker, max 3600 seconds).
- Rerun policy: deterministic-reset. Lab agents are intentionally recreated on rerun so workspace bindings and model policy stay exact. Exported traces and evidence bundles are the continuity mechanism, not transient agent state.
- Node.js pinned to `22.22.3` from the manifest.
- Default model: `ollama/gemma4:31b-cloud`. Escalation model: `ollama/kimi-k2.6:cloud`.

## Documentation Index

- [Start Here](docs/00-start-here.md)
- [What This Lab Is](docs/01-what-this-lab-is.md)
- [What This Lab Is Not](docs/02-what-this-lab-is-not.md)
- [VM Installation](docs/03-vm-installation.md)
- [Lab Topology](docs/04-lab-topology.md)
- [OpenClaw and Ollama Policy](docs/05-openclaw-ollama-policy.md)
- [Report Locations](docs/06-report-locations.md)
- [Evidence Bundle Format](docs/07-evidence-bundle-format.md)
- [Daily and Weekly Routines](docs/08-daily-weekly-routines.md)
- [Non-Coder Operator Guide](docs/09-non-coder-operator-guide.md)
- [Maintainer and Researcher Notes](docs/10-maintainer-and-researcher-notes.md)
- [Path Safety Policy](docs/11-path-safety-policy.md)
- [Reproducibility Checklist](docs/12-reproducibility-checklist.md)
- [OpenClaw Workspace Personas](docs/13-openclaw-workspace-personas.md)

## Public Boundary

This guide is intended for public understanding and reproducibility. It does not invite code contributions, promise support, or imply that any upstream project has accepted the lab branches.

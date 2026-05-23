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

Each case-study workspace is expected to use the fork-only lab branch:

```text
lab/integrated-neutrosophic-build
```

Current mappings:

| Workspace | Public fork | Branch |
| --- | --- | --- |
| Agent Squad | `SeCuReDmE-main-dev/agent-squad_case_study` | `lab/integrated-neutrosophic-build` |
| Aden | `SeCuReDmE-main-dev/aden_case_study` | `lab/integrated-neutrosophic-build` |
| Ragas | `SeCuReDmE-main-dev/ragas_case_study` | `lab/integrated-neutrosophic-build` |
| Haystack | `SeCuReDmE-main-dev/haystack_case_study` | `lab/integrated-neutrosophic-build` |

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

## Evidence Outputs

Public evidence bundles include:

```text
evidence-index.json
evidence-summary.md
daily_lab_report.md
weekly_nss_lab_report.md
reproducibility_appendix.md
```

The evidence index records repository, branch, commit, model, routine type, artifact path, and timestamp for each public workspace run.

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

## Public Boundary

This guide is intended for public understanding and reproducibility. It does not invite code contributions, promise support, or imply that any upstream project has accepted the lab branches.

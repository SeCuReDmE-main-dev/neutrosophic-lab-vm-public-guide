# Daily And Weekly Routines

The orchestrator supports three types of work:

- daily routine
- weekly NSS-style report
- manual acceptance

The lab also includes a prompt-governance milestone (M3.5) that now defines how delegated analysis is scoped across the four public lanes. That governance layer is documented here as part of the routine surface, but its live runtime pieces are still later implementation work.

## Prerequisites

The scheduler infrastructure must be installed first:

```bash
bash ./04_VALIDATION_LAB/pipeline/install_lab_scheduler.sh openclaw-e2e-test
```

## Daily Routine

The daily routine runs lightweight checks across the four case-study workers, aggregates evidence, and produces a daily lab report.

At the public-doc level, the daily routine now sits on top of two layers:

1. app-contract execution
2. prompt-governance design

The app-contract layer is the active runtime backbone. Prompt governance currently defines what delegated analysis should evaluate once the rotating assignment runtime is enabled.

Command:

```bash
bash ./04_VALIDATION_LAB/pipeline/run_public_workspace_routine.sh openclaw-e2e-test daily
```

Expected outputs:

- `evidence-index.json` with four entries
- `evidence-summary.md`
- `orchestrator_reports/daily_lab_report.json`
- `orchestrator_reports/daily_lab_report.md`

All outputs appear under `/home/ubuntu/openclaw-lab/exports/evidence/<run-id>/`.

The daily routine uses the default model (`ollama/gemma4:31b-cloud`). It does not escalate.

### Daily Routine and M3.5

M3.5 introduced these design-level rules for delegated analysis:

- the orchestrator owns prompt assignment
- each lane draws from a ten-prompt catalog
- assignment follows a seven-day anti-repeat rule
- each lane covers its ten prompts across a ten-day cycle

These rules are part of the public contract now, but the live assignment engine and execution logger are not yet declared operational in this public guide.

## Weekly Routine

The weekly routine synthesizes daily reports into a comprehensive NSS-style status report and generates a reproducibility appendix.

Command:

```bash
bash ./04_VALIDATION_LAB/pipeline/run_public_workspace_routine.sh openclaw-e2e-test weekly
```

Expected additional outputs (beyond daily):

- `orchestrator_reports/weekly_nss_lab_report.md`
- `orchestrator_reports/reproducibility_appendix.md`

The weekly routine may use the escalation model (`ollama/kimi-k2.6:cloud`) for cross-case synthesis.

### Weekly Routine and M3.5

M3.5 also defines how prompt-governance signals are intended to feed weekly synthesis:

- weekly lane interpretation may classify prompt-governance outcomes as improved, degraded, no-impact, or inconclusive
- prompt-governance trends are intended to support NSS-style weekly synthesis
- monthly twenty-eight-day recomposition is defined at the contract level

These weekly and monthly prompt-governance behaviors are planned runtime work. They should not yet be read as claims that the full signal pipeline is live.

## Manual Acceptance

Manual acceptance is a human-triggered full end-to-end verification path. Run it before publishing or relying on new evidence.

Command:

```bash
bash ./04_VALIDATION_LAB/pipeline/run_lab_acceptance.sh openclaw-e2e-test
```

This runs the full acceptance suite: static audit, VM validation, smoke tests (dashboard, model policy, export/ingest), and evidence bundle verification.

Host-side acceptance summary appears at:

```text
04_VALIDATION_LAB/output/lab_acceptance/lab_acceptance_report.md
```

## Scheduler Policy

The lab uses VM-side systemd user timers, not raw cron.

Timer names:

| Timer | Purpose |
| --- | --- |
| `openclaw-lab-daily.timer` | Triggers daily public routine |
| `openclaw-lab-weekly.timer` | Triggers weekly NSS report |
| `run_manual_acceptance_worker.sh` | Manual acceptance trigger |

Check scheduler status:

```bash
bash ./04_VALIDATION_LAB/pipeline/scheduler_status.sh openclaw-e2e-test
```

Raw cron is a fallback only if documented and controlled. Systemd timers are preferred because they provide journal logging, dependency ordering, and consistent environment isolation.

## Current Maturity Boundary

The public routine documentation now includes M3.5 because the governance design and contract are closed. This does not mean the following are already live:

- rotating prompt assignment engine
- prompt-execution logging infrastructure
- orchestrator runtime observer for prompt-governance flows
- completed ten-day and twenty-eight-day operational cycles

## Report Retention

Reports are retained for 30 days under `/home/ubuntu/openclaw-lab/reports/`. Older reports may be rotated. Evidence bundles under `/home/ubuntu/openclaw-lab/exports/evidence/` should be archived externally if long-term preservation is needed.

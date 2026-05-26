# Daily And Weekly Routines

The orchestrator supports three types of work:

- daily routine
- weekly NSS-style report
- manual acceptance

The lab also includes a prompt-governance milestone (M3.5) that defines how delegated analysis is scoped across the four public lanes. Its daily runtime subset is now active as part of M4, while the heavier weekly and monthly prompt-governance flows remain later work.

## Prerequisites

The scheduler infrastructure must be installed first:

```bash
bash ./04_VALIDATION_LAB/pipeline/install_lab_scheduler.sh openclaw-e2e-test
```

## Daily Routine

The daily routine runs lightweight checks across the four case-study workers, executes the orchestrator as a fifth contract subject, aggregates evidence, and produces a daily lab report.

At the public-doc level, the daily routine now sits on top of two active layers:

1. app-contract execution
2. prompt-governance daily runtime subset

The app-contract layer remains the runtime backbone. Prompt governance now actively supplies one governed delegated-analysis prompt per public lane per day, while weekly and monthly prompt-governance operations remain later work.

Command:

```bash
bash ./04_VALIDATION_LAB/pipeline/run_public_workspace_routine.sh openclaw-e2e-test daily
```

Expected outputs:

- `evidence-index.json` with four entries
- `evidence-summary.md`
- `orchestrator_reports/daily_lab_report.json`
- `orchestrator_reports/daily_lab_report.md`
- `orchestrator_reports/daily_contract_matrix.json`
- `orchestrator_reports/daily_delegation_log.json`
- `orchestrator_reports/daily_failure_register.md`

All outputs appear under `/home/ubuntu/openclaw-lab/exports/evidence/<run-id>/`.

The daily routine uses the default model (`ollama/gemma4:31b-cloud`). It does not escalate.

### Daily Routine and M3.5

M3.5 introduced these design-level rules for delegated analysis:

- the orchestrator owns prompt assignment
- each lane draws from a ten-prompt catalog
- assignment follows a seven-day anti-repeat rule
- each lane covers its ten prompts across a ten-day cycle

These rules are now part of the live daily routine surface. What remains later is the weekly trend-analysis pipeline, the orchestrator runtime observer, the real ten-day trial cycle, and the twenty-eight-day recomposition cycle.

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

These weekly and monthly prompt-governance behaviors are still planned runtime work. They should not be read as claims that the full signal pipeline is live.

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

The public routine documentation now includes M3.5 and M4 because the daily contract surface is closed. This does not mean the following are already live:

- orchestrator runtime observer for prompt-governance flows
- completed ten-day and twenty-eight-day operational cycles
- weekly prompt-governance trend analysis

## Report Retention

Reports are retained for 30 days under `/home/ubuntu/openclaw-lab/reports/`. Older reports may be rotated. Evidence bundles under `/home/ubuntu/openclaw-lab/exports/evidence/` should be archived externally if long-term preservation is needed.

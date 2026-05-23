# Daily And Weekly Routines

The orchestrator supports three types of work:

- daily routine
- weekly NSS-style report
- manual acceptance

## Prerequisites

The scheduler infrastructure must be installed first:

```bash
bash ./04_VALIDATION_LAB/pipeline/install_lab_scheduler.sh openclaw-e2e-test
```

## Daily Routine

The daily routine runs lightweight checks across the four case-study workers, aggregates evidence, and produces a daily lab report.

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

## Report Retention

Reports are retained for 30 days under `/home/ubuntu/openclaw-lab/reports/`. Older reports may be rotated. Evidence bundles under `/home/ubuntu/openclaw-lab/exports/evidence/` should be archived externally if long-term preservation is needed.

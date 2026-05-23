# Daily And Weekly Routines

The orchestrator supports three types of work:

- daily routine
- weekly NSS-style report
- manual acceptance

## Daily Routine

The daily routine should run lightweight checks and produce a daily lab report.

## Weekly Routine

The weekly routine should summarize cross-case evidence and produce a reproducibility appendix.

## Manual Acceptance

Manual acceptance is a human-triggered verification path. It should be run before publishing or relying on new evidence.

## Scheduler Policy

Systemd user timers are preferred over raw cron jobs. Raw cron is a fallback only if documented and controlled.

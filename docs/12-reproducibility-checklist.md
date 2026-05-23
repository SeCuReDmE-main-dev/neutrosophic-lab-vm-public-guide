# Reproducibility Checklist

Before using a report as evidence, confirm each item. Every check has an explicit pass/fail condition.

## Pre-Flight Checks

| # | Check | Pass condition | Fail condition |
| --- | --- | --- | --- |
| 1 | Static audit | `audit_static_lab.sh` exits 0 with no forbidden path patterns | Non-zero exit or forbidden path detected |
| 2 | VM validation | `validate_openclaw_multi_agent_lab.sh` exits 0 | Non-zero exit or validation errors |
| 3 | Manifest workspace count | Exactly 5 public workspaces, 0 private workspaces | Wrong count or private workspace present |
| 4 | Worker branches | All four workers on `lab/integrated-neutrosophic-build` | Any worker on a different branch |
| 5 | Orchestrator branch | Orchestrator on `PaQBoT` | Different branch |
| 6 | Node version | `22.22.3` pinned | Any other version |

## Evidence Bundle Checks

| # | Check | Pass condition | Fail condition |
| --- | --- | --- | --- |
| 7 | Entry count | Exactly 4 entries in `evidence-index.json` | Fewer or more than 4 entries |
| 8 | Expected repos | All four slugs present: `agent-squad_case_study`, `aden_case_study`, `haystack_case_study`, `ragas_case_study` | Any slug missing or unexpected slug present |
| 9 | Commit hashes | Every entry has a non-empty `commit_sha` | Any entry missing or empty commit hash |
| 10 | Origin URLs | Every entry has a non-empty `origin` URL | Any entry missing or empty origin |
| 11 | Model recorded | Every entry records the `model` field | Any entry missing model |
| 12 | Timestamps | Every entry has `generated_at` in ISO 8601 UTC | Any entry missing or malformed timestamp |
| 13 | Required files present | All six required files exist and are non-empty | Any file missing or empty |

## Safety Checks

| # | Check | Pass condition | Fail condition |
| --- | --- | --- | --- |
| 14 | No secrets | No tokens, keys, `.env` content, or credentials in any report | Any secret-like pattern detected |
| 15 | No Windows paths | No `C:\...` or `/mnt/c/...` in any report | Any Windows path detected |
| 16 | No unresolved variables | No `${workspace}`, `${anything}` patterns | Any unresolved variable detected |
| 17 | Report paths | All report paths under `/home/ubuntu/openclaw-lab` | Any path outside VM root |
| 18 | Smoke export/ingest | `smoke_export_ingest.sh` exits 0 | Non-zero exit |

## Expected Evidence Files

```text
evidence-index.json
evidence-summary.md
orchestrator_reports/daily_lab_report.json
orchestrator_reports/daily_lab_report.md
orchestrator_reports/weekly_nss_lab_report.md
orchestrator_reports/reproducibility_appendix.md
```

## Run Classification

- **PASS**: All 18 checks pass. The run is reproducible and citable as evidence.
- **INCOMPLETE**: Checks 1-6 pass but one or more evidence bundle checks (7-13) fail. Re-run the routine. Do not cite as evidence.
- **FAIL**: Any safety check (14-18) fails or any pre-flight check (1-6) fails. The run is not valid. Consult the recovery runbook.

## Minimum Trace Required

For a run to be considered reproducible, you must retain:

1. The `evidence-index.json` from the run
2. The `evidence-summary.md` from the run
3. The orchestrator repository at the exact commit used
4. The manifest file (`openclaw_multi_agent_lab_manifest.json`) at the exact version used

With these four artifacts, an independent researcher can reconstruct the topology, toolchain, model policy, and workspace configuration needed to reproduce the run.

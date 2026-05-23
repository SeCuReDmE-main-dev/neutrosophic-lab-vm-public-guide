# Evidence Bundle Format

The evidence bundle is the public audit record for a lab run.

Expected files:

```text
evidence-index.json
evidence-summary.md
orchestrator_reports/daily_lab_report.json
orchestrator_reports/daily_lab_report.md
orchestrator_reports/weekly_nss_lab_report.md
orchestrator_reports/reproducibility_appendix.md
```

Required entry fields:

- `repo_slug`
- `run_id`
- `routine_type`
- `model`
- `commit_sha`
- `classification`
- `origin`
- `branch`
- `artifact_path`
- `generated_at`

Bundle-level fields:

- `schema_version`
- `evidence_id`
- `source_policy`
- `entries`

The evidence bundle should contain four public worker entries for a complete routine.

# Report Locations

All reports must live under the VM lab root:

```text
/home/ubuntu/openclaw-lab
```

## Canonical Report Paths

```text
/home/ubuntu/openclaw-lab/reports/daily/
/home/ubuntu/openclaw-lab/reports/weekly/
/home/ubuntu/openclaw-lab/reports/reproducibility/
/home/ubuntu/openclaw-lab/reports/latest/
```

## Scheduler Logs

```text
/home/ubuntu/openclaw-lab/logs/scheduler/
```

## Evidence Exports

```text
/home/ubuntu/openclaw-lab/exports/evidence/<run-id>/
```

## Public Workspace Exports

```text
/home/ubuntu/openclaw-lab/exports/public/<repo>/<run-id>/
```

## Host-Side Acceptance Summary

After running acceptance, a summary is available on the host at:

```text
04_VALIDATION_LAB/output/lab_acceptance/lab_acceptance_report.md
```

This is the only host-side output. All other reports are VM-side only.

## Forbidden Report Locations

Reports must not be created in:

```text
C:\...
/mnt/c/...
Windows user profile roots
Any path outside /home/ubuntu/openclaw-lab
```

If a report appears outside the VM root, it is a path safety violation. The path guard (`lab_path_guard.sh`) enforces this at the script level.

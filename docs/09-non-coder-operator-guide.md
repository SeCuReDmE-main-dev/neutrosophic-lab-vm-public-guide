# Non-Coder Operator Guide

This page is for a person who does not want to edit code. You can run the lab, check its health, read reports, and recover from common problems — all from the command line.

## What You Can Do

### Check Lab Health (10-Minute Checklist)

Run these in order from WSL inside the orchestrator repo:

1. Static audit (no VM needed):
   ```bash
   bash ./04_VALIDATION_LAB/pipeline/audit_static_lab.sh
   ```

2. Validate VM topology:
   ```bash
   bash ./04_VALIDATION_LAB/pipeline/validate_openclaw_multi_agent_lab.sh openclaw-e2e-test
   ```

3. Check active workspace process:
   ```bash
   bash ./04_VALIDATION_LAB/pipeline/active_workspace_process_status.sh openclaw-e2e-test
   ```

4. Smoke dashboard:
   ```bash
   bash ./04_VALIDATION_LAB/pipeline/smoke_dashboard.sh openclaw-e2e-test
   ```

5. Smoke model policy:
   ```bash
   bash ./04_VALIDATION_LAB/pipeline/smoke_model_policy.sh openclaw-e2e-test
   ```

6. Smoke export/ingest:
   ```bash
   bash ./04_VALIDATION_LAB/pipeline/smoke_export_ingest.sh openclaw-e2e-test
   ```

7. Confirm the latest evidence bundle has all required files (see step 7 in the 10-minute checklist).

### Run Routines

Daily routine:
```bash
bash ./04_VALIDATION_LAB/pipeline/run_public_workspace_routine.sh openclaw-e2e-test daily
```

Full acceptance:
```bash
bash ./04_VALIDATION_LAB/pipeline/run_lab_acceptance.sh openclaw-e2e-test
```

### Read Reports

Reports are inside the VM at:

```text
/home/ubuntu/openclaw-lab/reports/daily/
/home/ubuntu/openclaw-lab/reports/weekly/
/home/ubuntu/openclaw-lab/reports/reproducibility/
```

After an acceptance run, a host-side summary appears at:

```text
04_VALIDATION_LAB/output/lab_acceptance/lab_acceptance_report.md
```

## What You Should Not Do

Do not:

- edit files inside `/home/ubuntu/openclaw-lab/runtime/`
- paste tokens or secrets into GitHub issues or the VM
- move report folders into Windows user roots (`C:\Users\...`)
- push branches to upstream projects
- modify public evidence bundles manually
- run lab scripts from PowerShell or cmd.exe — use WSL only

## If Something Breaks

### Quick Diagnosis

1. Run validation:
   ```bash
   bash ./04_VALIDATION_LAB/pipeline/validate_openclaw_multi_agent_lab.sh openclaw-e2e-test
   ```

2. If validation fails, identify the problem area from the error output:
   - **Gateway/bind error**: rerun the dashboard script
   - **Workspace/process error**: check active process status, stop if needed, rerun setup
   - **Toolchain/Node version error**: run static audit, then respawn VM if mismatch
   - **Evidence error**: recreate public export and evidence bundle

### Recovery Steps by Problem Type

**Gateway drift:**
```bash
bash ./04_VALIDATION_LAB/pipeline/validate_openclaw_multi_agent_lab.sh openclaw-e2e-test
bash ./04_VALIDATION_LAB/pipeline/smoke_dashboard.sh openclaw-e2e-test
```

**Workspace or process drift:**
```bash
bash ./04_VALIDATION_LAB/pipeline/active_workspace_process_status.sh openclaw-e2e-test
bash ./04_VALIDATION_LAB/pipeline/stop_active_workspace_process.sh openclaw-e2e-test
bash ./04_VALIDATION_LAB/pipeline/setup_openclaw_multi_agent_lab.sh openclaw-e2e-test
```

**Toolchain drift (wrong Node version, missing tools):**
```bash
bash ./04_VALIDATION_LAB/pipeline/audit_static_lab.sh
bash ./04_VALIDATION_LAB/pipeline/validate_openclaw_multi_agent_lab.sh openclaw-e2e-test
```
If Node version mismatches, respawn the VM from `spawn_openclaw_lab.sh`.

**Evidence drift (missing or corrupt evidence):**
Recreate public export and evidence bundle, then rerun orchestrator reporting.

**VM corrupted or unreachable:**
```bash
multipass delete openclaw-e2e-test && multipass purge
bash ./04_VALIDATION_LAB/pipeline/setup_openclaw_multi_agent_lab.sh openclaw-e2e-test
```

### If Multipass Is Unavailable

Static audit passes independently of VM availability:
```bash
bash ./04_VALIDATION_LAB/pipeline/audit_static_lab.sh
```

Dynamic VM checks are skipped when the Multipass socket is not available. The skip reason is documented in output as: "Multipass socket not available in current terminal environment."

## Safe vs Unsafe Commands

**Safe** (can run anytime):
- `audit_static_lab.sh` — static checks, no VM needed
- `run_lab_acceptance.sh` — full acceptance suite
- `scheduler_status.sh` — read-only scheduler check

**Unsafe** (avoid unless you understand the consequences):
- Running scripts that extract reports to `C:\Users\...` or Windows `$HOME`
- Running workers continuously without the scheduler lock
- Manually editing the manifest JSON without understanding path safety policy

# VM Installation

The implementation source is:

```text
https://github.com/SeCuReDmE-main-dev/moteur-neutrosophique-adaptable
```

Branch: `PaQBoT`

## Host Requirements

- Windows host (operator surface only)
- WSL/Ubuntu as the canonical command surface
- Multipass installed and available inside WSL
- Git
- Network access to GitHub
- Enough disk and memory for one Ubuntu VM (4 CPUs, 8 GB RAM, 40 GB disk)

## WSL Is Canonical, Windows Is Operator Surface

All lab scripts are bash scripts executed from WSL. Multipass must be available inside WSL — it is not guaranteed to exist in the PowerShell host `PATH`. Windows owns the GUI browser surface used by the dashboard. The Multipass guest owns the OpenClaw runtime, gateway, browser automation, and isolated workspaces.

Do not run lab scripts from PowerShell or cmd.exe. Do not redesign scripts for native Windows execution.

## Basic Flow

From WSL:

```bash
git clone https://github.com/SeCuReDmE-main-dev/moteur-neutrosophique-adaptable.git
cd "moteur-neutrosophique-adaptable"
git checkout PaQBoT
```

Spawn and prepare the VM:

```bash
bash ./04_VALIDATION_LAB/pipeline/spawn_openclaw_lab.sh openclaw-e2e-test
bash ./04_VALIDATION_LAB/pipeline/setup_openclaw_multi_agent_lab.sh openclaw-e2e-test
```

Validate:

```bash
bash ./04_VALIDATION_LAB/pipeline/validate_openclaw_multi_agent_lab.sh openclaw-e2e-test
```

## Post-Install: Audit, Acceptance, Scheduler

After validation passes, run the static audit (no VM needed):

```bash
bash ./04_VALIDATION_LAB/pipeline/audit_static_lab.sh
```

Run full acceptance:

```bash
bash ./04_VALIDATION_LAB/pipeline/run_lab_acceptance.sh openclaw-e2e-test
```

Install the scheduler for automated daily/weekly routines:

```bash
bash ./04_VALIDATION_LAB/pipeline/install_lab_scheduler.sh openclaw-e2e-test
```

Check scheduler status:

```bash
bash ./04_VALIDATION_LAB/pipeline/scheduler_status.sh openclaw-e2e-test
```

## VM Specs (from Manifest)

| Setting | Value |
| --- | --- |
| Image | Ubuntu 24.04 |
| VM name | `openclaw-e2e-test` |
| CPUs | 4 |
| Memory | 8 GB |
| Disk | 40 GB |
| Timeout | 1800 seconds |
| Node.js | 22.22.3 (pinned) |

## Important Boundary

Use WSL for lab commands. Windows is not the canonical execution surface. The VM owns the runtime and reports. Do not look for reports in Windows user folders.

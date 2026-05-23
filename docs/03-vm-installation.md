# VM Installation

The implementation source is:

```text
https://github.com/SeCuReDmE-main-dev/moteur-neutrosophique-adaptable
```

## Requirements

- Windows host
- WSL/Ubuntu as the command surface
- Multipass
- Git
- network access to GitHub
- enough disk and memory for one Ubuntu VM

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

Run routine:

```bash
bash ./04_VALIDATION_LAB/pipeline/run_public_workspace_routine.sh openclaw-e2e-test daily
```

## Important Boundary

Use WSL for lab commands. Windows is not the canonical execution surface.

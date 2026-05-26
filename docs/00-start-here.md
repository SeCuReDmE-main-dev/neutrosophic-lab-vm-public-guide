# Start Here

This repository explains how to understand and run the public neutrosophic VM lab.

The lab is for reading, reproducing, and auditing applied neutrosophic AI case-study traces. It is not a place to submit code patches.

## The Short Version

The lab runs inside one Ubuntu VM. Inside that VM, five public workspaces are created:

- four case-study workers (Agent Squad, Aden, Haystack, Ragas)
- one orchestrator (`lab-orchestrator-public`)

The orchestrator runs routines, collects traces, and writes reports. All runtime outputs stay inside `/home/ubuntu/openclaw-lab`.

The lab also includes a prompt-governance milestone (`M3.5`) that defines how delegated analysis is assigned across the four public lanes. This is a contract and governance milestone between M3 and M4, not a claim that the full rotating prompt runtime is already live.

## The First Command To Understand

From the implementation repository (`SeCuReDmE-main-dev/moteur-neutrosophique-adaptable`, branch `PaQBoT`), the core validation command is:

```bash
bash ./04_VALIDATION_LAB/pipeline/validate_openclaw_multi_agent_lab.sh openclaw-e2e-test
```

If validation passes, the VM topology is present and the lab can be used.

## Where Reports Appear

Reports appear only under:

```text
/home/ubuntu/openclaw-lab/reports/
```

Evidence bundles appear under:

```text
/home/ubuntu/openclaw-lab/exports/evidence/
```

Do not look for reports in Windows user folders. Windows is the operator surface only.

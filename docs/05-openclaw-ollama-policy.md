# OpenClaw And Ollama Policy

The lab uses OpenClaw inside the VM and Ollama cloud models for routine execution.

## Model Policy

Routine default:

```text
ollama/gemma4:31b-cloud
```

Escalation model (used for deeper synthesis and cross-case analysis):

```text
ollama/kimi-k2.6:cloud
```

## Escalation Rules

The default model handles all routine daily work across the four case-study workers. The escalation model is reserved for:

- weekly NSS report synthesis
- cross-case comparison and pattern analysis
- reproducibility appendix generation
- manual acceptance runs

Routine daily workers do not escalate. Escalation is triggered by the orchestrator, not by individual workspace agents.

## Runtime Boundary

OpenClaw runtime state belongs inside the VM at `/home/ubuntu/openclaw-lab/runtime/`. Scheduled lab reports must not be written to Windows folders.

The VM guest owns:
- OpenClaw runtime and gateway
- browser automation
- isolated workspaces
- reports, logs, and evidence exports

The Windows host owns:
- the GUI browser surface used by the dashboard
- nothing else in the lab runtime

## Non-Goals

- No local heavyweight inference on the host machine.
- No five-VM topology.
- No five always-on app servers.
- No adaptive engine inside the VM.
- No private hub or private evidence layer.
- No direct write-back from the orchestrator into public repo source trees.
- No GitHub secret injection into the VM.

## Path Risk

OpenClaw/Ollama workflows can accidentally produce output in unexpected host paths if commands are not guarded. This lab treats path safety as a core requirement.

Forbidden examples:

```text
C:\Users\jeans\${workspace}
C:\Users\jeans\.82123456789
/mnt/c/Users/jeans
${workspace}
${anything}
```

The path guard (`lab_path_guard.sh`) enforces `lab_assert_vm_path()` and `lab_reject_windows_path()` for all report and output paths. Static audit validates forbidden prefixes (`C:`, `/mnt/c`, `${`, `C:\`) and allowed prefixes (VM root only).

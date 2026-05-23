# OpenClaw And Ollama Policy

The lab uses OpenClaw inside the VM and Ollama cloud models for routine execution.

## Model Policy

Routine default:

```text
ollama/gemma4:31b-cloud
```

Escalation model:

```text
ollama/kimi-k2.6:cloud
```

## Runtime Boundary

OpenClaw runtime state belongs inside the VM. Scheduled lab reports must not be written to Windows folders.

## Path Risk

OpenClaw/Ollama workflows can accidentally produce output in unexpected host paths if commands are not guarded. This lab treats path safety as a core requirement.

Forbidden examples:

```text
C:\Users\jeans\${workspace}
C:\Users\jeans\.82123456789
/mnt/c/Users/jeans
```

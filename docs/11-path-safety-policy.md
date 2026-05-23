# Path Safety Policy

The lab must not create scheduled outputs outside the VM lab root.

Allowed root:

```text
/home/ubuntu/openclaw-lab
```

Forbidden examples:

```text
C:\...
/mnt/c/...
C:\Users\jeans\${workspace}
C:\Users\jeans\.82123456789
${workspace}
${anything}
```

## Why This Matters

OpenClaw/Ollama workflows can accidentally create folders at unsafe host paths if a working directory or report destination is unresolved.

The lab treats unresolved variables and Windows profile paths as unsafe.

## Rule

If a path is not under `/home/ubuntu/openclaw-lab`, it is not a valid scheduled lab report path.

# What This Lab Is

This lab is a public VM-based research environment for applied neutrosophic AI experiments.

It combines four public case-study workspaces:

- Agent Squad
- Aden/Hive
- Ragas
- Haystack

It also includes one orchestrator workspace:

- `lab-orchestrator-public`

The orchestrator does not act as an unrestricted autonomous engine. Its responsibilities are bounded:

- run routines
- collect public traces
- normalize evidence
- produce reports

## Why A VM

The VM gives a stable boundary for runtime behavior. OpenClaw, Ollama, reports, logs, and workspaces live inside the guest, not scattered across Windows user folders.

## Who This Is For

This guide is written for:

- mathematicians
- software developers
- maintainers reviewing the idea
- NSS readers
- independent reviewers

It is intentionally conservative and reproducibility-oriented.

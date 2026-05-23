# What This Lab Is

This lab is a public VM-based research environment for applied neutrosophic AI experiments.

It combines four public case-study workspaces:

- Agent Squad: multi-agent response merging and orchestration analysis
- Aden/Hive: worker-report and partial-success analysis
- Ragas: evidence-triplet metric and RAG evaluation analysis
- Haystack: evaluator uncertainty, retrieval confidence, and HITL status analysis

It also includes one orchestrator workspace:

- `lab-orchestrator-public`

The orchestrator does not act as an unrestricted autonomous engine. Its responsibilities are bounded:

- run routines
- collect public traces
- normalize evidence
- produce reports (daily, weekly, reproducibility)

## Why A VM

The VM gives a stable boundary for runtime behavior. OpenClaw, Ollama, reports, logs, and workspaces live inside the guest at `/home/ubuntu/openclaw-lab`, not scattered across Windows user folders.

## Who This Is For

This guide is written for:

- mathematicians interested in applied neutrosophy
- software developers evaluating the integration approach
- maintainers reviewing the idea
- NSS readers and reviewers
- independent researchers verifying reproducibility

It is intentionally conservative and reproducibility-oriented. The lab makes a research path visible; it does not claim upstream acceptance.

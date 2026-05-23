# Lab Topology

The VM root is:

```text
/home/ubuntu/openclaw-lab
```

Workspace roots:

```text
/home/ubuntu/openclaw-lab/workspaces/agent-squad-public
/home/ubuntu/openclaw-lab/workspaces/aden-public
/home/ubuntu/openclaw-lab/workspaces/haystack-public
/home/ubuntu/openclaw-lab/workspaces/ragas-public
/home/ubuntu/openclaw-lab/workspaces/lab-orchestrator-public
```

## Worker Workspaces

The first four workspaces are public case-study workers. They are cloned from public fork repositories.

Each worker branch is:

```text
lab/integrated-neutrosophic-build
```

## Orchestrator Workspace

The fifth workspace coordinates routines and reporting. It reads public traces and creates evidence outputs.

It is not a private hub and not a general adaptive engine.

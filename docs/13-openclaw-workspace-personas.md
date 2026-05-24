# OpenClaw Workspace Personas

This page explains how the public neutrosophic VM lab uses OpenClaw-native bootstrap files to give each workspace a stable operating persona without turning the VM into an over-designed agent framework.

The current lab has five public workspaces:

- `agent-squad-public`
- `aden-public`
- `haystack-public`
- `ragas-public`
- `lab-orchestrator-public`

Each workspace receives a small bootstrap contract made of:

- `AGENTS.md`
- `SOUL.md`
- `USER.md`
- `TOOLS.md`
- `MEMORY.md`
- optional `HEARTBEAT.md`

These files are seeded deterministically into the VM workspaces during lab setup. They are treated as runtime guardrails, not literary prompts.

## Why the lab stays with OpenClaw-native files

The lab intentionally uses only the files OpenClaw already understands as workspace bootstrap surface. This keeps the behavior predictable and keeps the prompt budget small enough to stay useful.

That decision matters for three reasons.

First, the VM is a reproducibility surface. The goal is not to create five free-form personalities. The goal is to bind five public workspaces to five disciplined roles that can be re-created on every rerun.

Second, the lab already has enough moving parts:

- one Ubuntu VM
- one OpenClaw gateway
- one Ollama/OpenClaw toolchain policy
- five public workspaces
- daily and weekly reporting

Adding nonstandard runtime files would make the bootstrap harder to reason about and harder to validate.

Third, this guide is public and codeless. It describes the contract, but it does not ask readers to trust undocumented agent magic.

## Why `TODO`, `WELCOME`, and `WORKFLOW` are not first-class bootstrap files

Those file names can still exist later as support documents, but they are not part of the runtime contract in this first stable version.

The reason is simple: they do not need to be injected into OpenClaw to make the workspaces behave correctly.

Their useful content already has a proper home:

- role and outputs belong in `AGENTS.md`
- posture and limits belong in `SOUL.md`
- user expectations belong in `USER.md`
- command and path discipline belong in `TOOLS.md`
- durable facts belong in `MEMORY.md`

That keeps the persona system small, explicit, and testable.

## Common contract across all five workspaces

All five workspaces share the same high-level operating rules.

### Shared invariants

- the runtime lives inside one Ubuntu VM
- heavy work should stay one-process-at-a-time unless the lab policy changes
- no secrets are pulled into reports
- no host-private paths should appear in outputs
- evidence must remain public-safe
- abstention is preferable to fabricated certainty

### Shared user frame

The common `USER.md` describes the operator as direct, scope-sensitive, evidence-oriented, and intolerant of speculative drift. That is not a style ornament. It is a control surface. It keeps the workspaces aligned with the lab's real use: collect trace, compare evidence, report honestly, and stop when the role boundary is reached.

### Shared tool frame

The common `TOOLS.md` tells every workspace the same essential truth:

- runtime and outputs stay under `/home/ubuntu/openclaw-lab`
- host execution flows through WSL and Multipass
- Windows/local paths are not report targets
- safe commands and validation are preferred over uncontrolled mutation

This shared tool layer prevents the persona system from fragmenting into five different operational realities.

## `agent-squad-public`

### What it represents

`agent-squad-public` stands for the multi-agent response-merging and orchestration study surface. Its upstream identity is not a general judge and not the lab controller. It is the lane where different agent outputs, agent conflict, and merger behavior are observed.

### What uncertainty shape it watches

This workspace watches uncertainty that appears when multiple candidate answers compete for the same final surface.

Its main question is not "who is right forever?"  
Its question is closer to:

- when do multiple agents converge cleanly?
- when do they diverge?
- when is disagreement real signal instead of noise?
- when should ambiguity remain visible instead of being flattened too early?

This makes it the most consensus-sensitive persona in the lab.

### What outputs it should produce

The workspace should emit public-safe traces showing:

- how responses were merged
- whether disagreement stayed unresolved
- what reproducibility metadata is available
- whether the evidence supports a stable merged answer

It should not emit cross-hub comparative judgments. It contributes one lane of evidence. It does not summarize the lab.

## `aden-public`

### What it represents

`aden-public` is the governance and worker-state lane. Its role is shaped by queen, hive, worker, blocked-worker, and retry behavior.

It is the workspace most concerned with operational flow under imperfect conditions. It cares about whether work advances, stalls, partially succeeds, retries, or collapses.

### Why the persona is hive-governance oriented

This workspace is not primarily about answer quality at the report surface. It is about execution structure.

Its persona therefore emphasizes:

- worker-state tracking
- blocked execution visibility
- retry discipline
- partial success handling

This is a different uncertainty shape than `agent-squad-public`. Here the key issue is not merging several answers. It is understanding whether the system is moving work forward in a coherent way.

### What outputs it should produce

It should produce traces that expose:

- worker progress
- blocked states
- retry decisions
- partial completion versus full completion

Its reports should not fabricate success just because some substeps ran. The persona is designed to surface execution truth, not optimistic narration.

## `haystack-public`

### What it represents

`haystack-public` is the retrieval, evaluator, and human-in-the-loop lane.

This workspace is where the lab watches how a system behaves when evidence must be retrieved, passed through evaluators, and sometimes deferred to clarification or human review.

### Evaluator and HITL focus

The persona here is built around evaluator uncertainty.

That means it watches:

- ambiguous retrieval
- weak evidence handoff
- evaluator hesitation
- transitions into clarification paths
- moments where abstention is more honest than a forced decision

This workspace is especially important because it models a common real-world failure pattern: a system can look active and polished while still being epistemically weak.

### What outputs it should produce

It should produce traces that help answer:

- was the retrieved evidence actually enough?
- did evaluator logic distinguish insufficiency from contradiction?
- was human clarification properly invited when needed?
- did the pipeline expose uncertainty instead of burying it?

This lane is therefore central to the lab's larger thesis that operational success and epistemic quality are not the same thing.

## `ragas-public`

### What it represents

`ragas-public` is the metric and evidence-discipline lane. It is the workspace most explicitly tied to judged support, insufficiency, contradiction, and metric truthfulness.

### Evidence discipline

This persona is strict on one point: a score is not an argument by itself.

The workspace should keep asking:

- what evidence supports this score?
- what evidence contradicts it?
- what remains insufficiently supported?
- what does the judge know versus infer?

That makes `ragas-public` the cleanest measurement-oriented persona in the lab.

### Contradiction versus insufficiency

The distinction matters. A statement can be unsupported without being disproven. It can also be contradicted directly. Treating those as the same thing weakens the entire reporting stack.

The `ragas-public` persona is therefore engineered to preserve this difference and to keep the metric layer closer to evidence reality.

### What outputs it should produce

The workspace should emit public-safe metric traces and summaries showing:

- support level
- contradiction level
- insufficiency level
- judge confidence boundaries
- reproducibility metadata tied to the run

It does not own orchestration. It owns disciplined scoring and evidence interpretation for its lane.

## `lab-orchestrator-public`

### What it represents

`lab-orchestrator-public` is the fifth workspace and the only one allowed to produce consolidated cross-hub reports.

It is not framed as a grand adaptive engine. That is deliberate.

### Why it is not an adaptive engine

The lab deliberately narrowed this workspace to something more operationally honest:

- orchestrate the four public hubs
- collect public-safe traces
- normalize evidence
- compose comparative reports
- maintain daily and weekly reporting cadence

That scope is strong enough to make the lab useful and reproducible without pretending that a universal adaptive engine already exists.

### Why it is a control, reporting, and evidence hub

The orchestrator is where the four lanes become one auditable surface.

It exists to answer questions like:

- did all four lanes run?
- what evidence was produced?
- what is missing?
- what contradictions remain?
- what can responsibly be reported across the whole lab?

Because of that role, it is the only workspace that receives the optional `HEARTBEAT.md` in the current design. That file is useful where scheduled cadence matters. It is not needed in every workspace.

### What outputs it should produce

The orchestrator should produce:

- normalized evidence bundles
- daily comparative summaries
- weekly NSS-oriented reports
- reproducibility appendices

It should also remain conservative. If one lane is weak or missing, the orchestrator should report the weakness instead of covering it with synthetic certainty.

## Public and codeless boundary

This repository remains documentation-only.

That means:

- no code is shipped here
- no runtime artifacts are shipped here
- no VM automation is duplicated here
- no persona file contents are treated as runnable product code here

This page describes behavior and architecture boundaries only.

The implementation remains in the orchestrator repository, where the persona files are seeded, validated, and exercised against the real VM.

## Why this persona system matters

The personas are not decorative.

They are the lightest possible way to give each workspace:

- a clear role
- a clear stop condition
- a clear evidence responsibility
- a clear reporting boundary

That is why the lab can stay both expressive and testable. The personas are deep enough to shape behavior, but small enough to validate mechanically.

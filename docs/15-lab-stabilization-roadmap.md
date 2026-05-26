# Lab Stabilization Roadmap

This roadmap tracks the hardening work required before the lab can be treated as a stable, shareable, daily-running public research environment.

The roadmap is grouped into 10 milestones and 250 micro-actions. It is intentionally detailed because this lab is not being assembled from a ready-made template. The work includes architecture hardening, scheduler stabilization, evidence safety, reporting quality, and public-shareability controls.

## Milestone Schedule

| Milestone | Due Date | Focus |
| --- | --- | --- |
| `M0` | May 31, 2026 | Freeze baseline scope and tracking |
| `M1` | June 7, 2026 | Host and VM determinism |
| `M2` | June 14, 2026 | OpenClaw runtime stability |
| `M3` | June 21, 2026 | Persona and contract integrity |
| `M3.5` | June 24, 2026 | Prompt governance design and contract hardening |
| `M4` | June 28, 2026 | Daily routine readiness |
| `M5` | July 5, 2026 | Evidence safety and data quality |
| `M6` | July 12, 2026 | Weekly NSS package quality |
| `M7` | July 19, 2026 | Observability and recovery |
| `M8` | July 26, 2026 | Public shareability hardening |
| `M9` | August 2, 2026 | Daily test launch and stabilization |

## M0 — Baseline Freeze and Tracking Setup

Status: closed as a verified baseline documentation and governance freeze. This does not mean daily testing has launched or that later runtime validation milestones are complete.

- [x] M0-01 Freeze the official scope of lab v1.
- [x] M0-02 Freeze the official list of the 5 workspaces.
- [x] M0-03 Freeze the `1 VM / 1 gateway / 5 workspaces` policy.
- [x] M0-04 Freeze the `public-only workspaces` policy.
- [x] M0-05 Freeze the `WSL-primary host execution` policy.
- [x] M0-06 Freeze the manifest Node version as baseline.
- [x] M0-07 Freeze the default and escalation model policy.
- [x] M0-08 Freeze the canonical VM path structure.
- [x] M0-09 Freeze the definition of a daily test.
- [x] M0-10 Freeze the definition of a weekly NSS run.
- [x] M0-11 Freeze the definition of a shareable lab.
- [x] M0-12 Freeze the definition of public-safe evidence.
- [x] M0-13 Establish the required baseline artifact list.
- [x] M0-14 Establish the critical script list.
- [x] M0-15 Establish the critical document list.
- [x] M0-16 Establish the manual validation checkpoint list.
- [x] M0-17 Establish the automated validation checkpoint list.
- [x] M0-18 Maintain the private exhaustive TODO source.
- [x] M0-19 Maintain the milestone map.
- [x] M0-20 Maintain the tracking policy.
- [x] M0-21 Define the status format for micro-actions.
- [x] M0-22 Define the expected-proof format for micro-actions.
- [x] M0-23 Define the closure rule for one micro-action.
- [x] M0-24 Define the closure rule for one milestone.
- [x] M0-25 Define the promotion rule for `daily tests may start`.

## M1 — Host and VM Determinism

Status: closed after final verified host and VM determinism checks. The final M1 verifier passed with all mandatory runtime probes executed, including acceptance reproducibility. Daily testing is still gated. This does not mean daily testing has launched or that later runtime validation milestones are complete.

- [x] M1-01 Verify `spawn_openclaw_lab.sh` is idempotent on the host.
- [x] M1-02 Verify `setup_openclaw_multi_agent_lab.sh` is idempotent.
- [x] M1-03 Verify `validate_openclaw_multi_agent_lab.sh` detects critical drift.
- [x] M1-04 Verify `cloud-init.template.yaml` to `cloud-init.yaml` coherence.
- [x] M1-05 Verify cloud-init rendering is fully manifest-driven.
- [x] M1-06 Verify the Node `22.22.3` pin.
- [x] M1-07 Verify the expected Python runtime inside the VM.
- [x] M1-08 Verify the LibreOffice renderer pin.
- [x] M1-09 Verify `loginctl enable-linger` installation.
- [x] M1-10 Verify WSL is the only primary host surface.
- [x] M1-11 Verify PowerShell wrappers remain convenience-only.
- [x] M1-12 Verify Multipass resolution through the shared resolver.
- [x] M1-13 Verify WSL/Windows path resolution stability.
- [x] M1-14 Verify host-to-VM transfer stability.
- [x] M1-15 Verify VM-to-host transfer stability.
- [x] M1-16 Verify absence of Windows paths in public artifacts.
- [x] M1-17 Verify absence of host secrets in seeded workspaces.
- [x] M1-18 Verify the default VM name.
- [x] M1-19 Verify the default CPU, memory, and disk quotas.
- [x] M1-20 Verify the boot and setup timeout budget.
- [x] M1-21 Verify reproducibility of `audit_static_lab.sh`.
- [x] M1-22 Verify reproducibility of `run_lab_acceptance.sh`.
- [x] M1-23 Define the full VM rebuild procedure.
- [x] M1-24 Define the non-destructive reset procedure.
- [x] M1-25 Define the destroy-and-recreate procedure.

## M2 — OpenClaw Runtime Stability

Status: closed after final verified OpenClaw runtime checks. The hardened M2 verifier passed with real WSL/Multipass runtime probes and the existing dashboard/model-policy smoke scripts. Daily testing is still gated. This does not mean M3+ or daily launch milestones are complete.

- [x] M2-01 Verify gateway startup inside the VM.
- [x] M2-02 Verify expected LAN bind behavior.
- [x] M2-03 Verify `openclaw-gateway.service` status handling.
- [x] M2-04 Verify dashboard port availability.
- [x] M2-05 Verify tokenized dashboard URL emission.
- [x] M2-06 Verify gateway restart after stop.
- [x] M2-07 Verify clean shutdown of active workspace processes.
- [x] M2-08 Verify simple runtime log rotation expectations.
- [x] M2-09 Verify no zombie processes after workspace switches.
- [x] M2-10 Verify robustness of `active-process.json`.
- [x] M2-11 Verify stale gateway cleanup precision.
- [x] M2-12 Verify host wrappers do not assume a fixed OpenClaw binary path.
- [x] M2-13 Verify default model is applied to all lab agents.
- [x] M2-14 Verify escalation model is declared and visible.
- [x] M2-15 Verify non-concurrency policy for heavy workers.
- [x] M2-16 Verify the max runtime limit.
- [x] M2-17 Verify `app first, delegation second` discipline.
- [x] M2-18 Verify compatibility with systemd user scheduler.
- [x] M2-19 Verify filesystem permissions used by runtime flows.
- [x] M2-20 Verify stability of the report path resolver.
- [x] M2-21 Verify stability of the path guard.
- [x] M2-22 Verify dashboard smoke test remains non-destructive.
- [x] M2-23 Verify `smoke_model_policy.sh` remains stable.
- [x] M2-24 Define the quick gateway diagnosis procedure.
- [x] M2-25 Define the blocked worker recovery procedure.

## M3 — Persona and Contract Integrity

Status: closed after final verified persona and contract checks across host seeds and VM workspaces. The closure includes live sync and rerun-stability proof. This does not mean M4+ routine readiness is complete.

- [x] M3-01 Verify the 5 required bootstrap files exist in all 5 workspaces.
- [x] M3-02 Verify `HEARTBEAT.md` exists only in the orchestrator lane.
- [x] M3-03 Verify persona file size budgets.
- [x] M3-04 Verify absence of excessive duplication across persona files.
- [x] M3-05 Verify each `AGENTS.md` reflects the real upstream role.
- [x] M3-06 Verify each `SOUL.md` stays bounded and non-grandiose.
- [x] M3-07 Verify each `USER.md` stays stable and non-volatile.
- [x] M3-08 Verify each `TOOLS.md` contains only safe conventions.
- [x] M3-09 Verify each `MEMORY.md` contains only durable facts.
- [x] M3-10 Verify `what I watch` exists in each workspace.
- [x] M3-11 Verify `what I do not do` exists in each workspace.
- [x] M3-12 Verify `expected outputs` exists in each workspace.
- [x] M3-13 Verify `abstain/escalate conditions` exists in each workspace.
- [x] M3-14 Verify only the orchestrator claims consolidated reporting authority.
- [x] M3-15 Verify public hubs do not claim global orchestration.
- [x] M3-16 Verify persona seeds match the current manifest.
- [x] M3-17 Verify persona sync from host to VM.
- [x] M3-18 Verify persona stability on rerun.
- [x] M3-19 Verify no persona file leaks secrets.
- [x] M3-20 Verify no persona file leaks private paths.
- [x] M3-21 Define the controlled persona modification procedure.
- [x] M3-22 Define the persona drift audit procedure.
- [x] M3-23 Define the persona change acceptance procedure.
- [x] M3-24 Define the `persona contract green` gate.
- [x] M3-25 Define the `orchestrator authority green` gate.

Closed now at M3:

- all five required persona bootstrap files verified across all five workspaces
- `HEARTBEAT.md` restricted to the orchestrator lane only
- role, boundary, and section structure verified across persona files
- no secret leakage and no private-path leakage in persona files
- host-to-VM persona sync verified
- rerun stability verified after proof hardening
- controlled modification, drift audit, change acceptance, and green-gate procedures defined

Still true after M3 closure:

- M3 closes persona and contract integrity only
- daily testing remains gated
- M4+ routine readiness, evidence quality, and operational cycles remain later milestones

## M3.5 — Prompt Governance Design and Contract Hardening

Status: design and contract hardening closed. The live assignment engine, execution logger, orchestrator runtime observer, and operational ten-day/twenty-eight-day cycles are planned implementation work, not yet live.

This milestone was added to bridge the gap between M3 persona integrity and M4 daily routine readiness. It closes the governance question first so later runtime work has one public-safe contract surface to implement against.

- [x] M3.5-01 Define orchestrator-owned prompt governance scope.
- [x] M3.5-02 Define the seven shared prompt families and three lane-specific families per lane.
- [x] M3.5-03 Design the master prompt registry (40 prompts, 10 per lane, 7 shared + 3 specific).
- [x] M3.5-04 Draft the forty concrete prompt texts across all four lanes.
- [x] M3.5-05 Define the daily assignment algorithm (round-robin with seven-day cooldown).
- [x] M3.5-06 Define the ten-day full-coverage rule per lane.
- [x] M3.5-07 Define the orchestrator runtime observation protocol.
- [x] M3.5-08 Define weekly trend analysis and monthly twenty-eight-day recomposition.
- [x] M3.5-09 Define the integration contract with the routine contract model.
- [x] M3.5-10 Define M3.5 validation criteria and closure gate.

Closed now at M3.5:

- orchestrator-owned authority model
- prompt catalog structure
- assignment and anti-repeat rules
- weekly and monthly signal-flow design
- integration contract with daily and weekly routine contracts
- public-safe wording for boundaries and maturity

Still remaining after M3.5:

- runtime assignment
- execution logging
- runtime observation
- real ten-day trial evidence
- weekly and monthly prompt-governance operational outputs

- [ ] M3.5-11 Build the live daily assignment engine.
- [ ] M3.5-12 Build the execution logging infrastructure.
- [ ] M3.5-13 Build the orchestrator runtime observer.
- [ ] M3.5-14 Run a ten-day trial cycle with real lane execution.
- [ ] M3.5-15 Build the weekly trend analysis pipeline.
- [ ] M3.5-16 Build the NSS integration pipeline for prompt-governance signals.
- [ ] M3.5-17 Complete the first twenty-eight-day recomposition cycle.
- [ ] M3.5-18 Verify prompt-governance signals feed into weekly and monthly synthesis.
- [ ] M3.5-19 Verify lane outputs remain lane-local under prompt governance.
- [ ] M3.5-20 Verify cross-lane synthesis remains exclusively orchestrator-owned.

## M4 — Daily Routine Readiness

- [ ] M4-01 Verify the routine registry covers all 5 workspaces.
- [ ] M4-02 Verify the 5-block daily model per app.
- [ ] M4-03 Verify the target duration per block.
- [ ] M4-04 Verify the 10-second cooldown between blocks.
- [ ] M4-05 Verify block 1 pass criteria.
- [ ] M4-06 Verify block 2 pass criteria.
- [ ] M4-07 Verify block 3 pass criteria.
- [ ] M4-08 Verify block 4 skip/abstain rule.
- [ ] M4-09 Verify block 5 retry/alternate logic.
- [ ] M4-10 Verify per-app daily state file production.
- [ ] M4-11 Verify normalized payload production per app.
- [ ] M4-12 Verify `daily_contract_matrix.json` production.
- [ ] M4-13 Verify `daily_delegation_log.json` production.
- [ ] M4-14 Verify `daily_failure_register.md` production.
- [ ] M4-15 Verify each app proves a real behavior.
- [ ] M4-16 Verify agents never replace proof of app health.
- [ ] M4-17 Verify delegation starts only after health pass.
- [ ] M4-18 Verify delegated tasks are coherent per app.
- [ ] M4-19 Verify timeout budgets per app.
- [ ] M4-20 Verify sequential execution order across the 4 public apps.
- [ ] M4-21 Verify resistance to a partial lane.
- [ ] M4-22 Verify daily orchestrator report production.
- [ ] M4-23 Define the `daily test launch gate` checklist.
- [ ] M4-24 Define the `daily test minimum supervision` checklist.
- [ ] M4-25 Define the official daily start cadence.

## M5 — Evidence Safety and Data Quality

- [ ] M5-01 Verify production of `evidence-index.json`.
- [ ] M5-02 Verify production of `evidence-summary.md`.
- [ ] M5-03 Verify presence of the 4 expected public entries.
- [ ] M5-04 Verify presence of `routine_type`.
- [ ] M5-05 Verify presence of `repo_slug`.
- [ ] M5-06 Verify presence of `branch`.
- [ ] M5-07 Verify presence of `commit`.
- [ ] M5-08 Verify presence of timestamps.
- [ ] M5-09 Verify presence of artifact paths.
- [ ] M5-10 Verify presence of classification.
- [ ] M5-11 Verify presence of pass/fail/partial status fields.
- [ ] M5-12 Verify abstention reasons are present when needed.
- [ ] M5-13 Verify no secrets exist in evidence bundles.
- [ ] M5-14 Verify no Windows paths exist in evidence bundles.
- [ ] M5-15 Verify no non-public files are exported.
- [ ] M5-16 Verify coherence between evidence bundles and orchestrator reports.
- [ ] M5-17 Verify safety of `scan_report_safety.sh`.
- [ ] M5-18 Verify safety of `export_public_workspace_run.sh`.
- [ ] M5-19 Verify safety of `aggregate_public_evidence.sh`.
- [ ] M5-20 Verify safety of the private ingest flow.
- [ ] M5-21 Define the minimum quality threshold for one daily bundle.
- [ ] M5-22 Define the minimum quality threshold for one weekly bundle.
- [ ] M5-23 Define rejected-bundle motifs.
- [ ] M5-24 Define bundle retention strategy.
- [ ] M5-25 Define controlled purge strategy.

## M6 — Weekly NSS Package Quality

- [ ] M6-01 Verify `weekly_nss_lab_report.json` production.
- [ ] M6-02 Verify `weekly_nss_lab_report.md` production.
- [ ] M6-03 Verify `weekly_nss_lab_report.doc` production.
- [ ] M6-04 Verify `weekly_nss_lab_report.pdf` production.
- [ ] M6-05 Verify `weekly_reproducibility_audit.md` production.
- [ ] M6-06 Verify `weekly_cross_lane_findings.md` production.
- [ ] M6-07 Verify `weekly_package_index.json` production.
- [ ] M6-08 Verify the `nss-template-v1` mapping.
- [ ] M6-09 Verify LibreOffice renderer integrity.
- [ ] M6-10 Verify fallback behavior if the renderer is absent.
- [ ] M6-11 Verify `.doc` failure signaling.
- [ ] M6-12 Verify `.pdf` failure signaling.
- [ ] M6-13 Verify structural quality of canonical Markdown.
- [ ] M6-14 Verify structural quality of canonical JSON.
- [ ] M6-15 Verify alignment with `NSS-paper-template.doc`.
- [ ] M6-16 Verify inter-lane summary quality.
- [ ] M6-17 Verify contradiction and ambiguity section quality.
- [ ] M6-18 Verify reproducibility section quality.
- [ ] M6-19 Verify next-actions section quality.
- [ ] M6-20 Verify repeatability across two weekly runs.
- [ ] M6-21 Verify stability of alternate weekly scenarios.
- [ ] M6-22 Define the `weekly NSS green` gate.
- [ ] M6-23 Define the `weekly package partial but honest` gate.
- [ ] M6-24 Define the `weekly package rejected` gate.
- [ ] M6-25 Define weekly package archive strategy.

## M7 — Observability and Recovery

- [ ] M7-01 Verify daily scheduler logs.
- [ ] M7-02 Verify weekly scheduler logs.
- [ ] M7-03 Verify gateway logs.
- [ ] M7-04 Verify active worker logs.
- [ ] M7-05 Verify public export logs.
- [ ] M7-06 Verify evidence aggregation logs.
- [ ] M7-07 Verify NSS packaging logs.
- [ ] M7-08 Verify systemd user timer status visibility.
- [ ] M7-09 Verify visibility of recent runs.
- [ ] M7-10 Verify status reporting for the last daily run.
- [ ] M7-11 Verify status reporting for the last weekly run.
- [ ] M7-12 Verify status reporting for the last acceptance run.
- [ ] M7-13 Verify detection of a timer that stops firing.
- [ ] M7-14 Verify detection of a worker over budget.
- [ ] M7-15 Verify detection of a lane that stops emitting evidence.
- [ ] M7-16 Verify detection of a missing report.
- [ ] M7-17 Define the `daily failed before evidence` runbook.
- [ ] M7-18 Define the `daily partial evidence only` runbook.
- [ ] M7-19 Define the `weekly package incomplete` runbook.
- [ ] M7-20 Define the `dashboard unavailable` runbook.
- [ ] M7-21 Define the `OpenClaw gateway restart required` runbook.
- [ ] M7-22 Define the `renderer missing` runbook.
- [ ] M7-23 Define the `persona drift detected` runbook.
- [ ] M7-24 Define the `public shareability broken` runbook.
- [ ] M7-25 Define the signal-to-action escalation matrix.

## M8 — Public Shareability Hardening

- [ ] M8-01 Verify public `README.md` coherence with the private repo.
- [ ] M8-02 Verify coherence of the public topology guide.
- [ ] M8-03 Verify coherence of the public installation guide.
- [ ] M8-04 Verify coherence of the public routines guide.
- [ ] M8-05 Verify coherence of the public personas guide.
- [ ] M8-06 Verify coherence of the public evidence guide.
- [ ] M8-07 Verify coherence of the public safety guide.
- [ ] M8-08 Verify coherence of the public reproducibility guide.
- [ ] M8-09 Maintain this full public roadmap.
- [ ] M8-10 Maintain the GitHub Projects and Milestones usage guide.
- [ ] M8-11 Verify the public repo remains free of runtime code.
- [ ] M8-12 Verify the public repo exposes no secrets.
- [ ] M8-13 Verify the public repo promises no support.
- [ ] M8-14 Verify the public repo does not present itself as upstream.
- [ ] M8-15 Verify public branch descriptions remain honest.
- [ ] M8-16 Verify operational constraints are explicit in public docs.
- [ ] M8-17 Verify public limitations are explicit.
- [ ] M8-18 Verify the public/private boundary is explicit.
- [ ] M8-19 Verify `Start Here` is sufficient for an external reader.
- [ ] M8-20 Define the `public guide coherent` gate.
- [ ] M8-21 Define the `public guide safe to share` gate.
- [ ] M8-22 Define the `public roadmap safe to expose` gate.
- [ ] M8-23 Define the public guide update policy.
- [ ] M8-24 Define the private/public drift policy.
- [ ] M8-25 Define the external-share review procedure.

## M9 — Daily Test Launch and Stabilization

- [ ] M9-01 Verify all M0–M4 gates are green before real daily launch.
- [ ] M9-02 Verify daily artifacts are readable without hunting.
- [ ] M9-03 Verify weekly artifacts are readable without hunting.
- [ ] M9-04 Verify the orchestrator summarizes all 4 lanes correctly.
- [ ] M9-05 Verify one failed lane does not make the final report lie.
- [ ] M9-06 Verify the dashboard remains optional for core operation.
- [ ] M9-07 Verify timers are installed.
- [ ] M9-08 Verify timers survive logout.
- [ ] M9-09 Verify the latest daily run respects the 5 blocks per app.
- [ ] M9-10 Verify the latest weekly run respects the full NSS package contract.
- [ ] M9-11 Verify real execution times stay within an acceptable envelope.
- [ ] M9-12 Verify an operator can diagnose a problem in under 10 minutes.
- [ ] M9-13 Verify the documentation is enough to relaunch the lab after a pause.

## Related Documentation

For the public explanation of what M3.5 added and what remains after it, see:

- `17-prompt-governance-m3-5.md`
- [ ] M9-14 Verify the lab can be presented without improvised explanation.
- [ ] M9-15 Verify the public surface reflects the real current state.
- [ ] M9-16 Define the official moment to begin daily tests.
- [ ] M9-17 Define the weekly review cadence.
- [ ] M9-18 Define the documentation maintenance cadence.
- [ ] M9-19 Define the acceptance revalidation cadence.
- [ ] M9-20 Define the bundle and log cleanup cadence.
- [ ] M9-21 Define the weekly proof package to publish.
- [ ] M9-22 Define the minimum package to show to an NSS reader.
- [ ] M9-23 Define the final criterion for `lab shareable`.
- [ ] M9-24 Define the final criterion for `lab stable with minimal human overview`.
- [ ] M9-25 Define the final criterion for `solidification phase complete`.

## How to Read This Roadmap

- A checked box means the task is closed in the private source of truth.
- Milestones track phase completion.
- The GitHub Project visualizes current flow, blocked work, and time-oriented views.
- The public guide explains the work. It is not a support desk and not a software contribution venue.

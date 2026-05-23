# Maintainer And Researcher Notes

This lab is designed to make an applied research path visible, not to ask upstream maintainers to accept changes.

## For Maintainers

The lab branches are fork-only public builds on `SeCuReDmE-main-dev/*_case_study` repositories. They do not imply upstream approval.

If you maintain one of the upstream projects (Agent Squad, Aden/Hive, Ragas, Haystack), this repository is not asking you to review a PR or triage an issue. The lab branches exist for reproducibility, not as contribution requests.

## For Researchers

Use the evidence bundle to inspect:

- which repository was tested (`repo_slug`, `origin`)
- which branch was used (`branch`)
- which commit was used (`commit_sha`)
- which model was used (`model`)
- which routine was run (`routine_type`: daily, weekly, or manual_acceptance)
- when the artifact was generated (`generated_at`, ISO 8601 UTC)

The evidence bundle is the primary reproducibility artifact. Each entry links a specific commit to a specific model and routine. This allows independent verification: clone the same repo at the same commit, run the same routine with the same model, and compare outputs.

## Academic Framing

The lab explores how neutrosophic truth, indeterminacy, and falsity concepts can be represented in real AI software systems. The central finding across the four case studies is that the indeterminacy dimension `I` is the most informative part of the triplet but also the least portable — it changes shape according to the host system's decision surface:

- In Agent Squad: routing ambiguity and unresolved response fusion
- In Aden/Hive: incomplete, blocked, or contradictory worker reports
- In Ragas: missing, ambiguous, or insufficient evidence for a generated answer
- In Haystack: evaluator row status, retrieval confidence, and HITL decision semantics

## Citation

When citing this work, reference:

- The NSS case study article: "Applied Neutrosophic Triplets in AI Decision Systems" (Beaulieu, 2026)
- The public lab repository: `SeCuReDmE-main-dev/neutrosophic-lab-vm-public-guide`
- The implementation repository: `SeCuReDmE-main-dev/moteur-neutrosophique-adaptable` (branch `PaQBoT`)
- Author ORCID: https://orcid.org/0009-0007-2904-0443

## Scope Limitations

This lab does not:

- Claim that any upstream project has accepted neutrosophic integration
- Expose the private adaptive engine design
- Provide a universal neutrosophic subsystem for all AI projects
- Replace upstream testing, review, or governance processes

The public evidence is intentionally narrow: four case-study surfaces, one VM, one gateway, reproducible traces. The private engine remains outside the public manuscript and outside this repository.

## Reproducibility

All evidence bundles are designed for independent verification. The manifest (`openclaw_multi_agent_lab_manifest.json`) defines the exact VM, toolchain, model, and workspace configuration. The pipeline scripts are deterministic: same inputs produce same topology. The rerun policy (deterministic-reset) ensures that lab agents are recreated identically on each run.

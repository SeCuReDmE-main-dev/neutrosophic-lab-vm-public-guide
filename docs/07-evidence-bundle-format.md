# Evidence Bundle Format

The evidence bundle is the public audit record for a lab run. It is written to:

```text
/home/ubuntu/openclaw-lab/exports/evidence/<run-id>/
```

This page describes the public evidence contract that exists now. It also notes where M3.5 prompt-governance signals fit once the runtime pieces become live.

## Required Files (Complete Bundle)

A complete evidence bundle must contain all six files:

| File | Required | Description |
| --- | --- | --- |
| `evidence-index.json` | Yes | Normalized index of all evidence entries |
| `evidence-summary.md` | Yes | Human-readable summary of the run |
| `orchestrator_reports/daily_lab_report.json` | Yes | Machine-readable daily report |
| `orchestrator_reports/daily_lab_report.md` | Yes | Human-readable daily report |
| `orchestrator_reports/weekly_nss_lab_report.md` | Yes | Weekly NSS-style synthesis (for weekly runs) |
| `orchestrator_reports/reproducibility_appendix.md` | Yes | Reproducibility trace for audit |

The six files above remain the required public bundle surface after M3.5. Prompt governance does not add new mandatory public files yet.

## Required Entry Fields (evidence-index.json)

Each entry in `evidence-index.json` must include all of:

| Field | Required | Description |
| --- | --- | --- |
| `repo_slug` | Yes | Repository identifier (e.g., `agent-squad_case_study`) |
| `run_id` | Yes | Unique identifier for this run |
| `routine_type` | Yes | `daily`, `weekly`, or `manual_acceptance` |
| `model` | Yes | Model used (e.g., `ollama/gemma4:31b-cloud`) |
| `commit_sha` | Yes | Full Git commit hash of the workspace at run time |
| `classification` | Yes | `public` |
| `origin` | Yes | Full GitHub origin URL |
| `branch` | Yes | Branch name (e.g., `lab/integrated-neutrosophic-build`) |
| `artifact_path` | Yes | Path to the exported artifact relative to exports root |
| `generated_at` | Yes | ISO 8601 UTC timestamp |

## Bundle-Level Fields (evidence-index.json)

| Field | Required | Description |
| --- | --- | --- |
| `schema_version` | Yes | Version of the evidence bundle schema |
| `evidence_id` | Yes | Unique identifier for this bundle |
| `source_policy` | Yes | `public-safe-source` or `public-evidence-source` |
| `entries` | Yes | Array of evidence entries |

## Prompt-Governance Signal Status

M3.5 added a prompt-governance contract layer to the lab, but the live assignment engine, execution logger, and trend-analysis runtime are not yet operating.

What is true now:

- the orchestrator owns the prompt-governance design
- prompt-assignment and prompt-execution structures are defined at the contract layer
- weekly and monthly prompt-governance signal flow is defined at the contract layer

What is not yet required in the public bundle:

- a standalone prompt-assignment file
- a standalone prompt-execution log
- a mandatory weekly prompt-governance trend report

Until the runtime implementation is live, public evidence bundles should be interpreted as app-contract and reporting evidence first. Prompt-governance signals become required public evidence only after the assignment and logging surfaces are actually operating.

## Complete Run Criteria

A run is **complete** when:

1. `evidence-index.json` contains exactly four entries (one per public case-study workspace).
2. The four expected `repo_slug` values are present: `agent-squad_case_study`, `aden_case_study`, `haystack_case_study`, `ragas_case_study`.
3. All six required files exist and are non-empty.
4. Every entry has a non-empty `commit_sha`, `origin`, `branch`, and `generated_at`.
5. No entry contains forbidden path patterns (`C:`, `/mnt/c`, `${`, `C:\`).

M3.5 does not change the complete-run rule above. A bundle does not become incomplete simply because prompt-governance runtime artifacts are not present yet.

A run is **incomplete** if:

- Fewer than four entries in `evidence-index.json`.
- Any required file is missing or empty.
- Any entry is missing a required field.
- Any entry contains a forbidden path pattern.
- The `smoke_export_ingest.sh` check fails.

Incomplete runs should not be cited as evidence. Re-run the routine or consult the recovery runbook.

## Forbidden Content

Evidence entries must not contain:

- `.env` files, tokens, private keys, or credentials
- Personal Windows paths (`C:\Users\...`, `/mnt/c/Users/...`)
- Unresolved variable paths (`${workspace}`, `${anything}`)
- Orchestrator reports written back into public repo source trees

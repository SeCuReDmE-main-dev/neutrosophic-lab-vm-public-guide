# Non-Coder Operator Guide

This page is for a person who does not want to edit code.

## What You Can Do

You can run:

```bash
bash ./04_VALIDATION_LAB/pipeline/validate_openclaw_multi_agent_lab.sh openclaw-e2e-test
bash ./04_VALIDATION_LAB/pipeline/run_public_workspace_routine.sh openclaw-e2e-test daily
```

You can read reports under:

```text
/home/ubuntu/openclaw-lab/reports/
```

## What You Should Not Do

Do not:

- edit files inside `/home/ubuntu/openclaw-lab/runtime/`
- paste tokens into GitHub issues
- move report folders into Windows user roots
- push branches to upstream projects
- modify public evidence bundles manually

## If Something Breaks

Run validation again. If validation fails, use the implementation repository recovery guide.

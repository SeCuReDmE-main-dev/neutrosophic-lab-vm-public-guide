# Reproducibility Checklist

Before using a report as evidence, confirm:

- the VM validation passed
- the manifest has five public workspaces
- the four worker branches are `lab/integrated-neutrosophic-build`
- the evidence bundle has four entries
- each entry has a commit hash
- each entry has an origin URL
- each entry records the model
- report paths are under `/home/ubuntu/openclaw-lab`
- no secrets appear in reports
- no Windows user path appears in reports

## Expected Evidence Files

```text
evidence-index.json
evidence-summary.md
daily_lab_report.md
weekly_nss_lab_report.md
reproducibility_appendix.md
```

If any of these are missing, treat the run as incomplete.

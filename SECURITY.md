# Security Policy

## Do Not Submit Secrets

Do not paste into this repository or any associated VM:

- GitHub tokens
- OpenAI or Ollama credentials
- private keys (SSH, GPG, or otherwise)
- `.env` files
- VM snapshots containing credentials
- browser profiles
- local OpenClaw state with secrets
- personal Windows paths (e.g., `C:\Users\...`, `/mnt/c/Users/...`)

## If a Secret Is Accidentally Committed

1. Revoke the credential immediately at the provider (GitHub, Ollama, OpenAI, etc.).
2. Rotate any downstream tokens or keys that shared the same scope.
3. Do not attempt to rewrite public Git history — the secret is already exposed. Revocation is the only reliable mitigation.
4. If the secret was a GitHub personal access token, check the token's audit log for unauthorized access during the exposure window.

## Vulnerability Reports

This repository does not accept vulnerability triage for upstream projects. Security reports for Agent Squad, Aden/Hive, Ragas, Haystack, OpenClaw, Ollama, Multipass, or Ubuntu must go to their respective maintainers.

## Scope of Responsibility

This repository is documentation-only. It provides no runtime environment, no hosted service, and no authentication surface. The security boundary of the lab is the VM guest at `/home/ubuntu/openclaw-lab`. The host (Windows) is an operator surface only and is outside the documented security perimeter.

## Path Safety

The lab enforces path guards that reject:

- `C:\...` and `C:\Users\...`
- `/mnt/c/...`
- Unresolved variable paths (`${workspace}`, `${anything}`)
- Suspicious dot-directory roots under user profiles

All scheduled outputs must resolve under `/home/ubuntu/openclaw-lab`. Reports written outside this root are considered a path safety violation.

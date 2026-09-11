# Contributing

How to contribute to software in the `journeyoflife-org` organization. This is
the organization-wide default; where a repository has its own `CONTRIBUTING.md`,
that file is authoritative for it and overrides anything here.

## What this code is

Infrastructure and application source for a Catholic digital mission platform.
It runs production services handling donation records and special category
personal data under GDPR Article 9 (religious affiliation). Compliance is not a
final step: PCI-DSS, GDPR, SOC 2 Type II and ISO/IEC 27001:2022 controls are
enforced in the pipelines and in branch protection.

## Ground rules

1. **Never commit secrets.** No API keys, tokens, passwords, private keys,
   certificates with matching keys, or credential-bearing connection strings —
   including in examples, tests and fixtures. Configuration secrets live in
   Ansible Vault, Proxmox cloud-init or Vaultwarden. GitHub Actions secrets hold
   CI-scoped tokens only, never application secrets.
2. **Never pass credentials as command-line arguments.** Shell history leaks
   them. Read from a vault or an env file at runtime.
3. **Never put personal or parishioner data in an issue, PR, commit message, log
   or test fixture.** Use synthetic values.
4. **Do not disable a gate to make a check pass.** Suppressing a finding needs a
   written justification in the PR and, where the check is policy-as-code, an
   entry in the relevant ignore file.
5. **Do not merge your own pull request on a protected branch.** `main` requires
   review; squash-merge only; signed commits are mandatory.

## Workflow

```
issue → branch → pull request → review → squash-merge to main
```

1. **Open an issue first.** Production changes require a change record with a
   rollback plan before code is written. Use the repository's change-request
   form where one exists.
2. **Branch from `main`** with the naming convention
   `feature/JOL-XXXX-short-description`, `fix/...`, `docs/...` or
   `chore/...`.
3. **Install the pre-commit hooks** in your checkout:
   `pre-commit install`. They run secret scanning and linters locally; CI runs
   the same checks and cannot be satisfied by a local skip.
4. **Sign your commits.** Unsigned commits are rejected by branch protection.
5. **Open a pull request** and complete every section of the template,
   including the rollback plan. Incomplete rollback sections are a review
   rejection, not a nitpick.
6. **Keep changes focused.** One logical change per pull request. Do not
   reformat unrelated files; it destroys reviewability and blame.

## Tooling expectations

Validate what you changed, using the pinned versions recorded in the repository:

| Change touches | Run |
|----------------|-----|
| Terraform | `terraform fmt -recursive`, `terraform validate`, `tflint`, `checkov`, `tfsec` |
| Kubernetes manifests | `kubectl apply --dry-run=server`, `kubeval`, policy tests |
| Helm charts | `helm lint`, `helm template` diff against the affected environments |
| Python | `ruff`, `mypy`, `pytest`, `bandit` |
| YAML anywhere | `yamllint` with the repository config |
| Ansible | `ansible-lint`, `ansible-playbook --check --diff` |
| Shell | `shellcheck` |

`make help` in a repository lists its actual targets; prefer them to ad-hoc
commands.

## Cross-repository impact

Repositories are not independent. If a change alters a shared contract — a data
model, an API, an event schema, a secret name, a network port — the pull request
description must name the downstream repositories affected, and the change must
be coordinated with them. Cross-VLAN or cross-trust-boundary changes require an
architecture decision record before merge.

Church-platform and marketplace codebases are separate audit surfaces. Code is
not moved between them without a data protection impact assessment.

## Documentation

Every change that alters behaviour updates the matching document: the ADR if a
decision changed, the runbook if an operational procedure changed, the server
note if a host fact changed, and `CHANGELOG.md` for anything reaching
production. A change that cannot be described without inventing a new term is
usually a change in the wrong place.

## Review

Reviewers check for security impact, compliance impact, cross-repository impact
and a workable rollback, in that order, before style. Answer review comments
with evidence — a command and its output — rather than assertion.

## Getting help

See [SUPPORT.md](SUPPORT.md). For security issues use [SECURITY.md](SECURITY.md)
and do not open a public issue.

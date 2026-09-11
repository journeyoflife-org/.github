# Security Policy

Guidance for reporting security vulnerabilities in software published by the
**Journey Of Life (JOL)** organization. This file is the organization-wide
default and applies to every repository owned by `journeyoflife-org`. A
repository that ships its own `SECURITY.md` follows that file instead.

## Scope

**In scope**

- Source, configuration and deployment definitions in `journeyoflife-org` repositories
- Publicly reachable services operated from that source
- The AI service estate (inference, retrieval and tool servers) and its network boundaries

**Out of scope**

- Repositories owned by the separate `jolarca-dev` organization. That is a distinct
  commercial environment with its own governance and disclosure channel
  (ISO/IEC 27001:2022 A.8.13, segregation of networks and environments).
- Third-party components themselves — report the affected version and we will
  coordinate upstream.

## Supported versions

The platform is delivered from the current `main` branch of each repository.
Security fixes are merged to `main` and deployed promptly; aged feature branches
are not separately supported. Because this is a single-tenant production estate
rather than distributed software, there is no release-version matrix.

## Reporting a vulnerability

**Do not open a public issue, discussion or pull request for a security problem.**
Public reports expose pilgrims, parishes and donors to risk before a fix exists.

1. **Email** — `security@journeyoflife.org`
2. **GitHub private security advisory** — use *Report a vulnerability* on the
   Security tab of the affected repository. This creates a private thread with
   the maintainers and is the preferred channel when the repository is known.

Mark the message **P1** if it enables access to personal data, donation or
payment flows, or crosses a network trust boundary.

### What to include

- Description of the vulnerability and its class
- Affected repository and component, with commit or release identifier
- Step-by-step reproduction, or a proof-of-concept that does not touch live data
- Assessed impact and exploitability
- Suggested remediation, if you have one

Please allow time for a fix before disclosing publicly. We commit to the response
times below and will keep you informed of progress.

### Response times

| Severity | First response | Resolution target |
|----------|----------------|-------------------|
| **P1 — Critical** | 4 hours | 24 hours |
| **P2 — High** | 24 hours | 7 days |
| **P3 — Medium** | 72 hours | 30 days |

## Personal data and lawful basis

The platform processes **special category data under GDPR Article 9** — religious
affiliation of parishioners — together with donation records subject to PCI-DSS.

- Reports must **not** include real parishioner, pilgrim or donor data. Use
  synthetic values.
- If a report indicates that personal data has been exposed, we assess it as a
  potential personal data breach under **GDPR Article 33** and notify the
  competent supervisory authority within **72 hours of awareness** where the
  threshold is met, recording nature, categories, likely consequences and
  remediation.
- Concerns about the welfare of a person are handled outside this technical
  process through the appropriate safeguarding channel; send them to the same
  address and we will route them.

## How the platform is defended

Stated at a level suitable for a public document; no internal addressing,
topology detail or access information is published here.

- **Hosting** — the platform runs entirely on organization-owned local servers
  (bare metal plus Proxmox VE). There is no public-cloud control plane.
- **Secrets** — Ansible Vault for configuration secrets, Proxmox cloud-init for
  host provisioning, Vaultwarden for runtime secrets. No credentials in
  repositories, images or CI variables beyond short-lived tokens.
- **Network** — default-deny host firewalls with segmented VLANs separating the
  inference estate, other AI services and management access; cross-segment
  traffic requires an approved architecture decision.
- **Change control** — protected branches requiring pull-request review,
  code-owner approval, signed commits and linear history, per SOC 2 CC8.1.
- **Commit hygiene** — pre-commit and CI secret scanning (TruffleHog,
  git-secrets) plus static analysis (Bandit, Checkov, tfsec, OPA, Qodana).
- **Integrity and recovery** — AIDE file-integrity monitoring and encrypted,
  scheduled backups with tested restore drills.
- **AI runtime** — inference servers expose no public endpoint; tool servers run
  over stdio with audited invocations and an append-only audit log.

## Bug bounty

There is no paid bug bounty program. This is a charitable mission platform; we
are grateful for coordinated disclosure and will credit reporters on request.

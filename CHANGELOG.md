# Changelog

Notable changes to the organization-wide community-health defaults held in this
repository. Dates are ISO 8601. The change record for each entry is the linked
GitHub issue, which carries the risk assessment and rollback plan required by
SOC 2 CC8.1.

## 2026-10-15 — Contact channels corrected to channels that deliver

**Change record:** journeyoflife-org/.github#7

Every role mailbox this repository published lives on `journeyoflife.org`, which
has a null MX record (`MX 0 .`, RFC 7505) on Afternic parking nameservers: the
domain disavows mail, so a report sent to it is rejected at SMTP time. Private
vulnerability reporting was enabled on all 40 public repositories in the
organization in the same pass, which makes the advisory channel the only one with
an audit trail. Authority for the mapping: `journeyoflife-org/jol-control` →
`policy/contact-channels.yml`.

### Changed

- `SECURITY.md` — private security advisory is now channel 1 and e-mail channel 2,
  reversing an order that led with an address which cannot receive. The replacement
  address is a role-labelled filter on the single maintainer mailbox, stated as such
  rather than as a separate security function.
- `SECURITY.md` — the change-control bullet no longer claims pull-request review
  and code-owner approval. Both are configured but not enforced while the project has
  one maintainer; signed commits, linear history, and blocked force-push and deletion
  are what is actually enforced on `main`. An advertised control that fails on first
  test costs credibility for every other assertion in the pack.
- `SUPPORT.md`, `CODE_OF_CONDUCT.md` — same address correction. The enforcement
  section now states the conflict of interest openly: a report about the maintainer
  cannot be reviewed independently here, and welfare matters are referred to
  safeguarding authorities and civil law, which are external to this project.

Not changed, deliberately: the `https://journeyoflife.org/donate` links in
`SUPPORT.md`, `.github/FUNDING.yml` and `.github/ISSUE_TEMPLATE/config.yml`. That
domain is parked — it serves a 114-byte redirect to `/lander` — and
`journeyoflife.eu` is parked too. No working donation endpoint exists anywhere in
the organization, so the correct destination is an owner decision, not a guess.
Registered as S1-004 in the jol-control findings register.

## 2026-09-12 — Organization defaults established

**Change record:** journeyoflife-org/jol-infrastructure#54

Populated this repository, which previously contained a single stub README, and
applied branch protection to `main`.

### Added

- `SECURITY.md` — organization-wide vulnerability reporting policy: private
  advisory and mail channel, P1/P2/P3 response and resolution times, GDPR
  Article 33 breach handling, Article 9 special-category expectations, explicit
  in/out of scope including the separate `jolarca-dev` organization.
  Becomes the effective security policy for `jol-hub`, `jol-compliance` and
  `jol-domain-taxonomy`, which had none.
- `CODE_OF_CONDUCT.md` — Contributor Covenant 2.1 adapted for faith-based
  service contexts, with enforcement contact and safeguarding referral.
  Previously present in only 2 of 29 repositories.
- `SUPPORT.md` — support channels and their limits. Previously absent from the
  entire fleet.
- `CONTRIBUTING.md` — contribution contract: secret handling, credentials never
  as CLI arguments, signed commits, squash-merge, change records, per-layer
  validation expectations, cross-repository impact duty.
- `profile/README.md` — the organization profile page, previously empty.
- `.github/ISSUE_TEMPLATE/bug_report.yml`, `feature_request.yml`, `config.yml` —
  YAML issue forms. No `labels` are set, because a referenced label must exist
  in every consuming repository. Blank issues disabled; contact links point at
  policy files rather than at an issue form.
- `.github/PULL_REQUEST_TEMPLATE.md` — generalized from the infrastructure
  repository's template, adding mandatory security, compliance,
  cross-repository and verification sections.
- `.github/CODEOWNERS` — this repository only; `CODEOWNERS` does not inherit
  organization-wide.
- `.github/FUNDING.yml`, `LICENSE`, `README.md`, `.gitignore`, `CHANGELOG.md`.

### Changed

- `README.md` replaced the four-line stub; its previous content remains in
  Git history at the initial commit.

### Protection

- Ruleset `protect-main` applied to `main`, mirroring the
  `jol-infrastructure` ruleset minus the CI-dependent rules (`required_status_checks`,
  `code_scanning`, `code_quality`), which do not apply to a repository with no
  build. Retains: block deletion, block force-push, linear history, signed
  commits, pull request with code-owner review, resolve-all-threads,
  squash-merge only, require-up-to-date before merge.

### Known limitations recorded at the time of this change

- **Code-owner review is declarative, not substantive.** The organization has a
  single member and both owning teams contain only that member, so no eligible
  second approver exists. A second identity must be invited to the organization
  and added to the `security` and `devops` teams before this control can be
  evidenced in an audit.
- **Direct-push refusal could not be tested** by the administering identity,
  which holds an always-on administrator bypass inherited from the fleet
  ruleset convention. The bypass is not an approved merge path.
- **Not a fleet cleanup.** Roughly twenty-five repositories still carry their
  own `SECURITY.md`; those files win over the new default and remain
  unreconciled, including stale cloud-provider control claims in
  `jol-infrastructure`. Tracked as follow-up in the change record.
- **Out of fleet-sync scope.** A leading-dot directory is not matched by the
  bulk sync tooling; this repository is updated manually.

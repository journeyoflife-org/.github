# Organization community-health defaults

This repository holds the **default** community-health files for every
repository owned by
[`journeyoflife-org`](https://github.com/journeyoflife-org). It contains no
running code and is not deployed.

## How these files are used

GitHub applies a file from this repository to any repository in the organization
that **does not define its own file of the same type**. A repository-local file
always wins; this repository is only the fallback.

Precedence within any repository, including this one:

1. the `.github/` folder
2. the repository root
3. the `docs/` folder

That means editing a file here changes the default for the repositories that
inherit it, and for no others. To find out which is in force for a given
repository, open its *Insights → Community standards* profile, which names the
file actually being used.

## What lives here

| Path | Inherits to the whole organization | Purpose |
|------|-----------------------------------|---------|
| `SECURITY.md` | yes | How to report a vulnerability, response times, breach handling |
| `CODE_OF_CONDUCT.md` | yes | Community standards and enforcement |
| `SUPPORT.md` | yes | Where to ask for help, and what is not offered |
| `CONTRIBUTING.md` | yes | Contribution contract: secrets, signing, review, records |
| `.github/ISSUE_TEMPLATE/` | yes | Default issue forms; a repository's own folder replaces all of them |
| `.github/PULL_REQUEST_TEMPLATE.md` | yes | Default pull-request structure |
| `.github/FUNDING.yml` | yes | Donation link shown on repositories without their own |
| `profile/README.md` | no | Renders as the **organization profile page**, not as a file in any repository |
| `CODEOWNERS` | **no** | Governance of *this* repository only |
| `LICENSE` | **no** | Licenses cannot be defaulted; each repository carries its own |

Workflows, `dependabot.yml` and `CODEOWNERS` are deliberately **not** inherited
organization-wide. If a control must apply to every repository, it is copied per
repository or enforced by an organization ruleset — not placed here and assumed
to take effect.

## Issue template behaviour

Two details that are easy to get wrong and are enforced by the platform, not by
preference:

- Templates here are **YAML forms only**. Mixing Markdown templates and YAML
  forms in one folder causes the Markdown ones to be silently ignored.
- A repository that defines *any* valid template or `config.yml` in its own
  `.github/ISSUE_TEMPLATE` receives **none** of these defaults.
- Templates do not set `labels`, because a referenced label must already exist
  in every repository that uses the template.

## Changing these files

`main` is protected: pull request required, code-owner review required, signed
commits required, linear history, squash-merge only.

Because these files state the organization's security reporting path, a change
here is a governance change, not a documentation edit. Open an issue in
[`jol-infrastructure`](https://github.com/journeyoflife-org/jol-infrastructure)
with a rollback plan first, then reference it in the pull request.

**Maintenance note:** this directory is named with a leading dot, so it is not
matched by the fleet's bulk repository sync tooling and is updated manually with
`git pull` and `git push`.

## Not the organization profile

The file you are reading describes this repository. The text shown on
`github.com/journeyoflife-org` itself is [`profile/README.md`](profile/README.md).

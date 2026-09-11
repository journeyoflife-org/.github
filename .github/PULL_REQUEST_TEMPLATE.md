<!--
Organization-wide pull request template.

Every change to a protected branch is subject to SOC 2 CC8.1 change management.
Sections marked mandatory cannot be left blank; "N/A" is acceptable only with a
reason. A pull request that cannot be rolled back cleanly should not be merged.

Where a repository ships its own template, that one applies instead of this.
-->

## Change summary

<!-- What changed, in two or three sentences. Written for a reviewer returning in six months. -->

## Change type

- [ ] Defect fix
- [ ] Feature or capability
- [ ] Configuration or infrastructure definition
- [ ] Policy or gate
- [ ] Documentation only
- [ ] Refactor with no behaviour change
- [ ] Dependency update

## Motivation

<!-- The problem being solved and why now. Link the governing issue below. -->

## Ticket / change record

- **Issue:** <!-- #NNNN — mandatory for production changes -->
- **ADR or design document:** <!-- link, or "none required" with a reason -->

## Scope of change

<!-- Files, modules or services touched. Anything a reviewer must not overlook. -->

## Risk and blast radius

**Risk level:** Low / Medium / High / Critical

**What is affected if this is wrong:**
<!-- Services, environments, data, people. Name the failure mode, not just the component. -->

## Rollback plan (mandatory)

1.
2.
3.

<!-- State how to detect that rollback is needed, and whether the change is reversible after it has run for a period (migrations, retained data, issued credentials, model retraining, external side effects). -->

## Security impact

<!-- New attack surface, changed trust boundary, credential or key handling, dependency exposure. "None" must be argued, not assumed. -->

## Compliance impact

<!-- GDPR (lawful basis, retention, special category data, data subject rights), PCI-DSS scope, SOC 2 control, ISO 27001 control, audit evidence produced. -->

- Personal data created, moved, retained or exposed: yes / no — detail:
- New outbound network dependency or provider region: yes / no — detail:
- Cross-VLAN or cross-trust-boundary effect: yes / no — detail:

## Cross-repository impact

<!-- Tier 0 contracts, shared models, APIs, event schemas, secret names, ports. Name downstream repositories, or state "isolated" and why that is true. -->

## Verification performed

Paste the commands actually run and their outcome. Assertions without evidence
are not verification.

```text
# command
# result
```

- [ ] No secrets, credentials or personal data committed (secret scan clean)
- [ ] Tests or validation for the affected layer pass
- [ ] Rollback rehearsed or reasoned through
- [ ] Documentation updated to match (ADR, runbook, server note, `CHANGELOG.md`)
- [ ] Breaking changes and affected consumers named above

## Notes for reviewers

<!-- Concentrate attention: the subtle part, the rejected alternative, the assumption most likely to be wrong. -->

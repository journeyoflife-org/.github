# Journey Of Life

Digital infrastructure for the pastoral work of the Catholic Church in Europe —
built and operated in-house by a charitable organization, on hardware it owns.

The mission is practical rather than promotional: parishes, shrines, cemeteries
and funeral ministries need systems that treat people with dignity, keep their
data in their own jurisdiction, and still work on a volunteer's Tuesday evening.

## What this organization builds

| Layer | What lives there | Representative repositories |
|-------|------------------|------------------------------|
| **Contracts** | Shared domain models, identity, hub services | `jol-core`, `jol-hub`, `jol-auth` |
| **Applications** | Parish and ministry platforms, commerce, analytics | `jol-backend-platform`, `jol-ecommerce-engine`, `jol-analytics-ai` |
| **Presentations** | One site per rite and pastoral context, resolved per tenant | `jol-site-parish`, `jol-site-diocese`, `jol-site-cathedral`, `jol-site-basilica`, `jol-site-deanery`, `jol-site-cemetery-care`, `jol-site-funeral`, `jol-site-orthodox`, `jol-site-protestant`, `jol-site-other-church` |
| **AI estate** | Retrieval, inference and audited tool servers, kept inside their own network segments | `jol-rag-server`, `jol-llm`, `jol-mcp-servers`, `jol-hermes-agents` |
| **Integrations** | Registries, taxonomy, and links to parish management systems | `jol-link-registry`, `jol-domain-taxonomy`, `jol-bitrix24-integration` |
| **Platform and governance** | Infrastructure as code, hardening, policy, security, compliance, operations | `jol-infrastructure`, `jol-devops`, `jol-security`, `jol-compliance`, `jol-scripts` |

Commercial marketplace software is developed in the separate
[`jolarca-dev`](https://github.com/jolarca-dev) organization, with its own
governance and audit surface. Ministry and commerce code are deliberately not
commingled.

## Principles held to

- **Data stays where it belongs.** The platform runs on organization-owned
  servers in the EU. There is no public-cloud control plane.
- **Special category data is treated as such.** Religious affiliation is
  personal data of a sensitive class under GDPR Article 9; systems are designed
  for that assumption, not excused by it.
- **Every production change is recorded.** Issue, risk assessment, rollback
  plan, review, evidence — SOC 2 CC8.1.
- **Secrets never enter git.** Vault-backed configuration, pre-commit and CI
  secret scanning, short-lived CI tokens.
- **Least privilege by default.** Default-deny network policy, pod security
  standards, no standing administrative access to production.
- **Claims are verified or labelled.** If a control cannot be demonstrated with
  command output, it is documented as unverified rather than asserted.
- **AI serves the work, not the other way round.** Inference is EU-resident,
  prompts and completions are not retained as a matter of policy, and no
  output is published to a parish without a human standing behind it.

## Contribute

Read [CONTRIBUTING.md](../CONTRIBUTING.md) first: signed commits, review
required, no secrets, and a rollback plan in every pull request.

Report vulnerabilities privately as described in
[SECURITY.md](../SECURITY.md). Never open a public issue for a security
problem.

Questions about scope, partnership or data handling: open an issue in the
relevant repository, see [SUPPORT.md](../SUPPORT.md).

## Licence

Source in this organization is released under the Apache License 2.0 unless a
repository states otherwise. Publishing code under a licence does not create
permission to process the data it handles.

---

*This organization and its partners are not a legal, financial, medical or
pastoral authority in their own right. Canonical, diocesan and civil
requirements take precedence over anything in this software.*

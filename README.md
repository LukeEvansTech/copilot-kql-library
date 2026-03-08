# copilot-kql-library

A curated library of KQL queries for auditing, hunting, and reporting on Microsoft 365 Copilot activity across Microsoft Purview, Microsoft Defender XDR, and Microsoft Sentinel.

Each query lives next to a Markdown explainer that describes the scenario it answers, the data sources it uses, and any prerequisites or licence requirements.

## Categories

| Folder               | What's in it                                                                                                                      |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `queries/audit/`     | Compliance-focused queries against the Microsoft Purview unified audit log (Copilot prompt/response auditing, retention, access). |
| `queries/hunting/`   | Threat-hunting queries against Defender XDR / Sentinel `CloudAppEvents` and related tables (anomalous use, abuse, risky users).   |
| `queries/grounding/` | Queries that surface which files, sites, and data Copilot is grounding on — useful for oversharing and label-coverage analysis.   |

## Running queries

- **Microsoft Purview audit**: <https://compliance.microsoft.com/auditlogsearch> — paste KQL into the _Search_ field, ensure the time range covers your Copilot activity.
- **Microsoft Defender XDR Advanced Hunting**: <https://security.microsoft.com/v2/advanced-hunting>.
- **Microsoft Sentinel**: any Log Analytics workspace with the Microsoft 365 connector enabled.

Some queries assume the Microsoft Purview Audit (Premium) licence for full retention; lighter alternatives are noted where applicable.

## Contributing

PRs welcome. Each query should ship with:

- A working `.kql` file, syntactically valid in the target environment.
- A companion `.md` explaining: what it answers, prerequisites, columns returned, suggested time range, and known caveats.
- A short test sentence in `tests/queries.md` confirming you ran it against a real tenant (or a labelled exception).

See [CONTRIBUTING](.github/CONTRIBUTING.md).

## Licence

[MIT](LICENSE).

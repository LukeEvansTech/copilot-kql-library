# copilot-kql-library

A curated library of KQL queries for auditing, hunting, and reporting on Microsoft 365 Copilot.

## What's here

- **Audit queries** - compliance-focused queries against the Microsoft Purview unified audit log.
- **Hunting queries** - Defender XDR / Sentinel queries for anomalous or risky Copilot use.
- **Grounding queries** - surface which files, sites, and data Copilot is grounding on.

Browse the navigation on the left. Source files (`.kql`) live in [`queries/`](https://github.com/LukeEvansTech/copilot-kql-library/tree/main/queries) on GitHub, ready to paste into the relevant portal.

## Where to run them

| Category            | Portal                                                                                        |
| ------------------- | --------------------------------------------------------------------------------------------- |
| Audit               | [Microsoft Purview audit log search](https://compliance.microsoft.com/auditlogsearch)         |
| Hunting             | [Microsoft Defender XDR Advanced Hunting](https://security.microsoft.com/v2/advanced-hunting) |
| Hunting / Grounding | Microsoft Sentinel (any workspace with the Microsoft 365 connector)                           |

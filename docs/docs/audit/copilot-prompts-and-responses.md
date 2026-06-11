# Copilot prompts and responses (audit)

## Scenario

You need a complete record of who used Microsoft 365 Copilot, what they asked, what Copilot said in reply, and which resources Copilot looked at while answering. Common drivers:

- Compliance review of Copilot adoption.
- Incident response - did the user prompt Copilot for sensitive content?
- eDiscovery - Copilot interactions are subject to legal hold like any other M365 communication.

## Data source

Microsoft Purview unified audit log, record type `CopilotInteraction`. Each event captures:

| Property            | Description                                                                                                      |
| ------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `AppHost`           | The Copilot host app: `Word`, `Excel`, `PowerPoint`, `Outlook`, `Teams`, `Copilot`, `Loop`, `OneNote`, `Stream`. |
| `AppContext`        | Where in the app the interaction happened (e.g. `WordApp`, `Chat`, `Compose`).                                   |
| `Prompt`            | The user prompt sent to Copilot.                                                                                 |
| `Response`          | The model response surfaced to the user.                                                                         |
| `AccessedResources` | Array of grounding resources Copilot read (files, sites, mails).                                                 |

## Prerequisites

- Microsoft Purview Audit (Standard) - 180-day retention, default for E3/E5.
- Microsoft 365 Copilot licences assigned to the users in question.
- The tenant admin must have enabled audit logging (on by default since 2023).

## Columns returned

`TimeGenerated`, `UserPrincipalName`, `AppHost`, `AppContext`, `Prompt`, `Response`, `AccessedResourceCount`, `CorrelationId`.

## Caveats

- Prompt and Response storage is subject to the tenant's Copilot data retention configuration. If the retention policy excludes Copilot interactions, Prompt/Response columns may be null.
- `AccessedResources` can grow large; the query projects only the count. Drill in by removing the `array_length` cast.

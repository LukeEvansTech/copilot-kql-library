# Copilot accessed files (grounding)

## Scenario

Microsoft 365 Copilot answers using grounding data — the files, emails, and Teams messages it can see for the prompting user. Anything Copilot grounded on is, in effect, surfaced to that user. This query lists the resources Copilot accessed across all users in the window, ranked by access count.

Use it to:

- Find unexpectedly popular grounding sources.
- Spot files with weak labelling that Copilot is happily reading.
- Identify oversharing — if a "Confidential" file shows up here for a user who shouldn't have it, the access path is open via Copilot.

## Data source

Microsoft Purview unified audit log (`CopilotInteraction`), specifically `AccessedResources`. The query expands the array, filters to file/mail/Teams resource types, and aggregates by resource.

## Output columns

`ResourceType`, `ResourceName`, `ResourceUrl`, `SensitivityLabelId`, `AccessCount`, `DistinctUsers`, `LastSeen`.

## Caveats

- `SensitivityLabelId` is the GUID; cross-reference with `Get-Label` (Microsoft Purview compliance PowerShell) or your tenant label catalogue to translate.
- Resources without sensitivity labels show up as empty `SensitivityLabelId` — those are usually the highest-risk because labelling didn't catch them.
- Email and Teams resources don't have a meaningful URL; expect those to look bare.

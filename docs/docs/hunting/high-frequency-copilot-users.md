# High-frequency Copilot users (hunting)

## Scenario

A user is suddenly hammering Microsoft 365 Copilot far above their normal pattern. Possible explanations:

- Legitimate workload spike (release week, board prep, audit).
- Automated tooling driving Copilot via a hijacked session token.
- Compromised account being used to mass-query corporate data via Copilot grounding.
- Internal user attempting bulk data extraction at the speed Copilot allows.

This query flags users whose interaction count today exceeds a tunable spike factor over their own 29-day baseline.

## Data source

Microsoft Defender XDR Advanced Hunting - `CloudAppEvents` with `Application == "Microsoft 365 Copilot"`. The same query works in Microsoft Sentinel against `CloudAppEvents` from the M365 Defender connector.

## Tuning parameters

- `lookback` - baseline window (default 30 days).
- `TodayInteractions > 50` - minimum absolute volume so quiet users don't trigger.
- `SpikeFactor > 5` - multiple over baseline. Raise for noisy estates.

## Caveats

- Users new to Copilot have a zero baseline; the query falls back to comparing absolute volume only. Tune the absolute threshold for your tenant.
- `Application` string occasionally varies across Defender XDR releases. Cross-check with `summarize count() by Application` if results look empty.

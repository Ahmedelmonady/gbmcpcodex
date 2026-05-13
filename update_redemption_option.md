# update_redemption_option

Updates an existing redemption option by ID. **ALWAYS** call `get_redemption_option` first to get the current state with existing entity IDs preserved — updates require the full object with IDs to avoid duplicates.

{{> update_flow}}

## Parameters

Uses a subset of the same fields as `create_redemption_option` — see `codex://tools/create_redemption_option` for the full list.

- `id` — redemption rule ID to update.
- `ruleType`, `pointsToRedeem` — required for the update payload.
- Other fields optional — only include what changes.

## Why entity IDs matter

The backend uses IDs to identify which existing audience rules / collections / merchants to update vs. create. Stripping IDs and submitting fresh objects creates duplicate child entities — the original ones are not deleted.

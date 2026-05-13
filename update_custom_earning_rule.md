# update_custom_earning_rule

Updates an existing custom earning rule. **ALWAYS** call `get_custom_earning_rules` first to get the full object with entity IDs — updates require the complete object preserved.

{{> update_flow}}

## Parameters

- `rule` — full `ClientPointsSettingViewModel` with entity IDs preserved. Get from `get_custom_earning_rules`, modify, pass back.

## User prompting

Show current rule state, ask what to change, confirm before applying.

## Why entity IDs matter

The backend uses IDs to identify which existing conditions/collections to update vs. create. Stripping IDs and submitting fresh objects creates duplicate child entities — the original ones are not deleted.

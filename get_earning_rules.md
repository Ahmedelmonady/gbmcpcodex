# get_earning_rules

Returns the earning rules — cashback reward type (General/Exclude/Include) and dynamic conditions that control which orders earn points.

## Notes

- Different from `get_custom_earning_rules` (which returns named per-condition rules with their own reward configs).
- Use this tool when the user asks "which orders earn points" or wants to see the current cashback inclusion/exclusion logic.
- Required to read first before any `update_earning_rules` call.

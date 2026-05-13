# get_custom_earning_rules

Lists all custom earning rules for the client — returns each rule's name, config mode, conditions, and reward values.

## Notes

- Different from `get_earning_rules` (which returns the global cashback inclusion/exclusion settings).
- Required to read first before any `update_custom_earning_rule` or `delete_custom_earning_rule` call (you need the full rule object with entity IDs to update without creating duplicates).

# delete_custom_earning_rule

Deletes a custom earning rule by its rule name. Removes the rule and all tier-specific children with the same name.

## Parameter

`ruleName` — the exact rule name to delete (from `get_custom_earning_rules`).

## Irreversible

ALWAYS confirm before deleting:

- Show the rule name + key details (conditions, reward) so the user knows what they're deleting.
- Ask twice: "Are you sure you want to delete the custom earning rule **`<name>`**? This action is irreversible." once at the summary, once just before the call.

# delete_redemption_option

Permanently deletes a redemption option by ID.

## Parameter

`id` — the redemption rule ID to delete.

## Restrictions

- **The General (default) rule cannot be deleted.** Backend rejects with an error.

## Irreversible

Confirm twice with the user before calling:

- Show the rule name + key details (resolved via `get_redemption_option`).
- State explicitly that the rule and any pending coupon issuance will be removed.
- Ask twice — once at the summary, once just before the call. Use "Are you sure?" phrasing.

## Alternative

If the user just wants to hide the option without deleting, use `toggle_redemption_option_activation` instead.

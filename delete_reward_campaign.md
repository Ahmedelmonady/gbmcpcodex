# delete_reward_campaign

Permanently deletes a reward campaign by ID. Removes the campaign and all associated rewards, events, and audience rules.

## Parameter

`id` — the campaign ID to delete.

## Irreversible

This action cannot be undone. Confirm with the user before deleting:

- Show the campaign name and key details (resolved via `get_reward_campaign`).
- State explicitly that all associated rewards, events, and audience rules will be removed.
- Ask twice — once at the summary, once just before the call. Use "Are you sure?" phrasing.

## Alternative

If the user just wants to stop the campaign from running but keep the data, use `toggle_reward_campaign_activation` instead.

# toggle_reward_campaign_activation

Activates or deactivates a reward campaign by ID. Handles cache invalidation, job scheduling, and audit logging.

## Parameter

`id` — the campaign ID to toggle.

## Read-before-write

Call `get_reward_campaigns` (or `get_reward_campaign`) first to confirm the current state — toggling without knowing the current state can flip a campaign in the wrong direction.

## Notes

- This is a single endpoint — there is no separate activate/deactivate. The current `isActive` flag is flipped.
- Activating a newsletter campaign is the standard step after `create_newsletter` (which forces inactive at creation time).

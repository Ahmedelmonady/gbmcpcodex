# get_reward_campaign

Returns full details for a single reward campaign by ID — includes behavior configuration, reward configurations, challenge events, audience rules, scheduling, goal, and locales.

## Parameter

`id` — the campaign ID. Get IDs from `get_reward_campaigns`.

## Notes

- For browsing or filtering many campaigns, use `get_reward_campaigns` (slim) or `get_reward_campaigns_stats` (slim with achievement counts) instead.
- Required as the first step before any update — `update_reward_campaign` needs the full object with entity IDs preserved.

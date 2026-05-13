# get_reward_campaigns_count

Returns the total count of reward campaigns matching the filter — same filter syntax as `get_reward_campaigns`.

## When to use

Use when the user wants a count or quick stat (e.g. "how many active spin-the-wheel campaigns", "count of campaigns created this month") without needing the full list. Cheaper than paging through `get_reward_campaigns`.

## Filter syntax

Identical to `get_reward_campaigns` — see `codex://tools/get_reward_campaigns` for the full filter table and behavior-type IDs.

Omit the filter to get the total reward-campaign count for the client.

## User prompting

Ask what they want to count if not specified. Present the result as a short sentence (e.g. "You have 12 active campaigns.") rather than raw JSON.

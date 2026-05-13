# get_reward_campaigns_stats

Lists reward campaigns with their **per-campaign achievement counts pre-aggregated** in a single call. Each row returns `id`, `numberAchievements` (total achievements), and `numberPlayersAchieved` (unique players who achieved). Same filter syntax as `get_reward_campaigns`.

## When to use

Use when the user asks performance / ranking questions across many campaigns — e.g.:
- "which campaign has the most achievements"
- "top 5 campaigns by unique players"
- "how engaging is each campaign"

The backend joins the Achievement table once for ALL campaigns in the page, so this is **one round-trip** even for the full list.

## Avoid the N+1 trap

Do **NOT** loop `get_reward_campaign_customers_count` per campaign — that fires N+1 queries and overloads the server. Use this tool instead.

## To answer "campaign with most achievements"

Call once with `pageSize: 1`, `orderBy: <if backend supports an achievements sort>`, or just fetch a page and sort in your response.

## Filter syntax

Identical to `get_reward_campaigns` — see `codex://tools/get_reward_campaigns` for the full filter table. Combine with `status eq true` to limit to active campaigns.

## User prompting

Ask the user what they want to rank by (achievements, unique players, points awarded). Present results in a friendly readable list, not raw JSON.

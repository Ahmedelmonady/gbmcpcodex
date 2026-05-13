# get_reward_campaign_customers_count

Returns the total count of achievement records on a specific reward campaign matching the filter. Single number, much cheaper than paging through the full list.

## Default behavior

Returns count of **EVERY achievement record** (winners + NoLuck for games).

## To count ONLY winners

For game campaigns: add `success eq true` to the filter to exclude NoLuck rows.
For non-game campaigns: this filter is a no-op.

## Filter syntax

Identical to `get_reward_campaign_customers` — see `codex://tools/get_reward_campaign_customers` for the full filter table.

## User prompting

Ask which campaign and what to count if not specified. For "how many won" / "how many people got a prize" on game campaigns, include `success eq true` in the filter. Present the result as a short sentence (e.g. "1,234 customers participated in your Welcome Spin." or "342 customers won your Welcome Spin.") rather than raw JSON.

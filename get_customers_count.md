# get_customers_count

Returns aggregate customer counts (total, active, inactive) matching the filter — same filter syntax as `get_customers`.

## When to use

Use when the user wants a count or quick stat (e.g. "how many active customers in tier 2", "count of customers with points over 500") without needing the full list. Much cheaper than paging through `get_customers`.

## Filter syntax

Identical to `get_customers` — see `codex://tools/get_customers` for the full filter table. Omit the filter to get the total customer count for the client.

## User prompting

Ask what they want to count if not specified. Present the result as a short sentence (e.g. "You have 1,234 active customers.") rather than raw JSON.

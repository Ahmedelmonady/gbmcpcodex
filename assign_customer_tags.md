# assign_customer_tags

Assigns one or more tags to one or more customers by their **Gameball numeric IDs** (NOT external IDs).

## Flow

1. Call `get_customers` first to find customers (response includes `id` — the Gameball numeric ID).
2. Call `get_tags` to discover available tag IDs.
3. Pass both arrays to this tool.

## User prompting

Before calling, confirm with the user:

1. Which customers? (show names + IDs from `get_customers`)
2. Which tags? (show names from `get_tags`)
3. Confirm: "I'll assign **[tag names]** to **[N]** customers. Proceed?"

## Notes

- Idempotent — re-applying an existing tag is a no-op.
- Use the **Gameball numeric `id`** from `get_customers`, NOT the `externalId`.

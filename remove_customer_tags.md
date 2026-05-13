# remove_customer_tags

Removes one or more tags from one or more customers by their **Gameball numeric IDs**.

## Flow

1. Call `get_customers` first to find customers (response includes `id` — the Gameball numeric ID).
2. Call `get_tags` to discover tag IDs. Or use `get_customer_details` to see which tags a customer currently has.
3. Pass both arrays to this tool.

## User prompting — destructive, confirm

Always confirm before removing:

1. Which customers? (show names + IDs)
2. Which tags to remove? (show names)
3. Confirm: "I'll remove **[tag names]** from **[N]** customers. Are you sure?"

## Notes

- Use the **Gameball numeric `id`** from `get_customers`, NOT the `externalId`.

# get_collections

Returns the client's available product collections with their `collectionId` and `collectionName`.

## When to call

ALWAYS before:

- `create_redemption_option` — if scoping to specific collections (`collections[]`)
- `update_redemption_option` — same
- `create_custom_earning_rule` — if condition uses `OrderLineItems.Collection` `fieldPath`
- `update_earning_rules` — same
- `create_*_campaign` — if filtering campaign rewards by collection

Use the `collectionId` (NOT the name) when passing collections.

## Notes

- Collection set varies by client type (Shopify vs default) — backend resolves automatically.
- Read-only — to manage collections, use the source platform (Shopify, Salla, etc.).

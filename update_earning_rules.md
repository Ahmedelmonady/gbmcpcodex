# update_earning_rules

Updates earning rules — which orders earn points. Send ONLY the fields you want to change. **ALWAYS** call `get_earning_rules` first to show the user the current state.

{{> update_flow}}

## User prompting — interactive process

1. Call `get_earning_rules` and present the current configuration in friendly language.
2. ASK: "Which orders should earn points?"
   - "All orders (General)" — `cashbackRewardType=1`
   - "All orders EXCEPT specific items (Exclude)" — `cashbackRewardType=2`
   - "ONLY specific items (Include)" — `cashbackRewardType=3`
3. If Exclude/Include: ASK "Which field to filter on?" — call `get_merchants` or `get_collections` to discover values.
4. Show a summary of changes before submitting.
5. Confirm before applying.

## Fields

- `cashbackRewardType` (int) — `1`=General (all orders earn), `2`=Exclude (all except matching), `3`=Include (only matching), `4`=Merchant, `5`=Custom
- `items` (array) — conditions for Exclude/Include/Custom. **REPLACES the entire array** (not a merge). Each item:
  - `fieldPath` (string) — the order field. Common values:
    - `OrderLineItems.Collection`
    - `Merchant.ExternalId`
    - `Order.Channel`
    - `OrderLineItems.Category`
    - `OrderLineItems.Vendor`
    - `OrderLineItems.Sku`
    - `OrderLineItems.Tags`
    - `Order.Extra.<fieldName>`
  - `matchValue` (string) — value to match, comma-separated for multiple (e.g., `"POS,WEB"` or `"collection_123,collection_456"`)
  - `operator` (int) — `1`=Equals, `2`=NotEquals, `3`=GreaterThan, `4`=GreaterThanOrEqual, `5`=LessThan, `6`=LessThanOrEqual, `7`=Contains, `8`=NotContains, `9`=Exists
  - `logicalOperator` (int) — `1`=AND, `2`=OR (how this condition combines with the next)
- `collections` (array) — product collections for Include/Exclude: `[{ collectionId, collectionName }]`

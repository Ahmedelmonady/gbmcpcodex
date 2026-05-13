# get_merchants

Returns the client's merchants with their external IDs, names, and branches.

## Response shape (per merchant)

- `externalId` — the value to use in conditions (`Merchant.ExternalId`)
- `name` — display name
- `branches[]` — array of `{ externalId, name }`

## When to call

ALWAYS before:

- `create_custom_earning_rule` — if condition uses `Merchant.ExternalId` or `Merchant.Branch.ExternalId` `fieldPath`
- `update_earning_rules` — same
- `create_redemption_option` / `update_redemption_option` — if scoping to specific merchants (`merchants[]`)

The condition's `matchValue` uses the merchant's `ExternalId` (e.g., `Merchant.ExternalId` = `deraah`), NOT the display name.

## User prompting

Resolve user-supplied merchant names via case-insensitive match against `name`. Confirm the match back: "Found `<name>` (ID `<externalId>`) — use this one?" before passing the ID.

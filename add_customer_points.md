# add_customer_points

Adds points or a currency amount to a customer's wallet balance.

## Parameters

- `customerId` — customer's external ID
- Either `points` (positive integer) OR `amount` (positive currency value) — not both. When using `amount`, the backend converts it to points using the client's redemption factor.
- `reason` — required, max 60 characters
- `expiryAfterDays` — optional. If omitted, the account's default points expiry setting is used. Set to a specific number of days to override.

## User prompting

Before calling, ask the user for:

1. The customer's external ID
2. How many points (or what currency amount) to add
3. The reason for adding points

Then confirm: "I'll add [X points / $X] to customer [ID] for reason: [reason]. Proceed?"

## Notes

- Idempotent — duplicate calls add duplicate points (no de-duplication on `reason`).
- Pair with `deduct_customer_points` for the inverse operation.

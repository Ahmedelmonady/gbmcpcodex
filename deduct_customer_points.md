# deduct_customer_points

Deducts points or a currency amount from a customer's wallet balance.

## Parameters

- `customerId` — customer's external ID
- Either `points` (positive integer — backend handles the sign) OR `amount` (positive currency value) — not both
- `reason` — required, max 60 characters

## Behavior

- Balance will not go below zero — if the deduction exceeds available balance, it's capped at the current balance.
- **No expiry setting** — expiry does not apply to deductions.

## User prompting — destructive, confirm twice

Ask for:

1. The customer's external ID
2. How many points (or what currency amount) to deduct
3. The reason for the deduction

Show a plain-language summary, then confirm twice:
- At the summary: "I'll deduct [X points / $X] from customer [ID] for reason: [reason]."
- Just before the call: "Are you sure?"

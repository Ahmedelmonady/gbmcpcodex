# get_tiers

Returns the client's VIP tiers with their IDs, names, order, and score thresholds.

## When to call

ALWAYS before:

- `get_customers` with a tier filter — the syntax uses tier IDs (e.g. `level in 1,2,3`), not names.
- Any user question about tier structure ("show me tiers", "what tiers do I have").

## Notes

- For full per-tier details (rewards, locales, icon, pointing config), use `get_tier_details` with the ID.
- Read-only — tier creation/edit is dashboard-only.

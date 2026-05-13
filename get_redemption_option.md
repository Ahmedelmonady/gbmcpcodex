# get_redemption_option

Returns detailed information for a single redemption rule by ID — audience targeting, collections, merchants, advanced coupon options, and localized reward names.

## Parameter

`id` — the redemption rule ID. Get from `get_redemption_options`.

## Notes

- Required before `update_redemption_option` (you need the full object with entity IDs preserved).
- For just-the-list use `get_redemption_options` (slim payload).

# toggle_redemption_option_activation

Activates or deactivates a specific redemption option by ID. Toggles the `IsVisible` flag.

## Parameter

`id` — the redemption option ID to toggle.

## Read-before-write

Call `get_redemption_options` (or `get_redemption_option`) first to confirm current state — toggling without knowing direction can hide a live option from customers.

## Notes

- Single endpoint — no separate activate/deactivate. Current `isVisible` flag is flipped.
- Does not affect existing coupons already issued to customers.

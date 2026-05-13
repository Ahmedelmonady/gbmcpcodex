# get_redemption_options

Lists all redemption options (slim payload: `id`, `ruleName`, `type`, `equivalentPoints`, `equivalentPointsValue`, `isVisible`, `hasCollections`).

## Notes

- For full details on one option (audience, collections, advanced coupon options, locales) use `get_redemption_option` with the ID.
- Required first step before `update_redemption_option`, `toggle_redemption_option_activation`, or `delete_redemption_option`.

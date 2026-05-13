# get_earning_config

Returns the general earn-points configuration — how many points customers earn per dollar spent, currency, expiry, pending period, and fee/tax exclusions.

## Notes

- **Singleton** — there is one earning config per client (not a list).
- The base earning rule. For per-condition cashback, see `get_earning_rules` and `get_custom_earning_rules`.
- Required to read first before any `update_earning_config` call so the user can see current state.

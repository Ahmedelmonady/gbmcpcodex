# update_earning_config

Updates the general earn-points configuration. Send ONLY the fields you want to change — backend loads current and merges. **ALWAYS** call `get_earning_config` first to show the user the current state.

{{> update_flow}}

## User prompting — interactive process

1. Call `get_earning_config` and present the current settings in friendly language.
2. Ask: "What would you like to change?" — do NOT assume what to change.
3. Walk through ONLY the settings the user wants to modify.
4. Show a summary of changes before submitting (current value → new value).
5. Confirm: "Ready to apply these changes?"

## WARNING: Currency changes

Changing currency propagates to ALL rules and the widget — **always confirm twice** with the user before modifying currency fields.

## Available fields

- `amountRewardThreshold` (number) — minimum order amount to earn points (e.g., `1.0` = earn on orders >= $1)
- `rewardWalletFactor` (number) — wallet points earned per $1 spent (e.g., `1.0` = 1 point per $1)
- `rewardRankFactor` (number) — score points earned per $1 spent
- `redemptionFactor` (number) — points needed per $1 of redemption value
- `currency` (string) — ISO currency code (e.g., `"USD"`, `"SAR"`)
- `currencySymbol` (string) — display symbol (e.g., `"$"`, `"SAR"`)
- `isUsingCurrencySymbol` (bool) — `true` = show symbol, `false` = show code
- `pointsExpiry` (int) — days until points expire (`0` = never expire)
- `pointsPendingDays` (int) — return window in days before points become available (pending period)
- `isPointsRewardOn` (bool) — master toggle for earning points
- `isPointsRedemptionOn` (bool) — master toggle for redeeming points
- `excludeNonProductCosts` (bool) — `true` = exclude shipping and non-product costs from earning calculation
- `excludeTaxes` (bool) — `true` = exclude taxes from earning calculation
- `holdPointsInMinutes` (int) — hold duration in minutes (1-21600)

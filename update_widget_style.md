# update_widget_style

Updates Branding + Launcher settings via `PUT /ClientBotSettings/style`.

## CRITICAL: send ALL style fields

ALWAYS call `get_widget_settings` first and pass ALL style fields back (modified + unchanged) — AutoMapper on the backend overwrites ALL mapped fields, including with nulls. Omitting a field wipes its value.

{{> update_flow}}

## Branding > Colors

- `isBotDarkTheme` (bool) — light/dark theme
- `botMainColor` (hex) — main widget body color
- `buttonBackgroundColor` (hex) — launcher button background
- `buttonFlagColor` (hex) — launcher button icon color
- `buttonForegroundColor` (hex) — launcher button text color
- `buttonSariColor` (hex) — secondary button color (copy of `buttonFlagColor`)

## Branding > Identity

- `widgetFont` (string) — `"Montserrat"`, `"Cairo"`, `"Tajawal"`, `"Noto"`
- `widgetRankPointsIcon` (URL) — rank/score points icon
- `widgetWalletPointsIcon` (URL) — wallet points icon

## Launcher > Customize

- `widgetIcon` (string) — launcher icon: `"1"`=default, `"2"`=badge, `"3"`=gift, `"4"`=love, `"5"`=trophy, or URL for custom upload
- `buttonDirection` (string) — `"left"` or `"right"`
- `isReverseDirectionEnable` (string) — `"true"` or `"false"`
- `enableLauncherEffect` (bool) — launcher animation

## Launcher > Shape

- `buttonShape` (string) — `"circle"`, `"rounded"`, `"tab"`, `"tabText"`, `"quarterCircle"`, `"toggle"`

## Image-value tristate (applies to widgetTrophyIcon, widgetReferralIcon, earnIconUrl, redeemIconUrl)

- `null` = use default built-in icon
- `"none"` = hide the icon completely (no image)
- URL string = custom uploaded image — use the icon library via `get_icons` or upload via `utilsApi.uploadImage`

## Per-language (optional)

`clientBotSettingLocals[]` — array of `{ languageId, programName, rankPointsName, walletPointsName, buttonShapeText }`.

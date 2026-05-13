# get_supported_languages

Returns the client's supported languages with their IDs, codes, names, and direction.

## Response shape (per language)

- `id` — use as `languageId` in any `locales[]` array
- `localeLanguageId` — the system-wide locale ID (1=English, 2=French, ... see `update_supported_languages` for the full table)
- `code` — `"en"`, `"ar"`, etc.
- `name` — `"English"`, `"Arabic"`, etc.
- `direction` — `"ltr"` or `"rtl"`
- `isDefault` (bool)

## When to call

ALWAYS before any tool that takes a `languageId` in nested locales — `create_*_campaign`, `create_redemption_option`, `update_redemption_option`, `update_widget_settings`. Use `id` (NOT `localeLanguageId`) as the `languageId` value.

## Note

To add/remove languages or change default, use `update_supported_languages` (separate write operation).

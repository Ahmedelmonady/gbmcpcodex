# update_supported_languages

Updates the client's supported languages — add, remove, or change the default language. ALWAYS call `get_supported_languages` first to get the current list, then modify and pass the FULL list back.

{{> update_flow}}

## How to mutate the list

- **Add a language**: append a new entry with `{ localeLanguageId, code, name, isDefault: false, isDeleted: false }`.
- **Remove a language**: set `isDeleted: true` on the existing entry. Must keep at least one non-deleted.
- **Change default**: set `isDefault: true` on the new default AND `isDefault: false` on the old one. Exactly one must be default.

## Available locale language IDs

- `1` = English
- `2` = French
- `3` = Spanish
- `4` = Italian
- `5` = German
- `6` = Portuguese
- `7` = Turkish
- `8` = Arabic
- `9` = Dutch
- `10` = Japanese
- `11` = Indonesian
- `12` = Korean

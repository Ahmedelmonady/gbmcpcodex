# get_widget_settings

Returns the current widget settings — all fields across Branding, General, Launcher, and Guest sections.

## Update split (important)

The dashboard splits widget settings into TWO endpoints with different semantics:

- **`update_widget_style`** → PUT /ClientBotSettings/style
  - Branding > Colors + Identity + Launcher fields
  - **MUST send ALL style fields** (modified + unchanged) — AutoMapper overwrites all mapped fields including nulls
- **`update_widget_settings`** → PUT /ClientBotSettings
  - General > Visibility + Guest + Referral + Icons fields
  - Partial updates OK — only sent fields change

## Notes

- Required first step before any update — to know current state and (for `update_widget_style`) to send back ALL style fields.
- Use `get_widget_settings` once and route fields between `update_widget_style` and `update_widget_settings` based on the section they belong to.

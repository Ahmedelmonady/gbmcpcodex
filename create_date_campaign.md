# create_date_campaign

Creates a date-triggered campaign (`DateBased`). Fires yearly on the customer's date attribute.

{{> template_flow}}

{{> core_required}}

## Badge (icon)

The template returned by `get_campaign_template('DateBased')` already includes an icon in `challengeBehaviour.icon` (e.g., `"birthday"` for Birthday templates). **Preserve it as-is** unless the user wants to change it.

If the user wants to swap: call `get_icons` to fetch the library and replace `challengeBehaviour.icon` with the new `IconView`. See `codex://tools/get_icons` for the shape.

## Date-specific (ask if not provided)

- "Which customer date? Birthday, join date, first order, or a custom date attribute?"
- **Built-in** (`isCustomAttribute:false`): `DateOfBirth`, `JoinDate`, `CreationDate`, `Counters_FirstOrderDate`
- **Custom** (`isCustomAttribute:true`): call `get_customer_attributes`, filter `attributeType===3`, use ID as `attributeKey`
- Set `configurations: { type:18, isCustomAttribute, attributeKey, attributeLabel }`
- Note: DateBased campaigns are single occurrence (once per year). No repeatability setting needed.

# get_customer_attributes

Returns the client's custom customer attributes with their IDs, keys, names, and data types.

## Attribute types

- `1` = Number
- `2` = String
- `3` = Date
- `4` = Boolean

## When to call

- **Audience targeting** — for `create_*_campaign` / `create_redemption_option` audience rules that key on customer attributes.
- **Date-based campaigns** — `create_date_campaign` filtering for date attributes (`attributeType === 3`):
  - Use the attribute's ID (as string) as `configurations.attributeKey`
  - Use the attribute name as `configurations.attributeLabel`
  - Set `isCustomAttribute: true`

## Built-in date attributes (no need to call get_customer_attributes for these)

For `create_date_campaign` with `isCustomAttribute: false`, use one of:

- `CreationDate`
- `Counters_FirstOrderDate`
- `DateOfBirth`
- `JoinDate`

# get_tags

Returns the client's tags with their IDs, names, and types.

## Tag types

- `1` = **Internal** (system-managed, not editable)
- `2` = **Segment**
- `3` = **RFM**
- `4` = **Custom** (user-created global tags)

## When to call

ALWAYS before any tool that takes a tag ID — use `id` (NOT name) as the value:

- `create_redemption_option` / `update_redemption_option` — audience targeting (`audience[].value` for `key: "Tag"`)
- `create_*_campaign` — audience targeting (same shape)
- `assign_customer_tags` / `remove_customer_tags` — `tagIds[]`
- `get_customers` — filter by tag IDs (`tags in 5,10,15`)

## User prompting

If the user names a tag, resolve via case-insensitive match. **Always confirm**: "Found `<resolved>` (ID `<id>`) — use this one?" before passing the ID anywhere.

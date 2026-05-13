# update_reward_campaign

Updates an existing reward campaign by ID. **ALWAYS** call `get_reward_campaign` first — updates require the full object with entity IDs to avoid duplicates.

{{> update_flow}}

## Ask about

Name, rewards, audience, scheduling, budget, reward cap, repeatability, visual customizations (colors, images, configurations) — whatever the user wants to change.

## Parameters

- `id` — campaign ID to update.
- `campaign` — full updated campaign object with entity IDs preserved.

## Why entity IDs matter

The backend uses IDs to identify which existing rewards/events/audience rules to update vs. create. Stripping IDs and submitting fresh objects creates duplicate child entities — the original ones are not deleted.

## Badge (icon) — mirror AddBadgeComponent exactly

The campaign object returned by `get_reward_campaign` includes the existing `challengeBehaviour.icon` and `.visibility`. **Preserve both as-is** unless the user explicitly wants to change them. Stripping or nulling `icon` removes the badge entirely.

The dashboard's badge picker (`add-badge.component.ts:145-149`) does this when the user clicks "Add Badge" / "Edit Badge" and confirms:

```typescript
apply() {
  challenge.challengeBehaviour.visibility = this.visibility   // user's chosen visibility
  if (this.icon.name) challenge.challengeBehaviour.icon = this.icon
}
```

Modal initialization quirk (`add-badge.component.ts:75-79`): if the campaign currently has `visibility = 2` (Not Visible — i.e., a hidden placeholder badge), the modal's visibility toggle defaults to **`1` (Always Visible)** — assuming if the user opened the picker they want the badge shown.

### MCP equivalent flows

**User wants to opt in to showing an existing hidden badge** (current `visibility = 2`):
- Just flip `challengeBehaviour.visibility = 1`. Don't touch `icon`.

**User wants to change the badge image** (regardless of current visibility):
1. Call `get_icons` to fetch the library.
2. Ask the user to pick a name (echo back: "Found 'badge-1' — use this one?").
3. Replace `challengeBehaviour.icon` with the **minimal 3-field shape** (see `codex://tools/get_icons`):
   ```json
   "icon": { "name": "<picked.name>", "fileName": "<picked.iconPath>", "iconTypeId": 1 }
   ```
4. If the badge was hidden (`visibility = 2`) and the user is picking a new one, also set `visibility = 1` — same as the dashboard modal's default. Otherwise preserve current visibility.

**User wants to hide the badge** (without removing the data):
- Set `challengeBehaviour.visibility = 2`. Leave `icon` intact.

**Visibility values**: `1` = Always Visible, `2` = Not Visible, `3` = Visible If Earned.

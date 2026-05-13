# get_icons

Returns the client's icon library from S3 — the same library the dashboard uses as the source for its badge / icon pickers.

## Response shape

```json
[
  { "name": "Driving",   "iconPath": "https://s3.us-east-2.amazonaws.com/.../gb-library/general/Driving.svg" },
  { "name": "Puzzle",    "iconPath": "https://s3.us-east-2.amazonaws.com/.../gb-library/general/Puzzle.svg" },
  ...
]
```

`name` is short (e.g. `"badge-1"`, `"coins"`, `"giftbox"`, `"spin-the-wheel"`). `iconPath` is the full S3 URL — environment-specific (don't hardcode the host).

## When to call

Call before any tool that sets a badge / icon and the user hasn't already specified one:

- **`create_event_campaign`** (EventBased) — REQUIRED. EventBased is built from scratch and has no template-supplied icon. Without setting `challengeBehaviour.icon`, the campaign saves with `icon: null` and the dashboard shows the row with a broken / empty badge.
- **`create_*_campaign`** for templated types (game, date, mission, calendar, newsletter, spending milestone) — only call if the user wants to **change** the badge. The template returned by `get_campaign_template` already includes a per-type default icon — preserve it.
- **`update_reward_campaign`** — only call if the user wants to swap the badge. The existing `icon` from `get_reward_campaign` is the current value; preserve it otherwise.
- **`create_redemption_option`** / **`update_redemption_option`** — for the redemption image, if user wants to pick from the library.
- **`update_widget_settings`** / **`update_widget_style`** — for widget element icons, if customizing.

## Constructing the IconView object (minimal shape)

When setting a badge on a campaign, the API expects `challengeBehaviour.icon` with **only these 3 fields** — verified from the dashboard's actual POST body:

```json
{
  "name": "<icons[i].name>",
  "fileName": "<icons[i].iconPath>",
  "iconTypeId": 1
}
```

- `name`: from the library entry's `name` field.
- `fileName`: from the library entry's `iconPath` field. **Note the API field rename**: library returns `iconPath`, the IconView field is `fileName`.
- `iconTypeId`: `1` (Challenge) for reward campaigns. Other surfaces use different IDs — see the per-tool codex entry.

**Do NOT include**: `id`, `isDeleted`, `creationDate`, `lastUpdate`. The backend fills these on insert. Including them works but adds noise.

## Default-when-user-doesn't-care (mirrors dashboard exactly)

The dashboard's behavior in `create-reward.component.ts:411-420` for any new campaign without an icon:

1. Wait for the icon library to load.
2. Set `challengeBehaviour.icon = libraryIcons[0]` (the first item in the array, with the 3-field minimal shape).
3. Set `challengeBehaviour.visibility = 2` (Not Visible).

The badge is stored but **hidden from the customer-facing widget**. The user can opt in later by changing visibility (the dashboard's "Add Badge" button defaults the modal toggle to "Always Visible" → flipping to `1`).

**Do NOT ask the user about the badge during create.** The dashboard never asks — it silently defaults. Match that: silent default + mention in post-create summary that the badge can be customized via `update_reward_campaign`.

**Never invent icon names** — always pick from the `get_icons` response.

## Folder parameter

Optional `folder` query parameter targets a different S3 folder. Omit it for the default `gb-library/general/` library, which is what the dashboard uses.

## Visibility enum (related)

Used together with the icon to control whether the badge displays:

- `1` — Always Visible (badge shown on widget)
- `2` — Not Visible (badge hidden — dashboard rewards list shows "No Badge")
- `3` — Visible If Earned (badge shown only after the customer earns the reward)

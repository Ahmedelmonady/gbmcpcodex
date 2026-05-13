# create_newsletter

Creates a newsletter subscription campaign (`SubscribeToNewsletter`).

{{> template_flow}}

## Required

- Campaign name and locales (set on `challengeBehaviour.locals[].gameName` per language — keep `extraTranslations` from template!).
- At least one reward.

## Ask the user (only if applicable and not already mentioned)

- **Audience** — "Target all customers (default), registered only, anonymous/guest, or a specific segment?"
- **Scheduling** — "Always active (default), or restrict to a specific date range?"
- **Budget** — "Set a budget limit? If yes, what's the total amount?"
- **Reward cap** — "Limit how many total rewards can be given out?"
- **Customizations** — "The template has a popup design with colors and text. Want to customize the heading, button text, or colors?"

## Badge (icon)

The template returned by `get_campaign_template('SubscribeToNewsletter')` includes the `news-letter` icon in `challengeBehaviour.icon`. **Preserve it as-is** unless the user wants to change it.

If the user wants to swap: call `get_icons` to fetch the library and replace `challengeBehaviour.icon`. See `codex://tools/get_icons` for the shape.

## Important

- MUST create as `isActive:false`. Activate separately via `toggle_reward_campaign_activation` after customer sync completes.
- Newsletter is always single occurrence. No repeatability or badge settings — the popup IS the campaign visual.

## Before submitting

Show the user a human-readable summary (NO raw IDs, operator numbers, or technical attributes — use friendly names only). Always state: "Will be created as inactive — activate when ready."

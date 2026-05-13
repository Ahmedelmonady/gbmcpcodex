# create_calendar_campaign

Creates a calendar campaign — a multi-day container with child campaigns per day.

## Two-step flow

1. **Create parent**: call `get_campaign_template('CalendarCampaign')` → set name, date range → call this tool.
2. **Create children**: for each day, call the appropriate create tool (`create_game_campaign`, etc.) with `parentChallengeId = parent ID`.

{{> core_required}}

## Badge (icon)

The template returned by `get_campaign_template('CalendarCampaign')` already includes a default calendar icon in `challengeBehaviour.icon`. **Preserve it as-is** for the parent unless the user wants to change it.

Each child campaign created with `parentChallengeId` gets its own icon — preserve the per-day template's icon (e.g., `calender-quiz` for quiz days, `calender-wheel` for spin days).

If the user wants to swap any icon: call `get_icons` and replace the `IconView`. See `codex://tools/get_icons`.

## Calendar-specific (ask if not provided)

- "What date range?" (start and end dates — REQUIRED for calendar)
- "What campaign type for each day?" (quiz, spin, scratch, etc.)
- Per-day details (e.g., quiz questions for quiz days)
- Each child MUST have `challengeBehaviour.startDate` and `.endDate` for its day window.
- Children are forced to single occurrence.
- Note: Calendar parent is inherently date-bound. No repeatability setting needed.

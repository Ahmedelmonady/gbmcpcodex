# get_campaign_template

Returns the seed-data template for a campaign type. **Call this BEFORE creating** — it returns the full object with all defaults (configurations, colors, images, localized game text, icon). Modify the fields the user wants, then pass the full object to the appropriate create tool.

## Parameter

`type` — campaign type enum name (case-insensitive). Accepted values:

- `SpinTheWheel`
- `SlotMachine`
- `ScratchAndWin`
- `Quiz`
- `MatchCardsCampaign`
- `Catcher`
- `TicTacToe`
- `SpaceShooter`
- `Puzzle`
- `TapTheTarget`
- `DrivingGame`
- `CalendarCampaign`
- `NonSequentialMission`
- `SpendingMilestone`
- `DateBased`
- `SubscribeToNewsletter`
- `EventBased`
- `ManualChallenge`
- `RewardCampaign`

## Notes

- For `EventBased`, the create tool builds from scratch instead of from a template — see `codex://tools/create_event_campaign`.
- The returned template includes `extraTranslations` — preserve them when modifying locales.

# create_game_campaign

Creates a game campaign: `SpinTheWheel`, `SlotMachine`, `ScratchAndWin`, `Quiz`, `MatchCardsCampaign`, `Catcher`, `TicTacToe`, `SpaceShooter`, `Puzzle`, `TapTheTarget`, `DrivingGame`.

{{> template_flow}}

{{> core_required}}

## Badge (icon)

The template returned by `get_campaign_template` already includes a per-game icon in `challengeBehaviour.icon` (e.g., `"scratch-bw"` for SpinTheWheel, `"spin-the-wheel"` for some variants). **Preserve it as-is** unless the user wants to change it.

If the user wants to swap: call `get_icons` to fetch the library, ask them to pick, and replace `challengeBehaviour.icon` with the new `IconView` object. See `codex://tools/get_icons` for the shape.

`challengeBehaviour.visibility` for game campaigns defaults to `1` (Always Visible) since games are meant to be discoverable from the widget.

## Game-specific (ask if not provided)

- **Reward segments** — "How many rewards? What does each award? Include a 'no luck' outcome?" (min 2 for Spin/Slot)
- **Repeatability** — "Can customers play multiple times, or once only?" Default from template: unlimited, once per day. Set `isUnlimitedOccurance`, `intervalLimit`, `timeIntervalTypeId` (1=Day, 2=Week, 3=Month).
- **Quiz ONLY** — "What questions? Answers? Which is correct? Time limit?" — set `configurations.questionsLocales[]`: `[{ langId, langCode, questions: [{ questionText, answers: [{ answerText, isCorrect }] }] }]`. No template default for questions.
- All game rewards use `rewardType:7`, optional `rewardType:8` for NoLuck.

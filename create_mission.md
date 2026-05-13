# create_mission

Creates a mission campaign (`NonSequentialMission`). Tasks can be completed in any order.

{{> template_flow}}

{{> core_required}}

## Badge (icon)

The template returned by `get_campaign_template('NonSequentialMission')` already includes a default mission icon in `challengeBehaviour.icon`. **Preserve it as-is** unless the user wants to change it.

If the user wants to swap: call `get_icons` to fetch the library and replace `challengeBehaviour.icon` with the new `IconView`. See `codex://tools/get_icons` for the shape.

## Mission-specific (ask if not provided)

- "What are the mission tasks?" (each task = one event from `get_events`, call `get_events` first)
- "Reward per step or only a completion reward?"
- Set `challengeEvents[]` with one event per task. Backend auto-creates `StepReward` per event.
- Note: Missions are single occurrence. No repeatability setting needed.

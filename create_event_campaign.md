# create_event_campaign

Creates an event-triggered campaign: `EventBased` or `SpendingMilestone`.

## Flow by type

- **EventBased** — do NOT call `get_campaign_template` — build from scratch. Call `get_events` first, then construct the object directly. EventBased is the ONLY type that skips the template.
- **SpendingMilestone** — MUST call `get_campaign_template('SpendingMilestone')` first — it has all visual defaults (progress bar, colors, images, localized text). Then call `get_events` for `GB_ITEM_PURCHASED` `eventId` + `total_paid` `metadataId`. Modify the template's existing `challengeEvents[0].challengeEventMetadata[0].value` — do NOT rebuild from scratch.

{{> core_required}}

## Badge (icon) — silent default, mirror the dashboard exactly

EventBased has no seed template, so nothing pre-populates the icon. **Do NOT ask the user about the badge during create.** The dashboard never asks either — it silently auto-defaults before POSTing. The user can opt in to a custom badge later via `update_reward_campaign`.

The dashboard's logic (`create-reward.component.ts:411-420`) for any new campaign without an icon:

```typescript
// Wait for icon library to load, then if no icon set yet:
icon.fileName    = libraryIcons[0].iconPath
icon.name        = libraryIcons[0].name
icon.iconTypeId  = IconTypes.Challenge          // = 1
challengeBehaviour.icon       = icon
challengeBehaviour.visibility = VisibilityTypes['Not Visible']   // = 2
```

### MCP equivalent flow (do this BEFORE every EventBased create)

1. Call `get_icons` to fetch the library — returns array of `{ name, iconPath }`.
2. Pick `libraryIcons[0]` (the first item).
3. Set `challengeBehaviour.icon` with the **minimal 3-field shape** the dashboard POSTs (verified from network capture). Backend fills `id`, `isDeleted`, `creationDate`, `lastUpdate` — do NOT include those:
   ```json
   "icon": {
     "name": "<libraryIcons[0].name>",
     "fileName": "<libraryIcons[0].iconPath>",
     "iconTypeId": 1
   }
   ```
4. Set `challengeBehaviour.visibility = 2` (Not Visible). The badge is stored but hidden from the customer widget — exactly how dashboard-created campaigns start.

After create, mention in your summary: "Badge defaulted to placeholder (`<name>`), hidden from widget. Use `update_reward_campaign` to customize the icon or set `visibility=1` to show it."

For **SpendingMilestone** — `get_campaign_template('SpendingMilestone')` returns the icon already populated. Preserve it as-is and do NOT call `get_icons`.

## Event-specific (ask if not provided)

- **EventBased** — "Which event triggers this?" (show options from `get_events`). "Any conditions?" (e.g., order total >= 500). Set `challengeBehaviour.behaviorTypeId` to `9`.
- **SpendingMilestone** — "What spending threshold amount?" Change the template's `challengeEvents[0].challengeEventMetadata[0].value` to the threshold.
- **Repeatability** — "Can customers earn this multiple times?" Default: once. Set `isUnlimitedOccurance` + `intervalLimit` if multiple.

## challengeEventMetadata structure (ALL fields required, even id:0 for new)

```
challengeEvents: [{
  id: 0,
  eventId: <int>,
  eventOccurrence: 1,
  logicalOperator: 0,
  challengeEventMetadata: [{
    id: 0,
    challengeEventId: 0,
    eventMetadataId: <int>,
    value: "<string>",
    operator: <int>
  }]
}]
```

**Operators**: `1`=Equals, `2`=EqualsOrGreater, `3`=AccumulativeTotal, `5`=Contains, `7`=Between. `value` MUST be string. Verify after creation with `get_reward_campaign`.

## EventBased example — "50 points when order total >= 500"

(Mirrors what the dashboard POSTs: icon auto-defaulted to `libraryIcons[0]`, visibility=2.)

```json
{
  "challengeBehaviour": {
    "behaviorTypeId": 9,
    "name": "Order Bonus",
    "gameName": "Order Bonus",
    "description": "Earn points",
    "visibility": 2,
    "activationCriteriaTypeId": 1,
    "icon": {
      "name": "<libraryIcons[0].name>",
      "fileName": "<libraryIcons[0].iconPath>",
      "iconTypeId": 1
    },
    "locals": [{
      "languageId": "<langId>",
      "name": "Order Bonus",
      "gameName": "Order Bonus",
      "description": "Earn points"
    }]
  },
  "isActive": false,
  "challengeEvents": [{
    "id": 0,
    "eventId": "<from get_events>",
    "eventOccurrence": 1,
    "logicalOperator": 0,
    "challengeEventMetadata": [{
      "id": 0,
      "challengeEventId": 0,
      "eventMetadataId": "<from get_events>",
      "value": "500",
      "operator": 2
    }]
  }],
  "rewardConfigurations": [{
    "rewardType": 1,
    "playerPoints": 50,
    "rewardOrder": 0,
    "locales": [{ "languageId": "<langId>", "rewardName": "50 points" }]
  }]
}
```

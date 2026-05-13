# get_events

Returns the client's events (triggers) with their IDs, names, and metadata fields.

## Response shape

Each event has:
- `id` — use as `eventId` in `challengeEvents[].eventId`
- `name` — system name
- `displayName` — friendly name
- `eventMetadata[]` — array of `{ id, key, isNumeric }`
  - `id` — use as `eventMetadataId` in `challengeEventMetadata[].eventMetadataId`
  - `key` — e.g. `"total_paid"`, `"product_id"`

## When to call

ALWAYS before any tool that takes an `eventId` — primarily `create_event_campaign` (EventBased) and `create_mission` (each task is an event).

## challengeEventMetadata structure

```
{
  eventMetadataId: <metadata.id>,
  value: "<threshold>",
  operator: <EEventOperators>
}
```

## EEventOperators

- `1` = Equals
- `2` = EqualsOrGreater
- `3` = AccumulativeTotal
- `4` = DifferentValues
- `5` = Contains
- `6` = RepeatedValues
- `7` = Between

## Notes

- `value` is ALWAYS a string, even for numeric metadata.
- Verify created campaigns by calling `get_reward_campaign` after — confirms `eventId` and metadata wired correctly.

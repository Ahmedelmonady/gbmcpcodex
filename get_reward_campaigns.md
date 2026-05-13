# get_reward_campaigns

Lists reward campaigns with pagination and filtering (slim payload: `id`, `name`, `behaviorType`, `isActive`, `gbCode`). For full details (rewards, events, audience, scheduling) on a specific campaign, use `get_reward_campaign` with an ID.

## Filter syntax

Semicolon-delimited conditions joined by `;f;` (AND logic).
Format: `{field} {operator} {value}` separated by `;f;`.

## Available filters (mirrors the dashboard rewards-list filters)

| Filter | Syntax | Example |
|--------|--------|---------|
| Created after | `cdate ge {date}` | `cdate ge 2026-01-01` |
| Created before | `cdate le {date}` | `cdate le 2026-03-31` |
| Campaign name (contains) | `cname in {text}` | `cname in welcome` |
| Display name (contains) | `dname in {text}` | `dname in spring` |
| Rank Points >= | `frubies ge {int}` | `frubies ge 100` |
| Rank Points <= | `frubies le {int}` | `frubies le 500` |
| Wallet Points >= | `points ge {int}` | `points ge 50` |
| Wallet Points <= | `points le {int}` | `points le 200` |
| Active status | `status eq {bool}` | `status eq true` |
| Visibility | `visibility eq {id}` | `visibility eq 1` (1=Always Visible, 2=Not Visible, 3=Visible If Earned) |
| Behavior type | `behavior eq {id}` | `behavior eq 15` |
| Activation Settings | `activation eq {id}` | `activation eq 1` (1=Always Active, 2=Scheduled) |
| Repeatability | `repeatability eq {id}` | `repeatability eq -1` (-1=Unlimited, otherwise occurrence count) |
| In-App Notification Status | `notifyStatus eq {id}` | `notifyStatus eq 2` (1=Global, 2=On, 3=Off) |
| Email Notification Status | `emailStatus eq {id}` | `emailStatus eq 2` (1=Global, 2=On, 3=Off) |

## Behavior type IDs

The dashboard exposes these 14 options:

`4`=HighScore, `5`=Signup (UponLogin), `7`=Birthday, `8`=JoinAnniversary, `9`=EventBased, `10`=SocialActivities, `11`=ScheduledChallenge, `12`=DailyStreak, `15`=SpinTheWheel, `17`=Popup (SubscribeToNewsletter), `18`=SlotMachine, `19`=Quiz, `20`=CalenderCampaign, `21`=ScratchAndWin.

## Combined example

```
status eq true;f;behavior eq 15;f;cname in welcome
```

## User prompting

If the user's request is vague, ask what they'd like to filter by — by name, status (active/inactive), behavior type, visibility, activation, repeatability, notification status, or creation date. Present results as a friendly readable list, not raw JSON.

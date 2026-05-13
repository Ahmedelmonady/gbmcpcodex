# get_customers

Lists customers with pagination and filtering. Returns slim payload: `id`, `externalId`, `displayName`, `email`, `currentLevelName`, `accPoints`, `pendingAccPoints`, `isActive`, `accountState`, `creationDate`. For full details, use `get_customer_details` with the `externalId`.

## Filter syntax

Semicolon-delimited conditions joined by `;f;` (AND logic).
Format: `{field} {operator} {value}` separated by `;f;`.

## Available filters

| Filter | Syntax | Example |
|--------|--------|---------|
| External ID (contains) | `id in {text}` | `id in john123` |
| Display name (contains) | `name in {text}` | `name in John` |
| Phone (contains) | `phone in {text}` | `phone in +201` |
| Email (contains) | `email in {text}` | `email in john@test.com` |
| Tier (by IDs) | `level in {id,id}` | `level in 1,2,3` |
| Points >= | `points ge {int}` | `points ge 500` |
| Points <= | `points le {int}` | `points le 1000` |
| Points range | `points between {min},{max}` | `points between 100,500` |
| Pending points >= | `ppoints ge {int}` | `ppoints ge 50` |
| Pending points <= | `ppoints le {int}` | `ppoints le 200` |
| Pending points range | `ppoints between {min},{max}` | `ppoints between 0,100` |
| Score >= | `frubies ge {int}` | `frubies ge 100` |
| Score <= | `frubies le {int}` | `frubies le 500` |
| Score range | `frubies between {min},{max}` | `frubies between 50,200` |
| Created after | `cdate ge {date}` | `cdate ge 2026-01-01` |
| Created before | `cdate le {date}` | `cdate le 2026-03-31` |
| Active status | `active eq {bool}` | `active eq true` |
| Guest status | `isguest eq {bool}` | `isguest eq true` |
| Tags (by IDs) | `tags in {id,id}` | `tags in 5,10,15` |

## Combined example

```
level in 1,2;f;points ge 100;f;active eq true
```

## Important

Tier and tag filters use **IDs**, not names. Call `get_tiers` or `get_tags` first to resolve names to IDs.

## User prompting

If the user's request is vague (e.g. "show me customers"), ask what filters they'd like before calling. Suggest common options: by tier, points balance, tag, active status, or date range. Present results in a friendly readable format — not raw JSON.

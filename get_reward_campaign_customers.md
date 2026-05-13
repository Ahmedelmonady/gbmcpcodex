# get_reward_campaign_customers

Lists achievement records on a specific reward campaign with pagination and filtering. Each row is one customer's reward earned (or a NoLuck outcome for game campaigns). Includes customer info, achievement date, points/frubies awarded, voucher/coupon, and a `success` flag.

## Default behavior

Returns **EVERY achievement record** — winners and NoLuck losers (game campaigns) or just earners (non-game campaigns).

## To list ONLY winners

For game campaigns: add `success eq true` to the filter to exclude NoLuck rows.
For non-game campaigns: this filter is a no-op (no NoLuck concept exists).

## Game campaigns where success matters

`SpinTheWheel`, `SlotMachine`, `ScratchAndWin`, `Quiz`, `Catcher`, `MatchCards`, `TicTacToe`, `SpaceShooter`, `Puzzle`, `TapTheTarget`, `DrivingGame`.

All others (`EventBased`, `SpendingMilestone`, `Birthday`, `DateBased`, `NonSequentialMission`, `Newsletter`, etc.) have no NoLuck records — `success eq true` always matches all rows.

## Filter syntax

Semicolon-delimited conditions joined by `;f;` (AND logic). Format: `{field} {operator} {value}` separated by `;f;`.

## Available filters (mirrors the dashboard reward-customers-list filters)

| Filter | Syntax | Example |
|--------|--------|---------|
| External ID (contains) | `id in {text}` | `id in john123` |
| Display name (contains) | `name in {text}` | `name in John` |
| Email (contains) | `email in {text}` | `email in john@test.com` |
| Reward Points >= | `points ge {int}` | `points ge 50` |
| Reward Points <= | `points le {int}` | `points le 200` |
| Reward Frubies >= | `frubies ge {int}` | `frubies ge 10` |
| Reward Frubies <= | `frubies le {int}` | `frubies le 100` |
| Achieved after | `cdate ge {date}` | `cdate ge 2026-01-01` |
| Achieved before | `cdate le {date}` | `cdate le 2026-03-31` |
| Tags (by IDs) | `tags in {id,id}` | `tags in 5,10,15` |
| Game success | `success eq {bool}` | `success eq true` (true=won, false=NoLuck — applies to game campaigns: Quiz, Catcher, SpinTheWheel, SlotMachine, ScratchAndWin, etc.) |
| Voucher product (contains) | `voucherpname in {text}` | `voucherpname in t-shirt` |
| Voucher discount >= | `voucherdicount ge {number}` | `voucherdicount ge 10` |
| Voucher discount <= | `voucherdicount le {number}` | `voucherdicount le 50` |
| Free shipping voucher | `vouchershipping sl {any}` | `vouchershipping sl 1` |
| Merchant name (contains) | `mname in {text}` | `mname in acme` |
| Branch name (contains) | `bname in {text}` | `bname in downtown` |
| Merchant IDs | `merchants id {id,id}` | `merchants id 1,2` |
| Branch IDs | `branches id {id,id}` | `branches id 5,8` |
| Achievement rank IDs | `rank in {id,id}` | `rank in 1,2,3` |

## Combined example

```
cdate ge 2026-01-01;f;success eq true;f;tags in 5,10
```
(winners on or after Jan 1, with tags 5 or 10)

## Important

Tag filters use IDs, not names. Call `get_tags` first to resolve names to IDs.

## User prompting

If the user asks "who won my Spin-The-Wheel" or "who got rewarded by my Quiz", call this tool with `success eq true` in the filter. If they ask "who participated" or want full audit, call without `success eq true`. Ask which campaign first if not specified — use `get_reward_campaigns` to list options. Present results in a friendly readable format, not raw JSON.

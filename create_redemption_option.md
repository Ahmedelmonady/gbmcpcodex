# create_redemption_option

Creates a new redemption option that defines how customers spend loyalty points.

## Pre-requisites (call BEFORE creating)

- `get_supported_languages` — discover available `languageId` values for `rewardNames` and `redeemInstructions`.
- `get_tags` — discover tag/segment IDs for audience targeting (use IDs not names).
- `get_collections` — if restricting to specific product collections.
- `get_merchants` — if restricting to specific merchants.

## Rule types

| Type | Use case | Required |
|---|---|---|
| `fixed_rate_settings` | Fixed currency discount (e.g., $5 off) | `discountValue` |
| `percentage_discount_settings` | Percentage off (e.g., 10%) | `discountValue` (1-100). Use `capping` to limit max discount. |
| `free_shipping_settings` | Free shipping coupon | (none beyond core) |
| `free_product_settings` | Free product reward | `productId`, `productName` |
| `custom` | Third-party coupon | `couponGroupHandle` |

## Validation

- `pointsToRedeem >= 1` (always required)
- `discountValue` required for `fixed_rate` and `percentage` types
- `percentage` `discountValue` must be `1-100`
- `couponGroupHandle` required for `custom` type
- `productId` required for `free_product` type
- **General type cannot be created** — one per client, auto-created by backend

## Audience targeting

- `audience[].key` — `Segment`, `Tag`, `RFM`, or customer attribute key
- `audience[].operator`:
  - For `Tag` / `Segment` / `RFM`: `9`=In, `13`=NotIn
  - For customer attributes: `1`=Is, `2`=GreaterThan, `3`=LessThan, `4`=Equals, `5`=Contains, `12`=NotEquals
- `audience[].value` — tag/segment ID (number as string) or comma-separated IDs for multi-select
- `audienceLogicalOperator` — `and` or `or` between rules (max 5 rules)

## Cashback variants

- `isCashback: true` on `fixed_rate` or `percentage` → cashback reward (deferred credit)
- `applyToFees: true` on `percentage` → discount applies to fees only

## Image / icon

- If the user wants a custom icon, ask for the local file path and pass as `imagePath` — the tool uploads it via `utilsApi.uploadImage()` and sets `iconPath` on the create payload.
- Supported formats: `.jpg`, `.jpeg`, `.png`, `.gif` (max 1MB).
- If `imagePath` is omitted, the default icon is used.
- Alternatively, the user can pick from the icon library — call `get_icons` and pass the URL via `iconPath` directly (skip upload).

## User prompting

1. Ask: "What kind of reward — fixed currency discount, percentage off, free shipping, free product, or a custom third-party coupon?"
2. Ask for the points cost.
3. For fixed_rate/percentage: ask for the discount amount.
4. For free_product: ask for the product ID/name.
5. Ask about audience scope (all customers / specific tags or segments).
6. Show a friendly summary, confirm, then call.

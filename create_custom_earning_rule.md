# create_custom_earning_rule

Creates a custom earning rule with conditions (merchant, collection, channel, etc.) and a specific point reward.

## Config modes (choose one)

- **`percentage`** — X% cashback of order amount. Set `walletCashback`.
- **`per_unit`** — X points per $Y spent. Set `rewardWalletFactor` and `amountRewardThreshold`.
- **`fixed`** — flat X points per qualifying order. Set `equivalentPoints`.

## Conditions — define which orders qualify

| Field Path | Description | Example matchValue |
|---|---|---|
| `Merchant.ExternalId` | Merchant ID(s) | `deraah` or `deraah,zara` |
| `Merchant.Branch.ExternalId` | Branch ID(s) | `branch_123` |
| `OrderLineItems.Collection` | Product collection(s) | `summer-sale` |
| `OrderLineItems.Category` | Product category | `Electronics` |
| `OrderLineItems.Vendor` | Vendor name | `Nike` |
| `OrderLineItems.Sku` | Product SKU(s) | `SKU-001,SKU-002` |
| `OrderLineItems.Tags` | Product tags | `new-arrival` |
| `Order.Channel` | Order channel | `WEB,POS` |
| `Order.Extra.<field>` | Custom order field | any value |

## Operators

**Condition operators**: `1`=Equals, `2`=NotEquals, `7`=Contains, `8`=NotContains.

**Logical operators** (between conditions): `1`=AND, `2`=OR.

## Discovery tools (call BEFORE creating to resolve IDs/values)

- `get_merchants` — resolve merchant names to ExternalIds for `Merchant.ExternalId` conditions.
- `get_collections` — resolve collection names to IDs for `OrderLineItems.Collection` conditions.

## User prompting — interactive process

1. Ask: "What should this rule be called?"
2. Ask: "Which orders should qualify?" — call `get_merchants` or `get_collections` to show available options.
3. Ask: "How should customers be rewarded?" — explain the three options:
   - Percentage cashback (e.g. 5% of order amount)
   - Points per amount spent (e.g. 2 points per $10)
   - Fixed points per order (e.g. 1000 points flat)
4. Ask for the reward value based on the chosen mode.
5. Show a friendly summary before creating: rule name, conditions, reward type + value.
6. Confirm: "Ready to create this custom earning rule?"

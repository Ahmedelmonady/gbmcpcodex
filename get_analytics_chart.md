# get_analytics_chart

Fetches one analytics chart from the dashboard analytics service. Mirrors what the dashboard fetches per-card on its analytics pages.

## Required parameters — ask if missing

1. **`chartName`** — pick one of the 90 friendly names from the catalog below. If the user's request doesn't make the chart obvious, ask which one. Echo the chosen name back before calling.

## Optional parameters

- `from` / `to` — ISO 8601 datetimes, inclusive on both ends (`from` at `00:00:00.000`, `to` at `23:59:59.999`). **Default = last 30 days.** Convert user-stated periods ("April", "last quarter") to absolute ISO 8601 with day boundaries.
- `groupingType` (`Daily | Weekly | Monthly`) — default per chart (catalog `Default grouping` column). Surfaced in the combined ask in step 2 when `defaultGrouping ∈ {Daily, Weekly, Monthly}`; not user-selectable on `None`/`Category` charts.
- `aggregationType` (`Sum | Count | AVG`) — leave unset; the analytics service applies each chart's natural aggregation. Only set if the user explicitly asks for an override.
- `tag` — segment/audience filter. Don't ask proactively (dashboard defaults to "All Tags"). Only set when the user names a segment, then resolve via `get_tags` and confirm the match before re-running.
- `challengeId` — only meaningful on a few campaign-related charts. Don't ask proactively. Only set when the user names a specific reward campaign, then resolve via `get_reward_campaigns` and confirm the match before re-running.

## Available charts (90)

### Member Analytics (11)

| Chart | Type | Default grouping |
|---|---|---|
| Enrolled Members | card | None |
| Excluded Members | card | None |
| New Members | card | None |
| Member Growth | line | Monthly |
| Tier Distribution (Members) | bar | Category |
| Engagement Rate | line | Monthly |
| Engaged Customers | line | Monthly |
| Engagement Interactions | line | Monthly |
| Retention Rate | line | Monthly |
| Customers Who Placed Orders | line | Monthly |
| Retention Cohort | heatmap | Category |

### Purchase Behavior (13)

| Chart | Type | Default grouping |
|---|---|---|
| Customer Growth | line | Daily |
| Customer LTV by Segment | line | None |
| Attributed Sales | card | None |
| Attributed Revenue | card | None |
| Attributed Revenue Over Time | bar | Monthly |
| Revenue Contribution | bar | Monthly |
| Average Order Value (AOV) | card | Monthly |
| Order Frequency | card | Monthly |
| Average Basket Size (ABS) | card | Monthly |
| AOV by Redeemer Segment | line | Monthly |
| Order Frequency by Segment | line | Monthly |
| ABS by Redeemer Segment | line | Monthly |
| Transaction Volumes | line | Monthly |

### Points & Rewards (32)

| Chart | Type | Default grouping |
|---|---|---|
| Total Available Points | card | None |
| Total Pending Points | card | None |
| Expiring Points (Next 15 Days) | card | None |
| Total Accumulated Points | card | Monthly |
| Accumulated Points by Source | bar | Monthly |
| Total Deducted Points | card | Monthly |
| Deducted Points by Type | bar | Monthly |
| Redeemed Points by Type | bar | Monthly |
| Redemption Rate | bar | Monthly |
| Total Coupons Issued (Reward Source) | card | None |
| Total Coupons Burned (Reward Source) | card | None |
| Coupons Reward by Source | bar | Monthly |
| Top Created Coupons (Reward Source) | bar | Category |
| Top Burned Coupons (Reward Source) | bar | Category |
| Total Issued Coupons | card | None |
| Total Used Coupons | card | None |
| Coupon Usage Rate | card | None |
| Coupons Issued by Source | bar | Daily |
| Coupons Used by Source | bar | Daily |
| Coupons Issued by Type | bar | Daily |
| Coupons Used by Type | bar | Daily |
| Issued vs Used Coupons Trends | line | Monthly |
| Orders With Coupons | card | None |
| Order Value With Coupons | card | None |
| AOV With Coupons | card | None |
| AOV Without Coupons | card | None |
| Top Issued Coupons | bar | Category |
| Top Used Coupons | bar | Category |
| Total Coupons Expired | card | None |
| About to Expire Coupons | card | None |
| Coupon Expiry Rate | card | None |
| Coupon Expiry Trends | line | Monthly |

### Campaign Performance (8)

| Chart | Type | Default grouping |
|---|---|---|
| Reward Campaign Reach | card | None |
| Customers Who Achieved Reward Campaigns | card | None |
| Campaigns Cost in Points (Trend) | line | Monthly |
| Campaigns Coupons Issued (Trend) | line | Monthly |
| Top Achieved Campaigns | bar | Category |
| Top Points-Cost Campaigns | bar | Category |
| Top Coupon-Issuing Campaigns | bar | Category |
| Widget Funnel Game Performance | table | None |

### Referral Analytics (6)

| Chart | Type | Default grouping |
|---|---|---|
| Pending Referrals | card | None |
| Successful Referrals | card | None |
| Successful Referrals Rate | bar | Monthly |
| Total Referral Revenue | card | None |
| Total Revenue by Referral (Trend) | line | Monthly |
| Top Referring Customers | bar | Category |

### Tiers Performance (14)

| Chart | Type | Default grouping |
|---|---|---|
| Tier Upgrade Percentage | card | None |
| Tier Downgrade Percentage | card | None |
| Tier No-Change Percentage | card | None |
| Tier New Static Joiners Percentage | card | None |
| Tier Transition Trends | line | Monthly |
| Orders per Tier | bar | Category |
| Time Spent per Tier | bar | Category |
| Tiers Members Distribution | pie | Category |
| Stagnating Members per Tier | bar | Category |
| Revenue per Tier | bar | Category |
| Points Breakdown per Tier | table | None |
| Revenue Breakdown per Tier | table | None |
| Tier Performance Prediction | table | Category |
| Tiers Names and IDs | table | Category |

### Redemption Options (5)

| Chart | Type | Default grouping |
|---|---|---|
| Total Issued Coupons (Redemption Options) | card | None |
| Total Burned Coupons (Redemption Options) | card | None |
| Average Burn Rate (Redemption Options) | card | None |
| Total Expired Coupons (Redemption Options) | card | None |
| Redemption Options Performance | table | None |

### Home Analytics (1)

| Chart | Type | Default grouping |
|---|---|---|
| Home Revenue Distribution | table | None |

## Common questions and the chart that answers them

- "How many active members?" → **Enrolled Members**
- "Member growth this quarter?" → **Member Growth** + `groupingType: monthly`
- "Which campaigns have the most achievements?" → **Top Achieved Campaigns**
- "Referral revenue trend?" → **Total Revenue by Referral (Trend)** + `groupingType: monthly`
- "Tier upgrade rate?" → **Tier Upgrade Percentage**
- "Average order value?" → **Average Order Value (AOV)**
- "Coupon usage rate?" → **Coupon Usage Rate**

## Interaction protocol

1. **Pick the chart.** If intent is ambiguous ("how is engagement?"), pick which lens (rate / count / interactions / retention) — ask the user only if you genuinely can't tell.
2. **Bucket-size ask** — only when `defaultGrouping ∈ {Daily, Weekly, Monthly}`. Phrasing: *"Bucket size — default is **<defaultGrouping>**. Keep that, or pick `Daily`/`Weekly`/`Monthly`?"* Wait for the user's reply. Skip this step entirely on charts whose `defaultGrouping` is `None` or `Category` (grouping is fixed).
3. Call the tool with the agreed values.
4. **Render in two parts** — always table first, then the chart in its **defined natural type from the catalog `Type` column** (no chart-type prompt, no opt-in, no choice):
   - **Part A — Markdown table**: always render the raw values as a markdown table with explicit column headers (metric name + units, e.g. `| Week starting | New members | % vs prior |`), thousands-separator formatted numbers. This is the source of truth.
   - **Part B — Chart in its natural type**: directly render the chart in the type from the catalog. Do NOT ask the user which type they want — the type is fixed by the chart's natural format. For `card` charts, skip Part A and just render the bolded value + trend (cards are scalar — no table or chart needed).

   **Where each rendered element comes from in the tool response (`data` object):**
   - `data.title` → chart title (heading above the chart)
   - `data.series[]` → array of `{ name, data }`. Single series → use `series[0]`. Multi-series → iterate; each `series[i].name` is a legend entry, `series[i].data` is the value array.
   - `data.xAxis.categories` → x-axis tick labels (dates or category names). Fall back to `data.labels` if `xAxis.categories` is empty/missing.
   - `data.labels` → legend labels (also used for pie slice labels and heatmap rows).
   - `data.metric` → for `card` charts: `currentValue` (the bolded number), `previousValue` + `delta` (the ▲/▼ trend), `postText` (small suffix label).
   - `data.tableData` → for `table` and `heatmap` charts: rows of `{ key: value }` records (column headers come from the keys).
   - `data.agg` → aggregation type that was applied (informational; surface only if the user asks).

   Always ground the rendering in these exact fields — don't invent labels or values that aren't in the response.

   **ASCII rendering recipes** — clarity-first; always label axes, label every series, and surface every data point's numeric value:
   - **`bar`** → vertical bars from `███` blocks. **Y-axis** on the left with `┤` ticks, k/M-suffixed labels, metric label from `data.series[0].name` at the top. **X-axis** on the bottom (`└─→`) with `data.xAxis.categories` (or `data.labels`) as ticks. **Numeric value from `data.series[0].data[i]` under each bar.** Multi-series → side-by-side bars per category from `data.series[]` + a **legend** line above using `series[i].name` (e.g. `■ Series A  ■ Series B`).
   - **`line`** → ⚠️ **DO NOT draw a freehand ASCII line plot. It will break.** Repeated past attempts produced misaligned axes, ghost markers, step rectangles, and improvised box-drawing characters. The deterministic recipe below is the ONLY allowed render path — emit exactly these three pieces, in this order, and nothing else:
     **(a) Sparkline** — one line, mandatory, can't misalign:
       1. Compute `Y_max` = next "nice" number ≥ `max(data.series[0].data)`. Nice = `10^k × {1, 2, 2.5, 5}`.
       2. For each value `v` in `data.series[0].data`, pick the corresponding character from `▁▂▃▄▅▆▇█` based on `round(v × 7 / Y_max)` (0 → `▁`, 7 → `█`).
       3. Join the characters with no separator. Output as one line, prefixed by `data.series[0].name`.

       Example for values `[250k, 310k, 370k, 370k, 200k, 100k]` (Y_max = 400k): `Orders: ▅▆██▄▂   peak ~370k Apr 6–13, ▼73% by Apr 27`.

       Multi-series → one sparkline line per `data.series[i]`, each prefixed by its name.

     **(b) Mermaid `xychart-beta` block** — mandatory; renders inline in Claude Code as a real chart. Pull values directly from the response:
       ```mermaid
       xychart-beta
           title "<data.title>"
           x-axis [<comma-separated data.xAxis.categories or data.labels>]
           y-axis "<data.series[0].name>" 0 --> <Y_max>
           line [<comma-separated data.series[0].data>]
       ```
       Multi-series → one `line [...]` per `data.series[i].data` with a 1-line note above naming each series in order (Mermaid `xychart-beta` does not yet have native series labels).

     **(c) Markdown table** — already part of step 4 Part A; the table is the source of truth and remains mandatory.

     That's it — no freehand ASCII line plot, no `╭╮╰╯` rounded corners, no step rectangles, no improvised y-axis labels. The sparkline gives at-a-glance trend, the Mermaid block gives a real chart on capable hosts, the table gives exact values. All three are deterministic — character-for-character predictable from the response data.
   - **`pie`** → category rows sorted largest→smallest, each showing label, proportional bar, percentage, and absolute value (e.g. `VIP    │ ████████████░░░░░░░  45%   (3,421)`). Total below. (Mermaid `pie` block is also acceptable for hosts that render it.)
   - **`heatmap`** → emoji grid cool→hot `⬜🟪🟦🟩🟨🟧🟥` with row + column labels. One-line **color→value legend** (e.g. `⬜ 0–10%   🟪 10–25%   🟦 25–50%   🟩 50–75%   🟨 75–90%   🟧 90–95%   🟥 95–100%`). For small grids, append numeric value per cell (e.g. `🟦 42%`).
   - **`table`** → if the chart's natural type IS `table`, only render Part A (the markdown table is the chart). Skip Part B.
5. **Tag / Campaign** — only when the user mentions a segment or specific campaign by name or ID. Resolve names via `get_tags` / `get_reward_campaigns`, confirm the match ("Found <name> (ID <id>) — use this one?"), then re-run the tool with the resolved id. Otherwise leave unset (default = all). Never invent an ID, never pass a raw name.
6. Show raw JSON only if the user explicitly asks for it.

---
name: feishu-broadcast
description: "Send scheduled data broadcasts to Feishu groups — table images, text summaries, multi-pin reports with ROI analysis."
---

# Feishu Broadcast

Automated data broadcast to Feishu group chats — scheduled reports with formatted table images, text summaries, and ROI analysis.

## Architecture

- **Data Source**: MySQL promotion data tables
- **Processing**: Python scripts aggregate by pin/channel/format
- **Rendering**: PIL table image generation or text formatting
- **Delivery**: Feishu API upload + send to group chat

## Broadcast Types

### Table Image Broadcast
1. Query data from promotion table (filter by date, pin, time_range='当天')
2. Aggregate by dimension (pin, Format, category)
3. Compare with plan targets
4. Calculate YoY metrics
5. Generate formatted table image with PIL
6. Upload image to Feishu API
7. Send to target group chat

### Text Summary Broadcast
1. Query and aggregate data
2. Format as aligned text table
3. Add emoji indicators (🔥 high ROI, ⚠️ low ROI)
4. Send as text message

## Key Configuration

| Config | Description | Example |
|--------|-------------|---------|
| `PIN_CHANNEL` | Pin to channel mapping | `{"swisse_群邑推广": "跨境"}` |
| `PIN_DISPLAY` | Pin display names | `{"swisse_群邑推广": "自营跨境"}` |
| `FORMAT_ORDER` | Format display order | `["快车", "推荐广告", "海投"]` |
| `FORMAT_SQL` | Format classification CASE WHEN | SQL CASE statement |
| `CHAT_ID` | Target Feishu group | `oc_xxxxx` |

## Critical Rules

1. **ALWAYS filter by `time_range='当天'`** — Multiple snapshots exist per day
2. **Check data freshness** — Verify latest date per pin before querying
3. **Handle empty results** — Exit with error, not silent failure
4. **Plan date fallback** — If plan table lacks target date, use latest available
5. **Avoid double counting** — When plan has both '整体' and individual channels, prefer '整体' directly

## Image Generation Tips

- No borders — use background color alternation
- Row height: ~40px
- Header with gray background
- Chinese font: SimHei or equivalent
- Max width: ~800px for mobile
- Add ▲/▼ indicators for YoY changes

## Cron Scheduling

Typical schedules:
- Every 2 hours: `0 10,12,14,16,18,20,22 * * *`
- Three times daily: `0 10,14,16 * * *`

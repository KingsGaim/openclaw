---
name: travel-planner-skill
description: "Plan trips — search flights, hotels, attractions, create day-by-day itineraries with maps and budgets."
---

# Travel Planner

Plan trips with flight/hotel/attraction search, itinerary creation, and budget estimation.

## Core Workflow

1. **Gather requirements** — Destination, dates, budget, preferences
2. **Research** — Use web_fetch for flights, hotels, attractions
3. **Build itinerary** — Day-by-day plan with activities
4. **Budget estimate** — Flight + hotel + food + activities
5. **Output** — Formatted itinerary document

## Output Format

```markdown
# 🗓️ 上海 → 东京 5日游

## ✈️ 交通
- 航班: XXX, ¥3,200/人, 5/15 08:00-12:30
- 返程: XXX, ¥2,800/人, 5/19 14:00-16:30

## 🏨 酒店
- XXX Hotel (银座), ¥800/晚 × 4晚 = ¥3,200

## 📋 每日行程
### Day 1 (5/15) — 到达 + 银座
- 12:30 到达成田机场
- 14:00 酒店入住
- 15:00 银座逛街
- 18:00 晚餐: 寿司大

### Day 2 (5/16) — 浅草 + 涩谷
...

## 💰 预算
| 项目 | 费用 |
|------|------|
| 机票 | ¥6,000 |
| 酒店 | ¥3,200 |
| 餐饮 | ¥2,000 |
| 交通 | ¥500 |
| 门票 | ¥800 |
| **合计** | **¥12,500/人** |
```

## Tips

- Use `web_fetch` for real-time flight/hotel prices
- Check visa requirements for international trips
- Consider season/weather for outdoor activities
- Build in buffer time between activities
- Group nearby attractions on same day
- Suggest local transport options

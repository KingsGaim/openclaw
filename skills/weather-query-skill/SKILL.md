---
name: weather-query-skill
description: "Query current weather and forecasts for any location. Supports multiple data sources."
---

# Weather Query

Get current weather and forecasts for any location.

## Tools

- **weather** skill: `~/.nvm/versions/node/v24.14.0/lib/node_modules/openclaw/skills/weather/SKILL.md`
- **weather-query** skill: `~/.openclaw/skills/weather-query/SKILL.md`

## Core Workflow

1. Resolve location name to coordinates/city code
2. Fetch current weather data
3. Optionally fetch forecast (3-7 days)
4. Format output with emoji indicators

## Output Format

```
📍 上海 | 2026-05-31 12:00
🌤️ 晴转多云 | 26°C (体感 28°C)
💧 湿度: 65% | 🌬️ 东南风 3级
🌡️ 最高 30°C / 最低 22°C
```

## Weather Icons

- ☀️ 晴天
- 🌤️ 晴转多云
- ⛅ 多云
- 🌥️ 阴
- 🌧️ 小雨
- 🌦️ 阵雨
- ⛈️ 雷阵雨
- 🌨️ 小雪
- ❄️ 雪
- 🌫️ 雾/霾

## Tips

- Include temperature in °C (Chinese standard)
- Add "体感温度" (feels like) when available
- Mention wind direction and level
- For outdoor plans: highlight rain/wind/UV alerts

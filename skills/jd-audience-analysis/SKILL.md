---
name: jd-audience-analysis
description: "Analyze JD (京东) audience data — 4A funnel, audience efficiency, new/old customer, competitor flow, keyword penetration. 18 analysis scenarios."
---

# JD Audience Analysis

Analyze JD (京东)人群 data for brand/marketing insights. Based on standard ISV analysis framework with 18 scenarios.

## Data Sources

- **Excel reports**: `isv 常用分析 topic` files with 18 sheets
- **Audience packages**: 人群包配置 Excel files (378+ packages)
- **Rolling period**: R365 days

## 18 Analysis Scenarios

| # | Scenario | Purpose | Key Metrics |
|---|----------|---------|-------------|
| 1 | 站外人群效率调优 | CID vs organic efficiency | TTL, paid ratio, repurchase |
| 2 | 扩展人群匹配 | Dimension matching | TTL volume, match rate |
| 3 | 派样人群复购分析 | Sample→full purchase | Sample count, repurchase rate |
| 4 | 高价值人群渗透 | High-value penetration | Penetration rate, TGI |
| 5 | 4A人群流转 | A1→A2→A3→A4 conversion | Flow rate, profile GAP |
| 6 | 新老客分析 | New vs repeat customers | New ratio, repurchase rate |
| 7 | 品牌竞品流入流出 | Competitor flow analysis | Inflow, outflow, net flow |
| 8 | 行业及竞品价格带分析 | Price band analysis | Distribution by price |
| 9 | 货品矩阵差异化 | Product matrix | SKU contribution |
| 10 | 品牌货品竞争得失 | Item competition | Share gain/loss |
| 11 | 品牌货品浏览未购去向 | Browse-no-purchase analysis | Destination brands |
| 12 | 转化频次&周期 | Purchase frequency | Repurchase cycle |
| 13 | 快车关键词渗透 | Keyword penetration | Search volume, penetration |
| 14 | 触点深浅资产分布&权重 | Touchpoint efficiency | Deep/shallow ratio |
| 15 | 触点获客成本 | CPA comparison | Cost, ROI |
| 16 | 搜索词渗透拆解 | Search word breakdown | Volume, penetration |
| 17 | 品类品牌竞品搜索量 | Category search comparison | Volume, share |

## Key Methodologies

### 4A Funnel
```
A1(了解) → A2(兴趣) → A3(购买) → A4(忠诚)
```
- Track flow rate between stages
- Identify profile gaps between stages
- A2 cross-category preferences

### New/Old Customer
```
新客占比 = 新客数 / 总购买
老客复购率 = 老客复购人数 / 老客总数
```

### Competitor Flow
```
净流入 = 流入量级 - 流出量级
```
Positive = gaining from competitors
Negative = losing to competitors

### TGI Interpretation
- TGI > 100: Above average
- TGI < 100: Below average

### Audience Package Naming
```
GM-营养保健行业-购买-260101_0228-剔15
│   │            │    │          │    └─ Price filter (≥15元)
│   │            │    │          └─ Period (26年1-2月)
│   │            │    └─ Type (购买/行业新/行业老/品牌新/品牌老)
│   │            └─ Scope (类目/品牌/店铺/SKU/关键词)
│   └─ Category
└─ GM = Grand Master prefix
```

### Set Operations
- **Intersection (∩)**: Meet multiple conditions
- **Union (∪)**: Meet any condition
- **Difference (-)**: Exclude specific audience

## Quick Response Guide

| User asks | Use scenario | Sheet |
|-----------|-------------|-------|
| "人群效率" | Efficiency analysis | 站外人群效率调优 |
| "新老客占比" | New/old customer | 新老客分析 |
| "竞品抢了多少" | Competitor flow | 流入流出 |
| "关键词效果" | Keyword penetration | 快车关键词 |
| "复购情况" | Repurchase | 派样复购 |
| "4A流转率" | 4A funnel | 4A人群流转 |

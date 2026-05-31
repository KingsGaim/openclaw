---
name: data-visualization
description: "Generate charts, graphs, and data visualizations using Python (matplotlib, seaborn, PIL). Create table images for broadcast."
---

# Data Visualization

Generate charts, graphs, and table images for data presentation and broadcast.

## Tools Available

- **matplotlib** — General purpose plotting
- **seaborn** — Statistical visualizations
- **PIL (Pillow)** — Image creation/manipulation, table rendering
- **pandas** — Built-in plotting via matplotlib

## Chart Types

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Line chart
plt.plot(dates, values)

# Bar chart
plt.bar(categories, values)

# Stacked bar
df.plot(kind='bar', stacked=True)

# Pie chart
plt.pie(sizes, labels=labels, autopct='%1.1f%%')

# Heatmap
sns.heatmap(correlation_matrix, annot=True)

# Scatter
plt.scatter(x, y, c=colors)
```

## Table Image Generation (for Broadcast)

For formatted table images (used in Feishu broadcast):

```python
from PIL import Image, ImageDraw, ImageFont

# Calculate dimensions
row_height = 40
col_widths = [120, 100, 100, 100, 100, 100]
img_width = sum(col_widths)
img_height = row_height * (len(rows) + 1)  # +1 for header

# Create image
img = Image.new('RGB', (img_width, img_height), 'white')
draw = ImageDraw.Draw(img)

# Draw header with background
draw.rectangle([0, 0, img_width, row_height], fill='#f0f0f0')

# Draw rows with alternating colors
for i, row in enumerate(rows):
    y = row_height * (i + 1)
    bg = '#fafafa' if i % 2 == 0 else 'white'
    draw.rectangle([0, y, img_width, y + row_height], fill=bg)
    # Draw text for each cell...

# Save
img.save('output.png')
```

## Best Practices

- Use Chinese fonts: set `plt.rcParams['font.sans-serif'] = ['SimHei', 'Arial Unicode MS']`
- For table images: no borders, use background color alternation for row distinction
- Save as PNG for sharp text rendering
- Keep tables within reasonable width (<800px) for mobile viewing
- Add emoji indicators (🔥 for high, ⚠️ for low) in text annotations

## Output

- Save to workspace: `charts/figure_name.png`
- Upload to Feishu via `feishu_doc upload_image`
- Or send as attachment in message

---
name: pptx-generator
description: "Create PowerPoint (.pptx) presentations programmatically with slides, charts, tables, and images."
---

# PPTX Generator

Create PowerPoint presentations (.pptx) programmatically.

## Core Library: python-pptx

```python
from pptx import Presentation
from pptx.util import Inches, Pt, Emu
from pptx.enum.text import PP_ALIGN
from pptx.dml.color import RGBColor

# Create
prs = Presentation()

# Title slide
slide = prs.slides.add_slide(prs.slide_layouts[0])
slide.shapes.title.text = "Title"
slide.placeholders[1].text = "Subtitle"

# Content slide
slide = prs.slides.add_slide(prs.slide_layouts[1])
slide.shapes.title.text = "Section Title"

# Add text box
from pptx.util import Inches
txBox = slide.shapes.add_textbox(Inches(1), Inches(2), Inches(8), Inches(4))
tf = txBox.text_frame
tf.text = "First paragraph"
p = tf.add_paragraph()
p.text = "Second paragraph"
p.font.size = Pt(18)

# Add table
rows, cols = 4, 3
table = slide.shapes.add_table(rows, cols, Inches(1), Inches(2), Inches(8), Inches(3)).table
for i in range(rows):
    for j in range(cols):
        table.cell(i, j).text = f"R{i}C{j}"

# Add image
slide.shapes.add_picture('image.png', Inches(1), Inches(1), width=Inches(4))

# Add chart
from pptx.chart.data import CategoryChartData
chart_data = CategoryChartData()
chart_data.categories = ['Q1', 'Q2', 'Q3']
chart_data.add_series('Series 1', (100, 150, 200))
slide.shapes.add_chart(
    XL_CHART_TYPE.COLUMN_CLUSTERED,
    Inches(1), Inches(2), Inches(8), Inches(4),
    chart_data
)

# Save
prs.save('output.pptx')
```

## Slide Layouts

- Layout 0: Title slide
- Layout 1: Title + Content
- Layout 5: Blank (custom layout)

## Best Practices

- Use HTML-to-PPT skill for complex designs (html-ppt skill available)
- For data-heavy slides: create tables or charts
- Images: reference workspace paths or download URLs first
- Chinese text: verify font support
- 16:9 is standard aspect ratio

## HTML-PPT Alternative

For designed presentations, use the `html-ppt` skill:
- Create HTML slides with CSS styling
- Convert to PPTX via skill workflow
- Better visual control than programmatic approach

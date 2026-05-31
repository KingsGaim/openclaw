---
name: docx-generator
description: "Create, read, and edit Word (.docx) documents programmatically."
---

# DOCX Generator

Create and manipulate Word documents (.docx).

## Core Tool: feishu_doc with docx actions

### Create Document
```json
{"action": "create", "title": "Report", "file_type": "docx", "folder_token": "fld_xxx"}
```

### Read/Write
- **read** — Fetch document content
- **write** — Overwrite with Markdown
- **append** — Append Markdown
- **insert** — Insert at position

### Local .docx Files

```python
from docx import Document
from docx.shared import Inches, Pt, RGBColor

# Create
doc = Document()
doc.add_heading('Title', level=1)
doc.add_paragraph('Content')

# Add table
table = doc.add_table(rows=3, cols=3, style='Table Grid')
for i, row in enumerate(data):
    for j, cell_val in enumerate(row):
        table.cell(i, j).text = str(cell_val)

# Add image
doc.add_picture('image.png', width=Inches(4))

# Save
doc.save('output.docx')
```

### Template Fill

```python
from docxtpl import DocxTemplate

tpl = DocxTemplate('template.docx')
context = {'name': 'John', 'items': [{'desc': 'A', 'qty': 2}]}
tpl.render(context)
tpl.save('filled.docx')
```

## Document Structure

- Headings (level 1-6)
- Paragraphs (with bold, italic, underline)
- Lists (ordered/unordered)
- Tables
- Images
- Page breaks
- Hyperlinks

## Best Practices

- Use `feishu_doc` for cloud documents
- Use `python-docx` for local file generation
- For mail merge: use `docxtpl` with .docx template
- Chinese text: ensure proper font settings
- Set page margins before adding content

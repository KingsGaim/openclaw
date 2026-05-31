---
name: pdf-tools
description: "Inspect, split, merge, OCR, redact, or convert PDFs with local CLI tools."
---

# PDF Tools

Operate on PDF files — inspect, merge, split, convert, extract text, and manipulate pages.

## Common Operations

### Inspect
```bash
# Page count
python -c "import fitz; print(fitz.open('file.pdf').page_count)"

# File info
pdfinfo file.pdf
```

### Merge
```bash
# Using pypdf
python -c "
from pypdf import PdfWriter, PdfReader
writer = PdfWriter()
for f in ['a.pdf', 'b.pdf']:
    writer.append(PdfReader(f))
writer.write('merged.pdf')
"
```

### Split
```bash
# Split by page range
python -c "
from pypdf import PdfReader, PdfWriter
reader = PdfReader('input.pdf')
writer = PdfWriter()
for i in range(0, 5):  # pages 1-5
    writer.add_page(reader.pages[i])
writer.write('output.pdf')
"
```

### Extract Text
```bash
# Using pdfplumber
python -c "
import pdfplumber
with pdfplumber.open('file.pdf') as pdf:
    for page in pdf.pages:
        print(page.extract_text())
"
```

### Convert
```bash
# PDF to images
python -c "
import fitz
doc = fitz.open('file.pdf')
for i, page in enumerate(doc):
    pix = page.get_pixmap()
    pix.save(f'page_{i+1}.png')
"
```

## Available CLI Tools

- `pdftk` — PDF manipulation toolkit
- `qpdf` — PDF transformation
- `gs` (Ghostscript) — Convert, compress
- `poppler-utils` — pdfinfo, pdftotext, pdfimages

## Best Practices

- Always verify page count before/after operations
- Use `fitz` (PyMuPDF) for fast operations
- For OCR: use `ocrmypdf` or `tesseract`
- Keep originals, write outputs beside inputs

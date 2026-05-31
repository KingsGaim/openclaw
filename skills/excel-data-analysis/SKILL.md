---
name: excel-data-analysis
description: "Read, parse, analyze Excel/CSV files with Pandas. Handle multiple sheets, skip headers, clean data, compute metrics."
---

# Excel Data Analysis

Read, parse, and analyze Excel (.xlsx) and CSV files using Pandas.

## Core Workflow

1. **Inspect** — List sheets, check structure
2. **Read** — Load data with appropriate parameters
3. **Clean** — Handle headers, empty rows, type conversion
4. **Analyze** — Compute metrics, aggregations, visualizations

## Key Patterns

### List Sheets
```python
import pandas as pd
sheets = pd.ExcelFile(file_path).sheet_names
print(sheets)
```

### Read with Header Skip
```python
# Most ISV files have 2-3 rows of metadata before actual data
df = pd.read_excel(file_path, sheet_name='SheetName', header=2)
df = df.dropna(how='all', axis=1)  # Remove empty columns
```

### Common Operations
```python
# Basic stats
df.describe()
df.info()

# Group by and aggregate
df.groupby('category').agg({'sales': 'sum', 'count': 'size'})

# Pivot table
pd.pivot_table(df, values='metric', index='row', columns='col', aggfunc='sum')

# Filter
df[df['status'] == 'active']

# Sort
df.sort_values('date', ascending=False)
```

## Column Naming

- Excel files often produce `"Unnamed: X"` column names
- Rename meaningful columns: `df.rename(columns={'Unnamed: 0': 'date'}, inplace=True)`

## Data Types

- Check types: `df.dtypes`
- Convert: `df['number'] = pd.to_numeric(df['number'], errors='coerce')`
- Dates: `df['date'] = pd.to_datetime(df['date'])`

## Output

- Save results: `df.to_excel('output.xlsx', index=False)`
- Display: Use markdown tables or lists (avoid markdown tables on Discord/WhatsApp)

## Common Pitfalls

1. **Header rows** — Data often starts at row 3+, use `header=2`
2. **Merged cells** — Produce NaN, fill with: `df.ffill()`
3. **Mixed types** — Coerce with `pd.to_numeric(errors='coerce')`
4. **Hidden rows** — Always check `len(df)` after loading
5. **Encoding** — CSV may need `encoding='gbk'` for Chinese data

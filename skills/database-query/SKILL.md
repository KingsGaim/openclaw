---
name: database-query
description: "Query MySQL databases — connect, execute SQL, fetch results. Supports complex queries, joins, aggregations."
---

# Database Query

Query MySQL databases for data retrieval and analysis.

## Connection

- Database config typically stored in `config/db_config.py`
- Uses PyMySQL or similar connector
- Connection params: host, port, user, password, database

## Core Workflow

1. Connect to database
2. Execute SQL query
3. Fetch results (all rows or paginated)
4. Format output (table, CSV, analysis)

## Common Query Patterns

### Basic Select
```sql
SELECT * FROM table_name WHERE condition LIMIT 100;
```

### Aggregation
```sql
SELECT 
    dimension,
    COUNT(*) as cnt,
    SUM(metric) as total,
    AVG(metric) as avg_val
FROM table_name
GROUP BY dimension
ORDER BY total DESC;
```

### Date Filtering
```sql
SELECT * FROM table_name 
WHERE date >= '2026-01-01' 
  AND date <= '2026-05-31'
  AND time_range = '当天';  -- Critical: always filter by time_range snapshot
```

### Joins
```sql
SELECT a.*, b.plan_total
FROM promotion_data a
LEFT JOIN plan_details b 
  ON a.date = b.date 
  AND a.pin = b.pin
WHERE a.date = '2026-05-31';
```

## Important Rules

1. **Always filter by `time_range`** — Tables have multiple snapshots per day (上午/下午/当天). Without this filter, data gets duplicated.
2. **Use LIMIT** — Prevent fetching millions of rows accidentally
3. **Check date range** — Verify data availability before complex queries
4. **Handle NULLs** — Use COALESCE or IFNULL for missing values

## Python Example
```python
import pymysql
config = load_config()  # from config/db_config.py
conn = pymysql.connect(**config)
with conn.cursor() as cur:
    cur.execute("SELECT * FROM table WHERE date = %s", ('2026-05-31',))
    rows = cur.fetchall()
    columns = [desc[0] for desc in cur.description]
    df = pd.DataFrame(rows, columns=columns)
conn.close()
```

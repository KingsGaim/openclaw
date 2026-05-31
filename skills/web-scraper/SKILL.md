---
name: web-scraper
description: "Scrape web pages, extract structured data, handle pagination, and crawl sites systematically."
---

# Web Scraper

Scrape web pages and extract structured data.

## Tools Available

### web_fetch
- Lightweight page fetch, extracts readable markdown
- No JS rendering, no login required
- Good for articles, docs, static pages

### browser (for dynamic content)
- Full browser automation with JS execution
- Login/cookie support via user profile
- Handle pagination, infinite scroll, dynamic content

## Scraping Patterns

### Static Page
```json
{"action": "fetch", "url": "https://example.com/article", "extractMode": "markdown"}
```

### Dynamic Page (Browser)
```
1. Open page: {"action": "open", "url": "https://..."}
2. Snapshot: {"action": "snapshot"}
3. Scroll down for infinite scroll
4. Re-snapshot after content loads
5. Extract data via evaluate
```

### Pagination
```python
# Browser approach
for page in range(1, 10):
    browser.navigate(f"https://example.com/list?page={page}")
    browser.snapshot()
    # Extract data from snapshot
```

### Data Extraction
```python
# From web_fetch markdown
import re
pattern = r'Price: (\d+\.?\d*)'
prices = re.findall(pattern, content)

# From browser evaluate
{"action": "act", "kind": "evaluate", "request": {"fn": "() => { return document.querySelectorAll('.item').map(el => el.textContent) }"}}
```

## Best Practices

- Respect robots.txt and rate limits
- Add delays between requests
- Handle errors gracefully
- Store extracted data in structured format (JSON/CSV)
- For large crawls, use background exec sessions
- Cache results to avoid re-scraping

## Ethical Guidelines

- Don't scrape personal/private data without permission
- Respect website terms of service
- Don't overload servers (add delays)
- Use data only for the requested purpose

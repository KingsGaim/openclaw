---
name: web-fetch-tools
description: "Fetch URLs and extract readable markdown/text content. Lightweight page access without browser automation."
---

# Web Fetch Tools

Fetch web pages and extract readable content as markdown or plain text.

## Tool: web_fetch

- Lightweight page access — no browser automation, no JS rendering
- Extracts readable content by stripping navigation, ads, etc.
- Fast and efficient for content extraction

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `url` | string | HTTP(S) URL to fetch (required) |
| `extractMode` | string | `"markdown"` (default) or `"text"` |
| `maxChars` | number | Max characters to return (truncates if exceeded) |

## Usage Examples

```json
// Fetch article as markdown
{"action": "fetch", "url": "https://example.com/article"}

// Fetch as plain text
{"action": "fetch", "url": "https://example.com/data", "extractMode": "text"}

// Limit output size
{"action": "fetch", "url": "https://example.com/long-page", "maxChars": 5000}
```

## Limitations

- No JavaScript rendering — dynamic content not loaded
- No login/cookie support — public pages only
- No form interaction — GET requests only
- For interactive pages, use browser-automation instead

## Best Practices

- Use for articles, documentation, API docs, blog posts
- Set `maxChars` for very long pages to save tokens
- Prefer `markdown` mode for structured content
- Use `text` mode for raw data extraction

---
name: feishu-wiki-tools
description: "Manage Feishu (Lark) knowledge base — spaces, nodes, search, create, move, rename wiki pages."
---

# Feishu Wiki Tools

Operate Feishu knowledge base (Wiki) — spaces, nodes, documents, search, and organization.

## Available Actions

- **spaces** — List all knowledge spaces
- **nodes** — List nodes under a space or parent node
- **get** — Get wiki node details
- **search** — Search wiki content by query
- **create** — Create new wiki node (docx/sheet/bitable)
- **move** — Move wiki node to different parent/space
- **rename** — Rename wiki node

## Key Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `space_id` | string | Knowledge space ID |
| `token` | string | Wiki node token (from URL `/wiki/XXX`) |
| `parent_node_token` | string | Parent node (omit for root) |
| `obj_type` | string | `docx` / `sheet` / `bitable` (default: docx) |
| `title` | string | Node title |
| `target_parent_token` | string | Target parent for move |
| `target_space_id` | string | Target space for move |
| `query` | string | Search query |

## URL Format

- Wiki URL: `https://feishu.cn/wiki/{token}`
- Extract token from path after `/wiki/`

## Usage Examples

```json
// List spaces
{"action": "spaces"}

// List nodes in space
{"action": "nodes", "space_id": "space_xxx"}

// Create wiki doc
{"action": "create", "space_id": "space_xxx", "title": "项目文档", "obj_type": "docx"}

// Create under parent
{"action": "create", "space_id": "space_xxx", "parent_node_token": "wiki_xxx", "title": "子文档"}

// Move node
{"action": "move", "node_token": "wiki_xxx", "target_parent_token": "wiki_yyy"}

// Rename
{"action": "rename", "token": "wiki_xxx", "title": "新标题"}

// Search
{"action": "search", "query": "关键词"}
```

## Notes

- Creating wiki nodes creates empty documents — use `feishu-doc-tools` to write content
- Move can change both parent and space simultaneously
- Search returns matching nodes across accessible spaces

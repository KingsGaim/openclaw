---
name: feishu-doc-tools
description: "Create, read, write, update Feishu (Lark) documents. Block-level operations, table insertion, image/file uploads."
---

# Feishu Doc Tools

Operate Feishu cloud documents — create, read, write, append, insert, manage blocks, tables, images, and files.

## Available Actions

- **read** — Fetch document content by `doc_token`
- **write** — Overwrite entire document with Markdown
- **append** — Append Markdown to document end
- **insert** — Insert content at specific position (`after_block_id` or `index`)
- **create** — Create new blank document (optionally in folder via `folder_token`)
- **list_blocks** — List all blocks with IDs for targeted operations
- **get_block** — Get a specific block by ID
- **update_block** — Update a block's content
- **delete_block** — Remove a block
- **create_table** — Create table with specified rows/cols
- **write_table_cells** — Write 2D matrix into table cells
- **create_table_with_values** — Create table pre-filled with values
- **insert_table_row / insert_table_column** — Add rows/cols
- **delete_table_rows / delete_table_columns** — Remove rows/cols
- **merge_table_cells** — Merge cell ranges
- **upload_image** — Upload image to document
- **upload_file** — Upload file attachment
- **color_text** — Apply color to text spans

## Key Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `doc_token` | string | Extract from URL `/docx/XXX` |
| `folder_token` | string | Optional target folder |
| `grant_to_requester` | bool | Grant edit permission to requesting user (default: true) |
| `after_block_id` | string | Insert after this block |
| `index` | number | 0-based insert position among siblings |

## URL Format

- Document URL: `https://feishu.cn/docx/{doc_token}`
- Extract token from path after `/docx/`

## Long Document Pattern

For documents exceeding output limits:
1. Create document first → get `doc_token`
2. Chunk content into logical sections
3. Append each chunk sequentially
4. Never write entire large doc in one call

## Usage Examples

```json
// Create document
{"action": "create", "title": "会议记录", "folder_token": "fld_xxx"}

// Read document
{"action": "read", "doc_token": "doc_xxx"}

// Write content
{"action": "write", "doc_token": "doc_xxx", "content": "# Title\n\nContent"}

// Append
{"action": "append", "doc_token": "doc_xxx", "content": "## New Section"}

// Create table with values
{"action": "create_table_with_values", "doc_token": "doc_xxx", "values": [["Name", "Value"], ["A", "1"], ["B", "2"]]}
```

## Notes

- All content is Markdown-formatted
- Block operations require `block_id` from `list_blocks` first
- Table operations need `table_block_id` from the table block

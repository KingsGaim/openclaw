---
name: feishu-bitable-tools
description: "Create and manage Feishu (Lark) Bitable (multidimensional tables) — apps, tables, fields, records, CRUD operations."
---

# Feishu Bitable Tools

Full CRUD operations on Feishu Bitable (multidimensional tables).

## Core Operations

### App Level
- **feishu_bitable_create_app** — Create new Bitable application (needs `name`, optional `folder_token`)
- **feishu_bitable_get_meta** — Parse Bitable URL to get `app_token`, `table_id`, and table list

### Table Level
- **feishu_bitable_list_fields** — List all fields (columns) with types and properties
- **feishu_bitable_create_field** — Add new field/column to a table

### Record Level
- **feishu_bitable_list_records** — List rows with pagination (page_size 1-500)
- **feishu_bitable_get_record** — Get single record by ID
- **feishu_bitable_create_record** — Create new row
- **feishu_bitable_update_record** — Update existing row

## Field Types

| ID | Type | Value Format |
|----|------|-------------|
| 1 | Text | `"string"` |
| 2 | Number | `123` |
| 3 | SingleSelect | `"Option"` |
| 4 | MultiSelect | `["A", "B"]` |
| 5 | DateTime | timestamp_ms |
| 7 | Checkbox | boolean |
| 11 | User | `[{id: "ou_xxx"}]` |
| 13 | Phone | `"string"` |
| 15 | URL | `{text: "Display", link: "https://..."}` |
| 17 | Attachment | file reference |
| 18 | SingleLink | record reference |
| 19 | Lookup | lookup value |
| 20 | Formula | computed |
| 1001 | CreatedTime | auto |
| 1002 | ModifiedTime | auto |
| 1003 | CreatedUser | auto |
| 1004 | ModifiedUser | auto |
| 1005 | AutoNumber | auto |

## URL Format

- `/base/{app_token}?table={table_id}` or `/wiki/{token}?table={table_id}`
- Always use `feishu_bitable_get_meta` first to extract tokens from URL

## Usage Examples

```json
// Get metadata from URL
{"action": "get_meta", "url": "https://feishu.cn/base/abc123?table=tbl456"}

// List fields
{"action": "list_fields", "app_token": "app_xxx", "table_id": "tbl_xxx"}

// Create field
{"action": "create_field", "app_token": "app_xxx", "table_id": "tbl_xxx", "field_name": "状态", "field_type": 3, "property": {"options": [{"name": "待办"}, {"name": "完成"}]}}

// List records
{"action": "list_records", "app_token": "app_xxx", "table_id": "tbl_xxx", "page_size": 100}

// Create record
{"action": "create_record", "app_token": "app_xxx", "table_id": "tbl_xxx", "fields": {"名称": "任务A", "状态": "待办", "截止日期": 1700000000000}}

// Update record
{"action": "update_record", "app_token": "app_xxx", "table_id": "tbl_xxx", "record_id": "rec_xxx", "fields": {"状态": "完成"}}
```

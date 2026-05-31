---
name: feishu-drive-tools
description: "Manage Feishu (Lark) cloud drive — list files/folders, get info, create folders, move, delete, comments."
---

# Feishu Drive Tools

Operate Feishu cloud storage (Drive) — file/folder management, comments, and permissions.

## Available Actions

- **list** — List files and folders in a directory (use `folder_token` to navigate, omit for root)
- **info** — Get file/folder metadata by `file_token`
- **create_folder** — Create new folder (needs `name`, optional `folder_token` for parent)
- **move** — Move file/folder to different location
- **delete** — Delete file/folder
- **list_comments** — List comments on a file
- **list_comment_replies** — List replies to a comment
- **add_comment** — Add comment to a file (optionally scoped to `block_id` for docx)
- **reply_comment** — Reply to a comment

## Key Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `file_token` | string | File or folder token |
| `folder_token` | string | Folder token (omit for root) |
| `type` | string | `doc` / `docx` / `sheet` / `bitable` / `folder` / `file` / `mindnote` / `shortcut` |
| `comment_id` | string | Comment ID |
| `block_id` | string | Optional docx block ID for scoped comment |
| `content` | string | Comment text |

## Usage Examples

```json
// List root directory
{"action": "list"}

// List specific folder
{"action": "list", "folder_token": "fld_xxx"}

// Get file info
{"action": "info", "file_token": "file_xxx"}

// Create folder
{"action": "create_folder", "name": "项目资料", "folder_token": "fld_xxx"}

// Move file
{"action": "move", "file_token": "file_xxx"}

// Add comment
{"action": "add_comment", "file_token": "file_xxx", "content": "请审核"}

// Comment on specific block
{"action": "add_comment", "file_token": "file_xxx", "block_id": "block_xxx", "content": "这里需要修改"}
```

## Notes

- Pagination available via `page_token` and `page_size` (max 100)
- File tokens can be extracted from Feishu file URLs
- Comments support both full-document and block-level scoping

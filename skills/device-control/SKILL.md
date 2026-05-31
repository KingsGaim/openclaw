---
name: device-control
description: "Control paired nodes — camera snap/clip, screen record, location, notifications, device status and health."
---

# Device Control

Operate paired devices/nodes for camera, screen, location, and notification management.

## Actions

| Action | Description |
|--------|-------------|
| `status` | List all paired nodes and their status |
| `describe` | Get detailed node info |
| `camera_snap` | Take a photo (front/back/both) |
| `camera_list` | List available cameras |
| `camera_clip` | Record a short video clip |
| `screen_record` | Record screen |
| `location_get` | Get device location |
| `notifications_list` | List device notifications |
| `notifications_action` | Open/dismiss/reply to notification |
| `device_status` | Get device status |
| `device_info` | Get device info |
| `device_health` | Get battery health info |
| `notify` | Send notification to device |
| `invoke` | Invoke custom command on device |

## Camera

```json
// Take photo
{"action": "camera_snap", "node": "node_name", "facing": "back"}

// Record clip
{"action": "camera_clip", "node": "node_name", "facing": "back", "duration": "10s"}
```

Parameters:
- `facing`: `"front"` / `"back"` / `"both"` (snap only)
- `duration`: Video duration string (clip only)
- `quality`: 1-100 image quality
- `maxWidth`: Max image width

## Location

```json
{"action": "location_get", "node": "node_name", "desiredAccuracy": "balanced"}
```
- `desiredAccuracy`: `"coarse"` / `"balanced"` / `"precise"`
- `locationTimeoutMs`: Timeout in ms

## Notifications

```json
// List
{"action": "notifications_list", "node": "node_name", "limit": 10}

// Dismiss
{"action": "notifications_action", "node": "node_name", "notificationAction": "dismiss", "notificationKey": "key"}

// Reply
{"action": "notifications_action", "node": "node_name", "notificationAction": "reply", "notificationReplyText": "OK"}
```

## Notifications (Send to Device)

```json
{"action": "notify", "node": "node_name", "title": "Alert", "body": "Something happened"}
```
- `priority`: `"passive"` / `"active"` / `"timeSensitive"`
- `delivery`: `"system"` / `"overlay"` / `"auto"`

## File Operations

Use `file_fetch` for retrieving files from nodes.

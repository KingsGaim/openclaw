---
name: cron-scheduler
description: "Manage scheduled tasks — create, list, update, remove cron jobs for reminders, recurring work, and automated broadcasts."
---

# Cron Scheduler

Manage Gateway cron jobs and wake events for scheduling reminders, recurring tasks, and automated work.

## Actions

- **status** — Check scheduler status
- **list** — List all jobs (filter by `agentId`, `includeDisabled`)
- **get** — Get specific job by `jobId`
- **add** — Create new job
- **update** — Patch existing job
- **remove** — Delete job
- **run** — Trigger job now
- **runs** — View run history
- **wake** — Send wake event immediately or at next heartbeat

## Schedule Types

### "at" — One-shot absolute time
```json
{"kind": "at", "at": "2026-06-01T09:00:00+08:00"}
```
ISO timestamps without timezone are UTC.

### "every" — Recurring interval
```json
{"kind": "every", "everyMs": 3600000}
```

### "cron" — Cron expression in timezone
```json
{"kind": "cron", "expr": "0 18 * * *", "tz": "Asia/Shanghai"}
```
Express in local wall-clock time, NOT UTC.

## Job Schema

```json
{
  "name": "string",
  "schedule": { "kind": "...", ... },
  "payload": { "kind": "systemEvent"|"agentTurn", "text"|"message": "..." },
  "sessionTarget": "main"|"isolated"|"current"|"session:<id>",
  "enabled": true,
  "delivery": { "mode": "none"|"announce"|"webhook" }
}
```

## Critical Constraints

- `sessionTarget="main"` REQUIRES `payload.kind="systemEvent"`
- `sessionTarget="isolated"/"current"` REQUIRES `payload.kind="agentTurn"`
- Default: prefer isolated agentTurn jobs unless user explicitly wants current-session

## Payload Types

### systemEvent
```json
{"kind": "systemEvent", "text": "Reminder message"}
```
Injects text as system event into main session.

### agentTurn
```json
{"kind": "agentTurn", "message": "Do this task...", "model": "optional", "timeoutSeconds": 300}
```
Runs agent with prompt in isolated session.

## Examples

```json
// Daily reminder at 9 AM Shanghai
{
  "name": "Morning standup",
  "schedule": {"kind": "cron", "expr": "0 9 * * *", "tz": "Asia/Shanghai"},
  "payload": {"kind": "agentTurn", "message": "Run standup report"},
  "sessionTarget": "isolated"
}

// One-shot reminder in 20 minutes
{
  "name": "Meeting reminder",
  "schedule": {"kind": "at", "at": "2026-05-31T12:10:00+08:00"},
  "payload": {"kind": "systemEvent", "text": "Reminder: Meeting in 10 minutes"},
  "sessionTarget": "main"
}

// Every 2 hours broadcast
{
  "name": "Data broadcast",
  "schedule": {"kind": "cron", "expr": "0 10,12,14,16,18,20,22 * * *", "tz": "Asia/Shanghai"},
  "payload": {"kind": "agentTurn", "message": "Run daily broadcast script"},
  "sessionTarget": "isolated"
}
```

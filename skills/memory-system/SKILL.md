---
name: memory-system
description: "Manage long-term memory — read/write MEMORY.md, daily logs, semantic search, memory maintenance."
---

# Memory System

Persistent memory management for session continuity and long-term knowledge.

## Memory Files

### MEMORY.md
- Long-term curated memory at workspace root
- **ONLY load in main session** (security: no leaking to strangers)
- Contains distilled insights, preferences, lessons learned
- Updated periodically from daily logs

### Daily Logs
- `memory/YYYY-MM-DD.md` — Raw logs of what happened each day
- Created in `memory/` directory
- Raw notes, decisions, context that matters

### Session Transcripts
- Indexed for semantic search
- Accessible via memory_search with `corpus=sessions`

## Tools

### memory_search
```json
{"query": "What did we decide about...", "maxResults": 5, "corpus": "memory|wiki|all|sessions"}
```
- Mandatory recall step before answering questions about prior work
- Semantic search across memory files

### memory_get
```json
{"path": "MEMORY.md", "from": 1, "lines": 50}
```
- Exact excerpt read from specific file
- `corpus=wiki` reads from registered wiki supplements

## Memory Management Workflow

### Write (During Session)
1. Note decisions in `memory/YYYY-MM-DD.md`
2. Update MEMORY.md for long-term significance
3. Update relevant config files for structural changes

### Maintain (During Heartbeats, every few days)
1. Read through recent daily files
2. Identify significant events/lessons worth keeping
3. Update MEMORY.md with distilled learnings
4. Remove outdated info from MEMORY.md

## Best Practices

- "Mental notes" don't survive restarts — WRITE TO FILE
- "Remember this" → update daily log or MEMORY.md
- Made a mistake → document it so future-you doesn't repeat
- MEMORY.md is curated wisdom, not raw logs
- Daily files are raw notes

## Security

- MEMORY.md only loaded in main session
- Don't load in shared contexts (Discord, group chats)
- Contains personal context that shouldn't leak to strangers

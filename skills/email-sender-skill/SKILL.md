---
name: email-sender-skill
description: "Send, read, and manage emails via SMTP/IMAP or email provider APIs."
---

# Email Sender

Send, read, and manage emails.

## Core Skill

Location: `~/.openclaw/skills/email-sender/SKILL.md`

## Capabilities

- **Send emails** — Compose and send via SMTP
- **Read emails** — Fetch inbox via IMAP
- **Search** — Filter by sender, subject, date, keywords
- **Attachments** — Attach files to outgoing emails

## Email Composition

```
To: recipient@example.com
Subject: 会议通知
Body: Markdown or HTML format
Attachments: file paths
```

## Best Practices

- Always confirm recipients before sending
- Draft first, ask for review before sending externally
- Use clear subject lines
- HTML emails for formatted content
- Plain text fallback

## Safety

- External email = "ask first" per AGENTS.md
- Never send half-baked replies
- Verify recipient email addresses
- Don't exfiltrate private data via email

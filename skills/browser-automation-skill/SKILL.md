---
name: browser-automation-skill
description: "Automate web browsers — navigate pages, fill forms, click buttons, take screenshots, extract data, test web apps."
---

# Browser Automation

Control web browsers for navigation, interaction, screenshot, and data extraction.

## Browser Tool Actions

| Action | Description |
|--------|-------------|
| `status` | Check browser status |
| `start` | Start browser session |
| `stop` | Stop browser session |
| `profiles` | List available browser profiles |
| `tabs` | List/open/close tabs |
| `open` | Navigate to URL |
| `snapshot` | Get page accessibility tree with refs |
| `screenshot` | Capture page as image |
| `act` | Perform actions (click, type, press, hover, drag, select, fill) |
| `navigate` | Navigate to new URL |
| `console` | Get browser console logs |
| `evaluate` | Execute JavaScript |
| `focus` | Focus a tab |
| `close` | Close a tab |

## Core Workflow

1. **Open** page: `{"action": "open", "url": "https://..."}`
2. **Snapshot**: `{"action": "snapshot", "targetId": "t1"}` — get refs like `e12`
3. **Act**: Use refs to interact: `{"action": "act", "kind": "click", "ref": "e12"}`
4. **Re-snapshot**: Get fresh refs after page changes
5. **Screenshot**: `{"action": "screenshot", "targetId": "t1"}` — capture visual state

## Action Types (kind)

- **click** — Click element by ref
- **type** — Type text (use `text` parameter)
- **press** — Press key (use `key` parameter: Enter, Tab, Escape)
- **hover** — Hover over element
- **fill** — Fill form field (replaces existing content)
- **select** — Select dropdown option
- **drag** — Drag from startRef to endRef
- **evaluate** — Run JavaScript (use `request.fn`)

## Profiles

- **openclaw** (default) — Isolated managed browser, no cookies
- **user** — User's logged-in browser, existing sessions/cookies

## Tips

- Use `refs="aria"` for stable Playwright aria-ref IDs across calls
- Default `refs="role"` uses role+name-based refs
- For multi-step flows, keep same `targetId` from snapshot
- Avoid `act:wait` unless no reliable UI state exists
- Stale refs? Take new snapshot

## Browser Automation Skill

For complex flows (login checks, Google Meet, multi-step), use the bundled `browser-automation` skill at:
`~/.openclaw/plugin-skills/browser-automation/SKILL.md`

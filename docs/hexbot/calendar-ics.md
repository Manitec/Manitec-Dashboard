# HexBot — Calendar ICS

> **Status:** Live on `main`  
> **Source:** [`lib/calendar-ics.ts`](https://github.com/Manitec/hexbot/blob/main/lib/calendar-ics.ts)  
> **Related issue:** [hexbot #3](https://github.com/Manitec/hexbot/issues/3)

HexBot can detect reminder/note output from its own replies and offer the user a one-click `.ics` calendar file download, compatible with Google Calendar, Apple Calendar, and Outlook.

---

## Pipeline Overview

```
User sends message
       │
       ▼
detectTaskIntent(userText)     ← fires before API call
       │
       ▼
Hex API streams reply
       │
       ▼
detectCalendarIntent(reply)    ← fires after stream completes
       │
       ▼
ActionPanel merges task + calendar data
       │
       ▼
User clicks "download .ics" → hexReminderToCalendar() → browser download
```

---

## Functions

### `detectCalendarIntent(assistantText)`

Scans the assistant reply for reminder/note creation patterns. Returns a `CalendarIntent` object or `null`.

```ts
import { detectCalendarIntent } from "@/lib/calendar-ics";

const intent = detectCalendarIntent(hexReply);
if (intent) {
  // offer .ics download
}
```

**Trigger patterns matched:**

| Pattern | Example |
|---|---|
| `Reminder set: ...` | Structured output header |
| `Reminder Details:` | Structured block header |
| `Note created: ...` | Legacy note format |
| `Note to Self: ...` | Format C header |
| `Reminder: <text>` at line start | Hex's most common inline format |
| `Note: <text>` at line start | Inline note format |
| `reminder` + time signal in same message | Catch-all for date-bearing reminders |

---

### `parseHexReminder(raw)`

Extracts structured fields from raw HexBot reminder text. Handles three output formats.

#### Format A — Structured block
```
Reminder Details:
Date: 3 days from now
Priority: Medium
Description: Review codebase for bottlenecks.
Notification: You'll receive a notification 1 day before the reminder is due.
```

#### Format B — Inline
```
Reminder: Review HexBot's architecture in the next 6-8 weeks to assess restructuring needs.
```

#### Format C — Note to Self
```
Note to Self: Hex Restructure
Reminder: As Hex continues to evolve...
Priority: Medium-High
Deadline: Review and assessment within 6-8 weeks.
```

**Extracted fields:**

| Field | Source | Default |
|---|---|---|
| `summary` | Title line (Note to Self > Reminder set > inline Reminder) | First non-label line |
| `daysOffset` | `N days from now`, `N weeks from now`, `in the next N weeks`, range midpoint | `3` |
| `priority` | `Priority: <value>` — supports `Medium-High` | `Medium` |
| `description` | `Description:` block, then `Next Steps:`, then `Deadline:` | `""` |
| `alarmMinutes` | `Notification: N days/hours/minutes before` | `1440` (1 day) |

**Date range handling:**  
`6-8 weeks` → midpoint → 7 weeks → 49 days. Same logic for day ranges.

---

### `buildIcs(config)`

Builds a standards-conformant iCalendar string (RFC 5545).

```ts
const ics = buildIcs({
  summary: "Review HexBot architecture",
  description: "Identify bottlenecks, consider restructure.",
  start: new Date("2026-05-01T13:00:00"),
  end:   new Date("2026-05-01T14:00:00"),
  alarmMinutes: 1440,
});
```

Produces: `VCALENDAR > VEVENT` with optional `VALARM` block. UIDs are generated via `crypto.randomUUID()` in the format `hexbot-<uuid>@manitec.local`.

---

### `downloadIcs(filename, content)`

Triggers a browser blob download. **Browser-only** — do not call server-side.

```ts
downloadIcs("review-hexbot-architecture.ics", icsString);
```

---

### `hexReminderToCalendar(rawAssistantText, autoDownload?)`

Full one-call pipeline: parse → build → download.

```ts
const { ics, filename, parsed } = hexReminderToCalendar(hexReply);
// autoDownload defaults to true — triggers browser download immediately

// To get the ICS string without downloading:
const { ics } = hexReminderToCalendar(hexReply, false);
```

---

### `isCalendarRequest(userText)`

Detects whether the user's own message is explicitly requesting a calendar action.

```ts
isCalendarRequest("add the note as a reminder"); // true
isCalendarRequest("what's the weather");          // false
```

---

## Confidence Levels

| Level | Meaning |
|---|---|
| `high` | Explicit `N days/weeks from now` or `tomorrow` found |
| `medium` | Date range found, or `in the next N weeks` phrasing |
| `low` | No date signal detected; defaults used |

---

## Known Limitations / Future Work

- **Google Calendar direct insert** — OAuth flow not yet implemented; currently `.ics` download only
- **Note/reminder persistence** — reminders are not stored to Firebase; session clear loses them
- **Session persistence** — identified in the HexBot architecture review note as a priority gap

---

## Related Docs

- [Action Panel](action-panel.md) — how calendar data surfaces in the UI
- [HexBot project overview](../projects/hexbot.md)

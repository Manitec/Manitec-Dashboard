# HexBot — Unified Action Panel

> **Status:** Live on `main`  
> **Source:** [`app/hex/page.tsx`](https://github.com/Manitec/hexbot/blob/main/app/hex/page.tsx)  
> **Related issue:** [hexbot #3](https://github.com/Manitec/hexbot/issues/3)

The action panel is a unified banner that appears below the input bar after HexBot detects a task or reminder in the conversation. It surfaces both a task creation action and a calendar download action in a single dismissible block.

---

## Architecture

### `ActionPanel` type

```ts
type ActionPanel = {
  task: TaskIntent;          // always present
  calendarData: CalendarIntent | null;  // added after stream completes
};
```

A single `actionPanel` state replaces the two separate states that existed previously (`pendingTaskIntent` + `pendingCalendarIntent`).

---

## Progressive Reveal

The panel fills in progressively so it never feels like it jumps:

```
1. User hits send
       │
       ▼
   detectTaskIntent(userText) fires
   → if match: panel opens with task row only
       │
       ▼
   Hex streams reply...
       │
       ▼
   Stream completes
       │
       ▼
   detectCalendarIntent(reply) fires
   → if match: calendarData merged into existing panel
   → calendar row appears in place (no new banner)
```

**Task row** — appears immediately on user send, before the API call returns.  
**Calendar row** — appears after the stream completes, only if Hex's reply contains a reminder/note.

---

## Calendar-Only Panel

If no task intent is detected from the user's input but the assistant reply looks like a reminder, a panel still opens — a minimal `TaskIntent` shell is synthesised to keep the structure consistent, and only the calendar row is rendered.

```ts
// Calendar-only: no task row visible, calendar row shown
{
  task: { title: calData.summary, priority: "normal", ... },
  calendarData: calData
}
```

---

## Panel Layout

```
┌─ action panel ─────────────────────────────────────────┐
│  task  [review architecture]  [hexbot]     ○ create task │
│  ──────────────────────────────────────────────────────  │
│  📅 cal  [49d]  [⏰ 1d before]          ○ download .ics  │
│  ──────────────────────────────────────────────────────  │
│                                              dismiss     │
└────────────────────────────────────────────────────────┘
```

- **Task row** — green accent, shows title + project tag + priority tag
- **Calendar row** — purple accent, shows days offset + alarm timing
- **Dismiss** — single button clears the entire panel

---

## Partial Completion Behavior

If the user creates the task but hasn't downloaded the calendar event yet:

- The task row is cleared from the panel
- The calendar row remains visible until dismissed or downloaded
- A single dismiss at any point clears everything

---

## Related Docs

- [Calendar ICS engine](calendar-ics.md) — parsing and ICS generation
- [HexBot project overview](../projects/hexbot.md)

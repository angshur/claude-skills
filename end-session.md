# /end-session — Session Close + Cockpit Update

Wrap up a session cleanly. Summarize what changed, update the cockpit, log to the weekly record. Run this before closing any session where something moved.

---

## How to invoke

- **Standard** — `end-session` — full close: recap + cockpit update + weekly log entry
- **Quick** — `end-session quick` — cockpit update only, no log entry
- **Log only** — `end-session log` — append to weekly log without touching cockpit

---

## What it does (in order)

### Step 1 — Session recap (from conversation context)

Scan the conversation and produce a structured summary:

```
SESSION RECAP — [DATE] [TIME BLOCK if known]

VEHICLES TOUCHED
- [Vehicle]: [what changed — decision made, task done, status shifted, blocker cleared]

PIPELINES TOUCHED
- [Pipeline]: [what moved]

NEW ITEMS CAPTURED
- Inbox: [any new ideas added]
- Files created/updated: [list]
- Decisions logged: [any decisions.md entries needed]

WHAT DIDN'T HAPPEN (planned but not done)
- [anything discussed but not acted on]
```

### Step 2 — Update cockpit.md

Read `~/Documents/Vercel/life-context/cockpit.md`.

For every vehicle, pipeline, capability, or foundation item that changed status or next action during the session — rewrite that row. Apply the status system:

| Indicator | Meaning |
|---|---|
| 🔴 | Broken — blocked, stalled, not moving when it should be |
| 🟠 | Deadline — time-sensitive, action needed this week |
| 🟡 | In progress — moving, no immediate crisis |
| 🟢 | Healthy — on track |
| ⚪ | Parked — intentionally inactive |

Update the `*Last updated*` date at the top.

Only rewrite rows that actually changed. Don't touch rows that weren't discussed.

### Step 3 — Update NOW.md (only if material change)

Read `~/Documents/Vercel/NOW.md`.

Update only if:
- A hard deadline was added or completed
- A top priority per vehicle shifted
- A blocker was cleared or added
- A relationship follow-up was completed or added

Don't touch NOW.md for minor session notes — it's a weekly file, not a session log.

### Step 4 — Append to weekly log

Read `~/Documents/Vercel/content/weekly-log.md`.

Append a session entry:

```markdown
## [DATE] — [Time block if known, e.g. "Saturday Leverage" or "ad hoc"]

**Vehicles touched:** [comma-separated list]
**Key outcomes:**
- [bullet: what was decided, built, sent, or moved]
- [bullet]
**New captures:** [inbox ideas, files, decisions]
**Left open:** [what was discussed but not completed — pick up next session]
```

---

## Rules

- **Don't fabricate.** Only log what actually happened in this conversation. If something wasn't touched, don't update its cockpit row.
- **Be specific.** "Decided to archive Clearpath" is better than "discussed foundation."
- **Keep it short.** The recap is for future-you to pick up cold, not a full transcript.
- **Flag blockers clearly.** If something is now 🔴, say why in one clause.
- **End with one sentence:** "Next session: start with ___." The single most important thing to pick up.

---

## Output format

After running, print:

```
✓ Cockpit updated — [N] rows changed
✓ Weekly log entry appended
✓ NOW.md [updated / not changed]

Next session: [one sentence on what to start with]
```

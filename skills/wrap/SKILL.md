---
name: wrap
description: Use at the end of every VS Code session to commit and push all work, write an Obsidian session note, and set up tomorrow's starting point.
---

# Session Wrap

Run this when the day's work is done. Three steps, all automatic — no questions asked.

---

## Step 1 — Save Everything to GitHub

```
git add -A
git commit -m "[brief description of what was done] — [date]"
git push
```

If there is nothing to commit, note it and move on.

---

## Step 2 — Write Obsidian Session Note

Create `_sessions/YYYY-MM-DD.md` in the vault:

```
# Session — [Date]

## What we worked on
[2–4 plain-English sentences — what was done, not how]

## Decisions made
[Any choices, directions, or conclusions agreed during the session]

## What's next
[Top 1–2 things to pick up next time, from today's Should Do or Check Later]
```

If the vault path is unknown, check:
1. `C:\Users\jomit\OneDrive\Documents\vault`
2. `C:\Users\jomit\Documents\vault`
3. `C:\Users\jomit\vault`

---

## Step 3 — Tomorrow's Starting Point

Ask one question:
> **"Anything you want to make sure is first on the list tomorrow?"**

If the user answers, add it as a note at the bottom of today's session file:
```
## First thing tomorrow
[what they said]
```

If they say nothing or "no", skip it.

---

## Confirm

```
════════════════════════════════════════
  SESSION WRAPPED — [Date]
════════════════════════════════════════
  ✅  Committed and pushed to GitHub
  ✅  Session note written to Obsidian
  ✅  Tomorrow's starting point noted
════════════════════════════════════════
  See you next time.
════════════════════════════════════════
```

---
name: wrap
description: Use at the end of every VS Code session to commit and push all work and set up tomorrow's starting point.
---

# Session Wrap

Run this when the day's work is done. Two steps, all automatic — no questions asked.

---

## Step 1 — Save Everything to GitHub

```
git add -A
git commit -m "[brief description of what was done] — [date]"
git push
```

If there is nothing to commit, note it and move on.

---

## Step 2 — Tomorrow's Starting Point

Ask one question:
> **"Anything you want to make sure is first on the list tomorrow?"**

If the user answers, respond with a clear note of it so they can see it next session.

If they say nothing or "no", skip it.

---

## Confirm

```
════════════════════════════════════════
  SESSION WRAPPED — [Date]
════════════════════════════════════════
  ✅  Committed and pushed to GitHub
  ✅  Tomorrow's starting point noted
════════════════════════════════════════
  See you next time.
════════════════════════════════════════
```

---
name: week
description: Use at the start of the week to plan it, or at the end of the week to retro it. Auto-detects which mode based on the day.
---

# Weekly Planning & Retro

Check today's day of the week and run the correct mode automatically. If run mid-week, ask: **"Are we planning the week or reviewing it?"**

---

## PLAN Mode (Monday or start of week)

### 1 — Gather context silently
- Run `git log --oneline --since="7 days ago"` to see what shipped last week
- Check Calendar for key meetings this week (if connected)
- Check Jira for sprint goals (if connected)

### 2 — Ask
> **"What are the 3 most important things to get done this week?"**

### 3 — Build the weekly plan

| Bucket | What goes in it |
|--------|----------------|
| 🎯 This Week's Goals | The 3 things the user named |
| 📋 Also Planned | Sprint tasks, calendar commitments, carry-overs from last week |
| 🔁 On the Radar | Things to watch but not act on this week |

### 4 — Commit and push automatically
```
git add -A
git commit -m "Week [XX] plan — [date]"
git push
```

Print:
```
════════════════════════════════
  WEEK [XX] PLAN — [Date range]
════════════════════════════════
  🎯 Goals
  • [goal 1]
  • [goal 2]
  • [goal 3]

  📋 Also planned: [N] items
  🔁 On the radar: [N] items
════════════════════════════════
  Saved to GitHub.
════════════════════════════════
```

---

## RETRO Mode (Friday or end of week)

### 1 — Gather context silently
- Run `git log --oneline --since="7 days ago"` to see what was actually shipped
- Check Calendar for what meetings happened this week (if connected)

### 2 — Ask three questions (one at a time)
1. *"What went well this week?"*
2. *"What didn't go as planned?"*
3. *"What will you do differently next week?"*

### 3 — Commit and push automatically
```
git add -A
git commit -m "Week [XX] retro — [date]"
git push
```

Print:
```
════════════════════════════════
  WEEK [XX] RETRO — [Date]
════════════════════════════════
  Goals completed: [N/N]
  Carry-overs noted for next week.
════════════════════════════════
  Have a good weekend.
════════════════════════════════
```

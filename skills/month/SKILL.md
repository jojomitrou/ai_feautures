---
name: month
description: Use at the start of the month to plan it, or at the end of the month to retro it. Auto-detects which mode based on the date.
---

# Monthly Planning & Retro

Check today's date and run the correct mode automatically:
- **Days 1–3 of the month:** PLAN mode
- **Days 28–31 of the month:** RETRO mode
- **Mid-month:** ask — *"Are we planning the month or reviewing it?"*

---

## PLAN Mode (start of month)

### 1 — Gather context silently
- Run `git log --oneline --since="30 days ago"` to see what shipped last month
- Check Jira for any monthly milestones or quarterly goals (if connected)
- Check Calendar for key dates this month (if connected)

### 2 — Ask
> **"What are the 3 most important outcomes you want from this month?"**

Then: *"Any deadlines or key dates this month I should know about?"*

### 3 — Build the monthly plan

| Bucket | What goes in it |
|--------|----------------|
| 🎯 Month Goals | The 3 outcomes the user named |
| 📅 Key Dates | Deadlines, launches, important meetings |
| 📋 Projects in Flight | Ongoing work that needs to move forward this month |
| 🔁 Carry-overs | Anything unfinished from last month |

### 4 — Commit and push automatically
```
git add -A
git commit -m "[Month] [Year] plan — [date]"
git push
```

Print:
```
════════════════════════════════════
  [MONTH] [YEAR] PLAN
════════════════════════════════════
  🎯 Goals
  • [goal 1]
  • [goal 2]
  • [goal 3]

  📅 Key dates: [N]
  📋 Projects in flight: [N]
  🔁 Carry-overs: [N]
════════════════════════════════════
  Saved to GitHub.
════════════════════════════════════
```

---

## RETRO Mode (end of month)

### 1 — Gather context silently
- Run `git log --oneline --since="30 days ago"` for a full picture of what shipped
- Check Jira for completed tickets this month (if connected)

### 2 — Ask four questions (one at a time)
1. *"What were the biggest wins this month?"*
2. *"What didn't happen that you expected to?"*
3. *"What took more time or energy than expected?"*
4. *"What's the one thing you'd do differently next month?"*

### 3 — Commit and push automatically
```
git add -A
git commit -m "[Month] [Year] retro — [date]"
git push
```

Print:
```
════════════════════════════════════
  [MONTH] [YEAR] RETRO
════════════════════════════════════
  Goals achieved: [N/N]
  Retro saved.
  Carry-overs noted for [next month].
════════════════════════════════════
  Good month. On to [next month].
════════════════════════════════════
```

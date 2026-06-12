---
name: prep
description: Use at the start of every VS Code session to run the daily workflow kickoff — verifies critical connections, ensures all work is saved to GitHub, gathers context, and organises the day into Must Do, Should Do, and Check Later.
---

# Daily Session Prep

Run this at the start of every session.

The golden rule of every session: **everything the user works on must end up saved in a GitHub repository**. Notes, plans, code, decisions — all of it. GitHub is the safety net. Nothing should live only on the laptop.

---

## Phase 1 — Foundation Check

### 1a — GitHub (blocking)

Run:
```
gh auth status
```

**If pass:** great, move on.

**If fail:** say —
> *"You're not logged into GitHub yet. Type `gh auth login` in the terminal and follow the steps — I'll walk you through it if you need."*

Do not proceed until GitHub is connected.

---

### 1b — GitHub Repo for Today's Work (blocking)

Check whether the current folder is a git repository:
```
git status
```

**If pass (inside a repo):**
- If there are uncommitted changes, commit and push immediately — no need to ask:
  ```
  git add -A
  git commit -m "Session save — [date]"
  git push
  ```
  Note it in the briefing: *"Saved [N] uncommitted files from last session."*

**If fail (not a repo):**
Say —
> *"This folder isn't connected to GitHub yet. Let's set that up now — what would you like to call this project?"*

Then:
1. `git init`
2. `gh repo create [name] --private --source=. --push`

Do not proceed until there is a GitHub repo for the current work.

---

### 1c — Service Checks (non-blocking)

Run all of these quietly and note status — do not block on any of them:

| Service | Check | If failing |
|---------|-------|------------|
| BigQuery | `gcloud auth list` | ⚠️ flag if data work needed today |
| Gmail | `list_labels` via MCP | ⚠️ non-blocking |
| Google Calendar | `list_events` via MCP for today | ⚠️ non-blocking |
| Jira | Atlassian MCP call | ⚠️ flag if ticket work needed today |

---

### 1d — Company Skills Sync (silent, invisible)

Every session, silently check whether the company skills repo (`https://github.com/jojomitrou/ai_feautures`) has been updated. Never show anything if there are no changes.

1. Read the stored commit hash from `$env:USERPROFILE\.claude\.skills-hash` — if the file doesn't exist, treat this as a first run
2. Run: `git ls-remote https://github.com/jojomitrou/ai_feautures HEAD` to get the latest remote hash (fast, no clone needed)
3. Compare:
   - **Same hash:** do nothing, show nothing, move on
   - **Different hash (or first run):**
     a. Clone to temp: `git clone https://github.com/jojomitrou/ai_feautures "$env:TEMP\qm-skills-update"`
     b. Get changed skill files: `git -C "$env:TEMP\qm-skills-update" log --oneline --name-only [old-hash]..HEAD -- skills/`
     c. Copy skills: `Copy-Item -Recurse "$env:TEMP\qm-skills-update\skills\*" "$env:USERPROFILE\.claude\skills\" -Force`
     d. Clean up: `Remove-Item -Recurse -Force "$env:TEMP\qm-skills-update"`
     e. Write new hash to `$env:USERPROFILE\.claude\.skills-hash`
     f. Extract updated skill names from changed paths (e.g. `skills/prep/SKILL.md` → `/prep`)
     g. For each updated skill, read its frontmatter `description` and summarise in one sentence — include in the briefing box

---

## Phase 2 — Last Session Summary (automatic)

Silently gather last session context from git — no question needed, always shown in the briefing:
- `git log --oneline -5` for the last 5 commits
- Summarise in 2–3 plain-English lines — what was worked on, nothing technical

---

## Phase 3 — Context Gathering (silent)

Gather this before asking the user anything. Do not narrate each step.

1. **GitHub** — open PRs (`gh pr list`), open issues (`gh issue list`)
2. **Calendar** (if connected) — today's meetings
3. **Jira** (if connected) — in-progress or blocked sprint tickets

---

## Phase 4 — Plan the Day

**Day-of-week awareness:**
- **Monday:** ask *"Any goals for the week?"* and add a **🗓 This Week** bucket above Must Do
- **Friday:** after the daily structure, ask *"It's Friday — want a quick review of the week?"* — if yes, summarise the last 5 days of git commits in plain English
- **Other days:** standard flow

Ask one question:

> **"What's the main thing you want to get done today?"**

Then combine with everything from Phase 3 and organise into three buckets:

### ✅ Must Do
- The user's stated main goal
- Blocking GitHub items (failing CI, PRs waiting on them)
- Today's meetings
- Blocked Jira tickets

### 📋 Should Do
- Open GitHub issues or non-blocking PRs
- Non-urgent sprint tasks
- Secondary goals the user mentioned

### 🔁 Check Later
- GitHub notifications not assigned to the user
- Anything the user wants to revisit later

---

## Phase 5 — End-of-Session Save

When the user says they're done, commit and push automatically — no confirmation needed:
```
git add -A
git commit -m "[brief description of what was done] — [date]"
git push
```

Then confirm:
> *"All saved to GitHub — [date]."*

Only pause if:
- The user says "don't push yet"
- There is a merge conflict
- The branch has protection rules blocking a direct push

---

## Daily Briefing Report

Gather everything silently first, then print one single box.

```
════════════════════════════════════════
  DAILY PREP — Quantum Media
  [Day, Date]
════════════════════════════════════════
  GitHub      ✅  @[username]
  BigQuery    ✅ / ⚠️
  Gmail       ✅ / ⚠️
  Calendar    ✅ / ⚠️
  Jira        ✅ / ⚠️

  📅 MEETINGS TODAY
  [HH:MM]  [meeting title — attendees if known]
  [HH:MM]  [meeting title]

────────────────────────────────────────
  🕐 LAST SESSION — [date of last commit]
  [2–3 plain-English lines from git log]

────────────────────────────────────────
  📢 STANDUP
  ✅ Yesterday
     • [plain-English summary of yesterday's commits]
  🔨 Today
     • [Must Do item 1]
     • [Must Do item 2]
  ⚠️ Blockers
     • [anything blocked — or "None"]

────────────────────────────────────────  ← only show if skills were updated
  🆕 SKILLS UPDATED
  • /[skill-name] — [one sentence: what it does]

────────────────────────────────────────
  ✅ MUST DO
  • [task 1]
  • [task 2]

  📋 SHOULD DO
  • [task 1]
  • [task 2]

  🔁 CHECK LATER
  • [item 1]
  • [item 2]
════════════════════════════════════════
```

After printing, ask only: **"Anything to add or move between buckets?"** — adjust, then begin the first Must Do item.

---
name: prep
description: Use at the start of every VS Code session to verify GitHub, BigQuery, Obsidian, Gmail, Google Calendar, and Jira are connected and ready before starting any work.
---

# Session Prep

Run this at the start of every session. Check all six connections and report status before doing anything else.

---

## Step 1 — GitHub

Run:
```
gh auth status
```
- **Pass:** output includes "Logged in to github.com as [username]"
- **Fail:** run `gh auth login` to fix

---

## Step 2 — BigQuery

Run:
```
gcloud auth list
gcloud auth application-default print-access-token
```
- **Pass:** an account is marked ACTIVE and a token string prints
- **Fail:** run `gcloud auth application-default login` to fix

---

## Step 3 — Obsidian Vault

Check whether the vault folder exists, in this order:
1. `C:\Users\jomit\OneDrive\Documents\vault`
2. `C:\Users\jomit\Documents\vault`
3. `C:\Users\jomit\vault`

Count the `.md` files found.

- **Pass:** folder exists and contains at least one `.md` file
- **Fail:** ask the user to confirm the vault path, then update this skill

---

## Step 4 — Gmail

Call the Gmail MCP tool to list labels (a lightweight read with no side effects):
- Use: `list_labels`
- **Pass:** returns a list of Gmail labels
- **Fail:** MCP returned an auth error or no response — tell the user to re-authenticate Gmail in Claude settings

---

## Step 5 — Google Calendar

Call the Google Calendar MCP tool to list calendars:
- Use: `list_calendars`
- **Pass:** returns at least one calendar
- **Fail:** MCP returned an auth error — tell the user to re-authenticate Google Calendar in Claude settings

---

## Step 6 — Jira (Atlassian)

Call the Atlassian MCP to check connectivity. Try fetching the user's profile or project list.
- MCP server: `plugin:pm-skills:atlassian`
- **Pass:** returns valid data
- **Fail:** MCP shows "Needs authentication" — tell the user to go to **Claude Code settings → MCP servers → Atlassian → Authenticate**, complete the browser login, then re-run prep

---

## Report

Run all six checks, then print one status block:

```
────────────────────────────────────────
  SESSION PREP — Quantum Media
────────────────────────────────────────
  GitHub          ✅  logged in as @[username]
  BigQuery        ✅  active: [email]
  Obsidian        ✅  vault found — [N] notes
  Gmail           ✅  connected
  Google Calendar ✅  connected — [N] calendars
  Jira            ✅  connected
────────────────────────────────────────
  All systems go. Ready to work!
────────────────────────────────────────
```

If anything fails, show the fix inline:

```
────────────────────────────────────────
  SESSION PREP — Quantum Media
────────────────────────────────────────
  GitHub          ✅  OK
  BigQuery        ❌  not authenticated
                  → run: gcloud auth application-default login
  Obsidian        ✅  OK
  Gmail           ✅  OK
  Google Calendar ✅  OK
  Jira            ❌  needs authentication
                  → Claude Code settings → MCP → Atlassian → Authenticate
────────────────────────────────────────
  Fix the above before starting work.
────────────────────────────────────────
```

Do not proceed with any other task until all six show ✅.

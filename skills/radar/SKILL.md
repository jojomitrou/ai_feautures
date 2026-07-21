---
name: radar
description: Use before any broad grep/search across the whole git-repos folder when the user mentions a project keyword — checks a personal keyword→location lookup table first, and builds new rows automatically as you use it, so you stop repeating yourself after twice.
version: 1.0
origin: company
---

# Radar

## Overview

A keyword → location lookup table, checked before any broad search. When a folder holds many projects, grepping all of them for every mention is slow and noisy (one term can hit 150+ files across unrelated repos). Radar's job: skip the broad search once a keyword is known, and go straight to the right repo and subfolder.

The table below ships empty except for one **example row** (format reference only — delete it once you have real rows). It is entirely personal: every real row you build reflects your own projects, and it lives inside the personal zone so upstream updates never touch it.

The distinctive part of this skill is the **learning loop** — it caches what it learns from your usage so you never have to explain the same routing more than twice.

---

<!-- personal:lookup-table:start -->
## Personal Lookup Table

| Keyword(s) | Repo | Check first, in order | Notes | confidence | learned |
|---|---|---|---|---|---|
| _example-keyword_ | `example-repo` | 1. `docs/*.md`<br>2. `src/relevant-folder/` | _delete this row once you have real ones — it's here to show the shape_ | confirmed | — |
<!-- personal:lookup-table:end -->

---

## How to Apply

1. Match the user's wording against the Keyword(s) column (substring match is fine).
2. **Row found, `confidence: confirmed`** → go straight there, skip the broad search entirely. Silent — no announcement, no question.
3. **Row found, `confidence: tentative`** → this is the keyword's *second* occurrence. Use the row (skip the broad search — that's already the payoff), but see the Learning Loop's Confirmation Pass below before treating it as settled.
4. **No row matches** → this is a new keyword. See the Learning Loop's Intro Pass below.
5. If the keyword matches more than one row, prefer the more specific (longer) match; if genuinely tied, ask once — that question doubles as that entry's confirmation pass, it doesn't count as a third ask.

---

## The Learning Loop (never repeat yourself more than twice)

**Occurrence 1 — Intro pass (no row matches):**
- Do the normal broad search this one time — but say plainly what's happening and why: *"No radar entry for '[keyword]' yet — searching broadly this once to find where it lives."* This is the intro: the user sees the action and what it's meant to achieve, nothing more is asked of them.
- Once found, add a new row tagged `confidence: tentative`, `learned:{today's date}`, with your best-guess keyword/repo/check-order/notes based on what you found.
- Tell the user in one line what got cached, e.g. *"Cached: '[keyword]' → `repo-name` — I'll confirm it's right next time this comes up."* Do not ask a question yet — that's the second occurrence's job.

**Occurrence 2 — Confirmation pass (a `tentative` row matches):**
- Use the cached row immediately (the broad search is already skipped — that's the payoff of caching on occurrence 1).
- Ask exactly one short question: *"Radar has '[keyword]' → `{repo}/{location}` from last time — still right?"* If you genuinely need another detail to nail the routing (check order, a disambiguation vs. a similarly-named repo, a gotcha), fold it into this same question rather than asking separately — this pass is allowed to double as clarification, but it is still one exchange, not two.
- On confirmation (or a corrected answer), flip the row to `confidence: confirmed`, update any details the answer changed, clear `learned:` (no longer relevant once confirmed).

**Occurrence 3 onward — silent (a `confirmed` row matches):**
- Use it, no question, no announcement. This is the steady state the whole loop exists to reach.

**Correction path (a `confirmed` row turns out wrong):** don't just patch the row in place — demote it back to `confidence: tentative` with a fresh `learned:` date, and it goes through the Confirmation Pass once more next time. A bad cache entry should never be able to calcify silently.

---

## Disambiguation

- Prefer the more specific keyword match when two rows could apply.
- A genuine tie is resolved by one question (see How to Apply, step 5) — that exchange **is** the confirmation pass for whichever row it resolves to, not an extra ask.

## Extending

Add a new project by adding one row: keyword list, repo name, ordered check-first list, and any gotcha worth flagging (legacy duplicate, wrong-repo trap, etc.) — either by hand, or let the Learning Loop build it from real usage.

<!-- personal:radar-extras:start -->
<!-- personal:radar-extras:end -->

---

## Never-do

1. Never invent a row without having actually located the answer at least once — no speculative caching.
2. Never silently apply a `tentative` row a second time without the one confirming question — that's the entire point of "never more than twice."
3. Never let a corrected/wrong row stay `confirmed` — demote it on any user correction.
4. Never ship real personal keyword rows upstream in the company version — the shipped table carries the one example row only.

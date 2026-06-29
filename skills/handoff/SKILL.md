---
name: handoff
description: Create or update a handoff.md file to capture session context for the next developer or AI session. Use this skill when the user says "handoff", "create a handoff", "update handoff", "wrap up", "end of session", "prepare handoff", "document what we did", or wants to capture current work state for continuity between sessions. Always use this skill when any of those phrases appear, even if the user just says "handoff" on its own.
---

# Handoff Skill

Generate or update a `handoff.md` in the current project root that captures the state of the current session so the next person (or AI session) can pick up immediately without losing context.

## When to Use

Invoke this skill at the end of a work session, before switching context, or any time the user wants to preserve session state. The goal is zero-friction continuity across sessions.

## Process

### Step 1: Gather Session Context

Run these commands to understand the current state:

```bash
git status
git log --oneline -10
git diff HEAD~1 --stat 2>/dev/null || git diff --stat
```

Also check for any open tasks, TODOs in modified files, and the current working directory structure.

### Step 2: Check for Existing handoff.md

Check if `handoff.md` exists in the project root:

- **If it does NOT exist**: Create it fresh using the template below.
- **If it DOES exist**: Read it first, then update only the sections that have new information. Preserve historical entries by appending to session history rather than overwriting.

### Step 3: Write or Update handoff.md

#### Template for New handoff.md

```markdown
# Handoff Document

## Last Updated
<ISO date and time>

## Project
<project name and one-line description>

## Current State
<one paragraph describing where the project is right now — what's working, what's not, overall health>

## What Was Done This Session
<bullet list of concrete things accomplished: files changed, features added, bugs fixed, decisions made>

## Pending Work
<bullet list of things started but not finished, or explicitly left for next session>

## Next Steps
<ordered list of what should be done next, with enough detail to start immediately>

## Important Context
<anything non-obvious that the next person needs to know: architectural decisions, workarounds, constraints, gotchas, why something was done a certain way>

## Recent Git Activity
<paste of `git log --oneline -10` output>

## Session History
### <date>
- <brief summary of this session's work>
```

#### Updating an Existing handoff.md

When updating:

1. **Update "Last Updated"** with the current date/time.
2. **Replace "Current State"** with the latest state (don't append — this is always the current snapshot).
3. **Replace "What Was Done This Session"** with what was done in THIS session (not previous ones).
4. **Replace "Pending Work"** with what's pending NOW (reflects current state, not history).
5. **Replace "Next Steps"** with updated next steps.
6. **Merge "Important Context"** — keep existing context that's still relevant, add new context, remove anything that's no longer true.
7. **Update "Recent Git Activity"** with a fresh `git log --oneline -10`.
8. **Append to "Session History"** — add a new entry summarizing this session. Do not remove prior entries.

### Step 4: Update Documentation if Needed

If the session included changes that affect:
- **README.md**: Update if new features, installation steps, or usage changed.
- **Any other docs**: Update the specific file if its content is now stale.

Only update documentation files that are genuinely out of date — don't rewrite docs for cosmetic reasons.

### Step 5: Report to User

Tell the user:
- Whether handoff.md was created or updated
- The path to the file
- A one-sentence summary of what was captured

## Output Format

After completing the handoff, output:

```
Handoff complete.
  File: handoff.md (<created|updated>)
  Session summary: <one sentence>
  Pending: <count> items
  Next steps: <count> items
```

## Notes

- Keep the handoff document **concise and scannable** — the reader should be able to orient themselves in under 2 minutes.
- Prefer bullet points over prose in all sections except "Current State" and "Important Context".
- If there's nothing new to report in a section, keep the previous content rather than writing "nothing to report".
- The "Session History" section is append-only — it becomes a running log of sessions over time.

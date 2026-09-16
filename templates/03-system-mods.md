# 03 — system modifications (complete ledger)

- 来源 / Source: <agent name>
- 时间 / Time: <YYYY-MM-DD>

> **Read this before changing anything.** Its purpose is to stop a new agent from undoing a previous
> fix, or deleting a backup it did not know about.

---

## A. Files and directories added

| Path | Size | Why | Reversible? |
|---|---|---|---|
| | | | |

## B. User data recovered or restored

| What | Where it went | Verified how |
|---|---|---|
| | | |

## C. Test artifacts created and removed

| Artifact | State |
|---|---|
| | removed / **left behind — check before recreating** |

## D. Deliberately NOT changed

> Record the decisions *not* to act, and who decided. These are as load-bearing as the changes.

| Thing | Why it was left alone | Decided by / when |
|---|---|---|
| | | |

## E. Permission exposure (current state, for future decisions)

| Path / object | Effective access | Who has it | Consequence |
|---|---|---|---|
| | | | |

## F. Disk usage summary

| Area | Size |
|---|---|
| | |

---

## <Letter>. <Date> — <what this change was>

**Who / when:** <agent>, <YYYY-MM-DD HH:MM>
**Trigger:** <user request>

| # | Action | Result |
|---|---|---|
| 1 | | |

**Side effects:** <files created, ACLs changed, processes left running — or "none">
**Revert procedure:** <exact steps>
**Verification:** <how you proved it worked, at the layer that failed>

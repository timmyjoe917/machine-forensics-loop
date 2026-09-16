# references — privacy & redaction

**Anything leaving this machine must pass through this file first.**

---

## Why this matters

Machine forensics artifacts are dense with identifying data: usernames appear in every path,
SIDs in every permission record, hostnames in every account name, and recycle-bin metadata contains
**literal filenames of documents the user deleted**. None of that is needed to explain a technical bug.

---

## Redaction table

| Never publish | Replace with | Why |
|---|---|---|
| Account name (e.g. a personal first name) | `<USER>` | Direct identifier |
| Host / domain / computer name | `<HOST>` | Direct identifier |
| Full SID | `S-1-5-21-...-<SUFFIX>` — **keep only the last 4 digits** | The RID is the signal; the machine SID is not |
| `C:\Users\<name>\...` | `<USERPROFILE>\...` | |
| Real file/folder names from `$Recycle.Bin`, Desktop, or Documents | `<REDACTED-FILE>` | **A list of deleted filenames is a privacy leak about the person** |
| Project directory names, thesis titles, client names | `<PROJECT>` | |
| Browser URLs, browsing history, tokens | `<REDACTED>` | Some may still be live; assume they are |
| Serial numbers, MAC addresses, IP addresses | `<REDACTED>` | |
| Email addresses, chat/messaging IDs | `<REDACTED>` | |
| Session IDs, account handles and IDs on any platform | `<SESSION-ID>`, `<ACCOUNT>` | |

**Truncated SID form keeps the technical value**: `-1003` group, `-1004` offline sandbox identity,
`-1005` online sandbox identity, `-1001` user. That is all a bug report needs.

---

## What to keep (it is the point of the report)

| Keep | Why |
|---|---|
| OS build number | Reproducibility |
| App name + version | The bug is version-specific |
| Error strings, verbatim | Searchability; that is how maintainers find duplicates |
| Log lines with the signal | Evidence |
| File ownership (`NT AUTHORITY\SYSTEM` vs a user) | Mechanism, not identity |
| ACL rights, registry rule names, exit codes | Evidence |
| Directory *structure* (e.g. `releases\<version>\bin\`) | Reproducibility |

**Rule of thumb**: a maintainer needs to reproduce the bug, not identify the reporter.
If a detail does not change whether they can reproduce it, redact it.

---

## Before posting — checklist

- [ ] Grep the draft for the account name, host name, and full SID
- [ ] Grep the draft for any substring of a real file or folder name
- [ ] Grep for `Users\` followed by anything other than `<USER>` or a literal OS path
- [ ] Check every pasted log line: does it contain a path under the user profile?
- [ ] Check screenshots separately — **screenshots are not covered by text redaction.**
      Crop or blur: window titles, sidebar thread names, recent-file lists, browser tabs, file names.
- [ ] Confirm no tokens/URLs with signatures remain

---

## Screenshots

Screenshots are the most common leak. Before sharing any:

- Crop to the exact control or error message
- Blur or crop sidebars, tab strips, recent-item lists, and window titles
- Verify no file names are legible anywhere in the frame
- Prefer a **text selection copied out of the UI** over a screenshot when the goal is just to quote a label

---

## The knowledge base itself

The knowledge base on disk may contain real names and paths — it has to, it is for the local agent.
**That is fine on the machine.** Two rules follow from it:

1. **The knowledge base is never published.** The manual is public; the notes are not. Do not push a
   knowledge base to a shared repository, and do not hand the folder to another person.
2. **The redaction table applies to anything that does leave**: bug reports, issues, gists, blog
   posts, pasted log lines, screenshots, and any *export* of a folder.

If you must move a knowledge base to another machine, it becomes **case study**, not data —
and every borrowed claim is 【假设】 until the new machine confirms it. See `SKILL.md` →
cross-machine rule.

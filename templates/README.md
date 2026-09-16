# <MACHINE> — machine forensics knowledge base

**This folder exists for one reason: so that any agent on this machine does not have to re-derive
what a previous one already established.**

Created: <YYYY-MM-DD>
Machine: <HOST> / user <USER> / <OS + build>
Agents that write here: <agent-name>, <agent-name>

---

## Before you touch anything, read in this order

| # | File | Why |
|---|---|---|
| **0** | the manual's `00-principles.md` | the two standing principles — they override everything here |
| 1 | `manifest.json` | machine-readable index: current risk, active issues, read order, **paths never to touch** |
| 2 | `01-verified-facts.md` | what is verified about this machine, with evidence |
| 3 | `03-system-mods.md` | **every change already made** — read before mutating anything |
| 4 | `05-mistakes.md` | mistakes already made here — the most valuable file |
| 5 | `04-playbook.md` | symptom → fix, for symptoms already seen here |
| 6 | `07-key-paths.md` | paths, identifiers, log signatures, one-line judgements |
| 7 | `<agent-name>/` | each agent's first-hand records, on demand |

State, in one line, what the knowledge base already says about the reported symptom — or that it
says nothing.

---

## Layout

```
<knowledge base>\
├── README.md                  ← you are here
├── manifest.json              machine-readable index
├── 00-principles.md           local copy of the principles (case history optional)
├── 01-verified-facts.md       verified facts + evidence
├── 03-system-mods.md          every change made to this machine
├── 04-playbook.md             symptom → fix
├── 05-mistakes.md             mistakes made here
├── 07-key-paths.md            paths / identifiers / log signatures
├── references/
│   └── baseline-values.md     this machine's baseline values
└── <agent-name>/              first-hand records, one directory per agent
```

Root files are the **shared layer** — what every agent here has agreed, each claim tagged.
`<agent-name>/` is one agent's **own record** — process, dead ends, wrong turns.

---

## Write protocol

**First-hand record** → `<agent-name>/<YYYY-MM-DD>-<topic>.md`, starting with:

```markdown
- 来源 / Source: <agent name>
- 时间 / Time: YYYY-MM-DD HH:MM
- 触发原因 / Trigger: <what the user asked for>
- 结论置信度 / Confidence: 已验证 | 部分推断 | 假设
```

Body structure: `templates/worklog.md` in the manual.
Tag every claim **【已验证】/【推断】/【假设】** and never write a lower level as a higher one.

**Then sync the shared layer** — new fact → `01-`; changed the machine → `03-`; new symptom → `04-`;
mistake → `05-`; new path or judgement → `07-`; risk changed → `manifest.json`.
**A first-hand record that never updates the shared layer is half-wasted work.**

**Nothing here is published.** Anything leaving this machine passes `references/privacy.md` first.

---

## Current status (one paragraph, kept up to date)

> <Risk level, what is currently degraded, what the current workaround is, and its root cause status.
> Update this every time it changes. A stale status line is worse than none.>

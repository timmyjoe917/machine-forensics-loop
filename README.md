# machine-forensics-loop

A portable discipline for diagnosing machine-level problems — with a **per-machine knowledge base**,
so that the second agent does not have to re-derive what the first one already established.

**This repository is the manual. It contains no facts about any machine.**
The knowledge base — one machine's own case notes — is created on the machine, from `templates/`,
the first time the loop runs, and grows from there.

```
manual          procedure      same for everyone, published here
knowledge base  case notes     one machine's own facts, built locally, never published
```

Everything an agent learns about *your* machine ends up in *your* knowledge base. Nothing an agent
learns about someone else's machine ships with the skill.

---

## The loop

**Read → Attribute → Reproduce with machine evidence → Fix → Prove adversarially → Write back.**

The core insight: most of the cost of debugging is re-deriving facts that were already established,
and most of the remaining cost is re-making mistakes that were already made and recorded.
This skill front-loads both.

## Install

Copy this folder wherever your agent reads skills from:

| Agent | Typical location |
|---|---|
| Codex | `<USERPROFILE>\.codex\skills\machine-forensics-loop\` |
| Any other agent | anywhere readable; point it at `SKILL.md` |

Nothing to configure. `SKILL.md` resolves the knowledge base at run time.

## First run on a machine

The agent will report that there is no knowledge base yet, then create one — empty but labelled — at
the resolved path, seeded from `templates/`. From then on, **every agent on that machine reads the
same notes before diagnosing anything**, and writes back what it finds.

Point `kb-path.txt` (created next to `SKILL.md`, git-ignored) at the folder that holds the knowledge
base, so every agent on the machine finds it without being told. Or set `$MACHINE_FORENSICS_KB`.

## What goes where

| File | Role |
|---|---|
| `SKILL.md` | the loop, Phases 0–5 |
| `00-principles.md` | the two standing principles — on-demand escalation, error-contamination guard |
| `references/knowledge-base.md` | knowledge base layout and write protocol |
| `references/report-template.md` | session records and upstream issue reports |
| `references/privacy.md` | redaction rules for anything that leaves the machine |
| `templates/` | skeletons a cold machine starts from |

## Why it is shaped this way

Two rules do most of the work, and both exist because they were violated for real:

1. **Escalation is asked for, never taken.** The sandbox is not an obstacle — it is how the decision
   gets handed back to the user.
2. **One agent's conclusion is not another's fact.** Every claim carries a source and a confidence
   tag; the reader re-verifies before citing; disagreements are settled by a test, not by authority.

The third rule is what keeps this repository useful to you: **facts never travel between machines.**
Someone else's knowledge base is a case study, never evidence about your machine.

## License

Add one if you intend others to reuse this. Without a license, default copyright applies and reuse is
not granted.

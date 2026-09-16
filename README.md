# machine-forensics-loop

**Give any AI agent a memory about your machine, so it stops re-diagnosing the same problem from
zero.**

An agent using this skill reads what is already known about the machine **before** it touches
anything, verifies with machine evidence instead of narration, fixes the problem, and writes back
what it learned — so the next agent, or the next session, starts where the last one stopped.

```
manual          procedure     same for everyone          <- this repository, and only this
knowledge base  case notes    one machine's own facts    <- created on your machine, never published
```

**This repository contains no facts about any machine.** The knowledge base is built *on your
machine*, by the agent, the first time it runs.

---

## Get it — nothing to configure

Send someone this link, or let your agent fetch it. There is no setup step, no config file to edit,
and nothing to change in the reader's environment.

| Way | Do this |
|---|---|
| **Send the link** | `https://github.com/timmyjoe917/machine-forensics-loop` |
| **Agent fetches it** | *"Clone `https://github.com/timmyjoe917/machine-forensics-loop` into your skills directory and start using it."* |
| **Download** | `Code → Download ZIP`, unzip, drop the folder into your agent's skill directory |
| **Clone** | `git clone https://github.com/timmyjoe917/machine-forensics-loop` |

Where the folder goes:

| Agent | Location |
|---|---|
| Codex | `<USERPROFILE>\.codex\skills\machine-forensics-loop\` — that is `~/.codex/skills/…` |
| Another harness with skills | that harness's skills directory |
| Anything else | anywhere it can read — point the agent at `SKILL.md` |

**Zero configuration is the intended path.** `SKILL.md` resolves the knowledge base at run time and
creates one if there is none. The optional knobs are at the bottom of this page, and you never need
them to start.

## What happens the first time

1. The agent looks for this machine's knowledge base and **says out loud that there is none** — it
   does not silently pretend to remember things.
2. It diagnoses your problem normally: read, attribute, reproduce with machine evidence, fix, prove
   it adversarially.
3. It creates the knowledge base — empty but labelled — from `templates/`, and writes down what this
   session actually established, tagged 【已验证】/【推断】/【假设】.
4. From then on, **every agent on that machine reads the same notes** before diagnosing anything,
   and writes back what it finds.

The notes stay on the machine. They are never published, and they are never copied to another machine
as if they described it.

## What is in here

| File | Role |
|---|---|
| `SKILL.md` | the loop — Phases 0–5 |
| `00-principles.md` | the two standing principles: on-demand escalation, error-contamination guard |
| `references/knowledge-base.md` | knowledge base layout and write protocol |
| `references/report-template.md` | session records and upstream issue reports |
| `references/privacy.md` | redaction rules for anything that leaves the machine |
| `templates/` | the skeletons a cold machine starts from |
| `CHANGELOG.md` | version history — check this if you downloaded a copy earlier |

## Why it is shaped this way

Two rules do most of the work, and both exist because they were violated for real:

1. **Escalation is asked for, never taken.** A sandbox is not an obstacle — it is how the decision
   gets handed back to the user.
2. **One agent's conclusion is not another's fact.** Every claim carries a source and a confidence
   tag; the reader re-verifies before citing; disagreements are settled by a test, not by authority.

The third rule is what makes this repository shareable at all: **facts never travel between
machines.** Someone else's knowledge base is a case study, never evidence about your machine.

## Optional: put the knowledge base somewhere specific

Only if you want it away from the default location:

| Knob | How |
|---|---|
| Per-machine, persistent | put one line in `kb-path.txt` next to `SKILL.md`: the absolute path |
| Per-session | set `MACHINE_FORENSICS_KB` to that path |
| Default (do nothing) | `<USERPROFILE>\.machine-forensics\` on Windows, `~/.machine-forensics/` elsewhere |

`kb-path.txt` is machine-local and is listed in `.gitignore` — it is not part of the published
manual.

## Version

`2.0.0` — the manual, and only the manual. See `CHANGELOG.md`. If you downloaded this before 2.0.0,
**discard that copy**: it bundled one machine's recorded facts alongside the procedure.

## License

MIT — see `LICENSE`. Use it, fork it, ship it inside your own tooling.

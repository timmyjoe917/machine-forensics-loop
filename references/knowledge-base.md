# references — the knowledge base: layout and write protocol

The knowledge base is **one machine's case notes**. It lives on that machine, and it never leaves it.
This file describes the shape it should have; `templates/` contains the skeletons to start from.

---

## Where it lives

Resolved in this order (see `SKILL.md` Phase 0):

1. `$MACHINE_FORENSICS_KB`
2. `kb-path.txt`, next to `SKILL.md` — one line, the absolute path
3. `<USERPROFILE>\.machine-forensics\` (Windows) / `~/.machine-forensics/` (macOS, Linux)

Whatever path is chosen, **write it into `kb-path.txt` next to `SKILL.md`** so every agent on the
machine finds the same knowledge base without asking. That file is machine-local — keep it out of any
published copy (it is listed in `.gitignore`).

Any agent on the machine can also be told the path directly; the point of step 2 is that they do not
have to be.

---

## Layout

```
<knowledge base>\
├── README.md                  index: read order, current status, write protocol
├── manifest.json              machine-readable index — agents read this first
│
├── 00-principles.md           the standing principles (copy of the manual's, case history optional)
├── 01-verified-facts.md       what is verified about this machine, with evidence
├── 03-system-mods.md          every change made to this machine — read before mutating anything
├── 04-playbook.md             symptom → diagnosis → fix, for symptoms already seen here
├── 05-mistakes.md             mistakes made here and the discipline they produced
├── 07-key-paths.md            paths, identifiers, log signatures, one-line judgements
├── references/
│   └── baseline-values.md     this machine's baseline values (identity, paths, versions)
│
└── <agent-name>/              one directory per agent: that agent's first-hand records
    └── <YYYY-MM-DD>-<topic>.md
```

Numbered files may be added or skipped — gaps are fine; the numbers are a reading order, not a
completeness checklist. Anything with no content yet should say so explicitly rather than being
absent or left empty.

The split matters:

- **The root files are the shared layer** — what every agent on this machine has agreed, with
  evidence, each claim carrying a confidence tag.
- **`<agent-name>/` is one agent's own record** — process, dead ends, wrong turns. Not shared truth.

---

## Write protocol

**First-hand records** go into your own directory, named after the agent:

```
<agent-name>/<YYYY-MM-DD>-<topic>.md
```

Create the directory on first use. Every record starts with:

```markdown
- 来源 / Source: <agent name>
- 时间 / Time: YYYY-MM-DD HH:MM
- 触发原因 / Trigger: <what the user asked for>
- 结论置信度 / Confidence: 已验证 verified | 部分推断 partly inferred | 假设 hypothesis
```

Body structure: `references/report-template.md`.

**Then synchronise the shared layer** — this is the obligation that makes the next run cheap:

| You produced | Update |
|---|---|
| a newly verified fact | `01-verified-facts.md` |
| a change to the machine | `03-system-mods.md` |
| a new symptom or fix | `04-playbook.md` |
| a mistake you made | `05-mistakes.md` |
| a new path, identifier, or judgement | `07-key-paths.md` |
| a change in risk level or issue status | `manifest.json` |

**A first-hand record that never updates the shared layer is half-wasted work** — the next agent
reads the shared layer, not your worklog.

---

## Confidence tags

```
【已验证】 verified  — machine evidence: logs, file attributes, ACLs, exit codes, SIDs, real output
【推断】 inferred   — reasoned from verified facts, not directly verified
【假设】 hypothesis — untested guess
```

Use whatever consistent three-level vocabulary you like; the requirement is that the levels exist and
that **a lower level is never written as a higher one**.

Every entry also records **where it came from** — which agent, which session. A conclusion inherited
from another agent is a lead for the reader to verify, never a fact.

---

## Cold start

On a machine with no knowledge base, Phase 5 creates one: copy `templates/` to the resolved path,
rename the files into place, fill in what this session actually established, and write `kb-path.txt`.

The correct starting content is mostly **empty but labelled**:

- `01-verified-facts.md` — machine baseline that is trivially checkable, tagged 【已验证】
- `03-system-mods.md` — "nothing recorded yet"
- `04-playbook.md` — "no symptoms recorded yet"
- `05-mistakes.md` — "nothing recorded yet" (this one will fill up fastest, and is the most valuable)
- `manifest.json` — honest `current_risk`, empty `active_issues`

**Do not invent entries to make it look complete.** A skeleton that says "nothing verified yet" is
the correct state, and it is more useful than one padded with guesses.

---

## Rules that keep the knowledge base honest

1. **One machine only.** Nothing in a knowledge base describes any other machine. A fact borrowed
   from elsewhere is 【假设】 until this machine confirms it.
2. **It is not published.** The manual is published; the notes are not. Anything leaving the machine
   passes through `references/privacy.md` first.
3. **Never delete a claim silently.** When evidence overturns something, mark it corrected and keep
   the trace — the record of how a wrong conclusion was caught is the most valuable entry in the file.
4. **A stale fact is worse than no fact.** If a version number, path, or status was true last month,
   say when it was true.

---
name: machine-forensics-loop
description: Diagnose and fix problems on any machine using a persistent, per-machine forensics knowledge base that the agent builds and maintains itself. Agent-agnostic - works for any coding agent, any OS. Use when the user reports something broken, failing, slow, missing, or asks to "check" a machine, an app, or an agent itself, before exploring from scratch. Reads this machine's existing knowledge base first, learns from recorded past mistakes, then attributes, reproduces, fixes, and writes findings back.
metadata:
  short-description: Machine forensics with per-machine persistent memory
  version: 2.0.0
  audience: any agent, any machine
---

# Machine Forensics Loop

A discipline for diagnosing machine-level problems **without repeating past mistakes**.

This package is the **manual**. It is identical for everyone, and it contains **no facts about any
particular machine**. The **knowledge base** — one machine's own case notes — is built and
maintained *on the machine*, by following the loop below. A machine that has never run this loop
starts with an empty one.

> **Manual ≠ case notes.** Reading someone else's knowledge base tells you how a *different*
> machine broke. It is never evidence about yours.

## Who this is for

**Any agent, on any machine — and the humans who work with them.**

Not tied to a product, harness, or vendor. It applies whether you are Codex, another coding agent,
or a custom harness of your own, and whether the machine runs Windows, macOS, or Linux. It needs
only two things:

1. A place to keep the knowledge base (a plain folder is enough).
2. Willingness to follow the loop: **read first, verify with machine evidence, write back.**

The two standing principles are deliberately agent-neutral: they are about how *any* agent should
handle permissions, and how it should treat *any* other agent's conclusions — including its own
past ones.

## When this applies

The user reports something broken / missing / slow / "check X" / "is X OK" on this machine.
**Do not start by exploring.** Start by reading.

## Phase 0 — Read (never skip)

### 0.1 Locate this machine's knowledge base

In this order:

| # | Source | Notes |
|---|---|---|
| 1 | `$MACHINE_FORENSICS_KB` | explicit override — wins over everything |
| 2 | `kb-path.txt` next to this `SKILL.md` | one line: the absolute path. **Machine-local — never published** |
| 3 | `<USERPROFILE>\.machine-forensics\` (Windows) or `~/.machine-forensics/` (macOS, Linux) | default for a machine that has never run this before |

**If none of them exists**, say so out loud — *"no knowledge base for this machine yet; I am starting
cold"* — then work normally and create it in Phase 5, seeding it from `templates/`. Ask for approval
before writing outside your writable roots.

### 0.2 Read it, in this order

1. `00-principles.md` — the two standing principles. **They override everything else here.**
   Use the copy shipped with this manual; a knowledge base may keep a local copy with its own
   case history attached.
2. `<kb>/manifest.json` — machine-readable index: current risk, active issues with status, read
   order, invariants, **known-dangerous paths**.
3. `<kb>/README.md` — the write protocol for that knowledge base.
4. The files listed in `<kb>/manifest.json` → `read_order`. At minimum, read the verified-facts file
   and the mistakes file before touching anything.
5. State, in one line, what the knowledge base already says about the reported symptom.
   If it says nothing, say that explicitly and proceed.

Do not silently skip this phase.

## Phase 1 — Attribute

Separate **observation** from **conclusion**. A report of the form "X is broken" is an observation;
"X is broken because Y" is a hypothesis the user (or a previous agent) has handed you.

- Treat every incoming report's *conclusions* as unverified, including your own past ones.
- Distinguish layers: the app, the shell, the sandbox, the filesystem, the OS.
  Failure in a *lower* layer makes symptoms in every upper layer identical.
- Find the **earliest** evidence, not the most recent: the first log file, the first account created,
  the first failure. Symptom-onset date ≠ root-cause-onset date.

## Phase 2 — Reproduce with machine evidence

Get a signal that goes red on *this* problem, and read it from a layer the failing component
cannot influence.

- Prefer logs, exit codes, file attributes, ACLs, and SIDs over narration — including your own.
- **A component's self-report is not evidence that it ran.** Cross-check against an independent
  artifact.
- **"Enumeration returned empty" ≠ "the thing is absent."** Before concluding absence, verify with a
  **mechanically different** method.
- When something is reported missing, check whether the *lookup path* is broken rather than the
  target. A dangling path produces the same error text as a missing file.

Read the full log history, not just today — a dormant fault plus a triggering change is a common
shape.

## Phase 3 — Fix

Before mutating anything:

- Read the modifications file. Do not undo a previous fix or delete a prior backup.
- Prefer a **reversible** change; record how to reverse it.
- Writes outside the workspace need the user's approval. Ask; do not route around a denial.

Verify the fix at the **same layer that failed**, and re-verify end-to-end afterward.
A fix that only passes a proxy check is not verified.

## Phase 4 — Prove it, adversarially

Before reporting success:

- **Make it fail first.** Break the thing deliberately, confirm your diagnostic detects it, then
  repair and confirm recovery. A tool that has only ever been run in the healthy state is untested.
- Execute the repair path for real at least once, not just the diagnostic path.
- Check for side effects: leftover test files, changed ACLs, orphaned processes.
- Verify the fix survived: re-run the check after the repair.

## Phase 5 — Write back

Update the knowledge base resolved in Phase 0. This is not optional — it is what makes the next run
cheap. **On a cold machine, this is the phase that creates the knowledge base.**

**Cold start:** create the knowledge base at the resolved path by copying `templates/` and filling in
what the current session actually established. Create the directory structure, `manifest.json`, and
the empty-but-labelled record files. An empty skeleton that says "nothing verified yet" is the
correct starting state — do not invent entries to make it look complete.

**Every run:** write your **one-hand record** into your own worklog directory (one subfolder per
agent, named after the agent — a fresh knowledge base has none yet; create yours), named
`<YYYY-MM-DD>-<topic>.md`, with the header and confidence tags the protocol requires. Then update
the **shared layer** for anything every agent on this machine should know:

- Append the session log with the timeline **including what you got wrong and how it was caught**.
- Update the verified-facts file: move items between 【已验证】/【推断】/【假设】 as evidence lands.
- Update the modifications file if you changed anything.
- Update `manifest.json`: current risk, active issue statuses, newly discovered invariants.
- Add new symptoms and their fixes to the playbook.
- If you made a mistake, record it. **A recorded mistake is the skill's most valuable asset.**

**A one-hand record that never updates the shared layer is half-wasted work** — the next agent will
read the shared truth, not your worklog.

Layout, filenames, and headers: `references/knowledge-base.md`.

## Standing discipline

Two principles apply to **every** agent using this skill, and override everything else here.
Full text: `00-principles.md`.

**① On-demand escalation.** Stay in the sandbox's writable workspace. To touch anything outside it,
*ask for approval* — never route around a denial. The sandbox is not an obstacle; it is the mechanism
that hands the decision back to the user. Check the knowledge base's `manifest.json` →
`test_path_rules` before writing anything: some paths cannot be granted at all, and a failed grant
can kill the current turn's command channel.

**② Error-contamination guard.** **One agent's conclusion is not another's fact.** Every claim in the
shared layer carries a source and a confidence tag; the inheriting agent **re-verifies before
citing**; disagreements are settled by a test, never by authority. This applies to *your own past
conclusions* too — treat them as leads, not facts.

### Cross-machine rule (the reason this manual is separate from the notes)

**Facts never travel between machines.** A knowledge base is about exactly one machine. Do not copy
another machine's verified facts, paths, SIDs, versions, or mistakes into this machine's knowledge
base as if they described it.

If you are handed someone else's knowledge base, read it as **case study** — how a similar fault was
reasoned about — and label anything you borrow as 【假设】 until *this* machine confirms it.

The failure modes the loop exists to prevent. Each one happened at least once, on a real machine:

| Anti-pattern | Corrective |
|---|---|
| Naming the symptom-onset date as the root-cause date | Find the earliest "from nothing to something" timestamp |
| Inferring capability from a permission table's *absence* | Test it. One command often falsifies the inference |
| Treating one mechanism's observation as another's behavior | Read and write are separate mechanisms; ACL ≠ sandbox profile ≠ integrity level |
| Building a negative conclusion on one enumeration method | Cross-validate with a mechanically different method |
| Telling a helper to act on a path it lacks the rights to change | Check ownership and required privilege **before** issuing the instruction |
| Reporting a conclusion from a component's self-report | Verify from outside that component |
| Citing another agent's (or your own past) conclusion as fact | Re-verify, or label it 【推断】 |

When you cannot verify something, say so and label it 【推断】 or 【假设】.
Never promote an inference to a verified fact for narrative convenience.

## References

- `00-principles.md` — the two standing principles, in full
- `references/knowledge-base.md` — knowledge base layout, write protocol, sync obligations
- `references/report-template.md` — session records and upstream issue reports
- `references/privacy.md` — redaction rules before anything leaves the machine
- `templates/` — the skeletons a cold machine starts from

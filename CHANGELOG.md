# Changelog

## 2.0.0 — the manual, and only the manual

**If you downloaded a copy before 2.0.0, discard it.** That package bundled one machine's recorded
facts — paths, identities, versions, incident history, past mistakes — alongside the procedure.
None of it describes your machine. Keep nothing from it except the discipline.

What changed:

- `SKILL.md` resolves the knowledge base **at run time** instead of pointing at a fixed folder:
  `$MACHINE_FORENSICS_KB` → `kb-path.txt` next to `SKILL.md` → `~/.machine-forensics/`.
- On a machine with no knowledge base, the agent reports a **cold start** and creates one from
  `templates/`. The previous version assumed a populated knowledge base already existed, and fell
  back to "explore from scratch" when it did not.
- `templates/` added — skeletons for every knowledge base file, plus the one-hand record.
- `references/knowledge-base.md` added — layout, write protocol, sync obligations.
- `references/privacy.md` now states plainly that the **knowledge base is not published**; only the
  manual is. Redaction alone was the right answer to the wrong question.
- `00-principles.md` is the de-identified, portable copy. The case histories that produced the two
  principles remain — correctly — inside the knowledge base that produced them.
- Cross-machine rule made explicit: someone else's knowledge base is a case study, and anything
  borrowed from it is 【假设】 until your own machine confirms it.

## 1.1.0 — agent-agnostic positioning

- Audience widened from one agent pair to **any agent, any machine, any OS**.
- Added `## Who this is for` and the confidence-tag vocabulary to the public text.

## 1.0.0 — first published package

- The procedure and one machine's knowledge base, exported together and redacted.
- Correct diagnosis discipline, wrong packaging: readers inherited another machine's case notes as if
  they were their own. Superseded by 2.0.0.

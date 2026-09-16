# 01 — verified facts

- 来源 / Source: <agent name>
- 时间 / Time: <YYYY-MM-DD>
- 结论置信度 / Confidence: <已验证 | 部分推断 | 假设>

> **This file is the machine's baseline.** Every entry carries evidence and a confidence tag.
> **Nothing in here was inherited from another machine.** A claim borrowed from elsewhere is 【假设】
> until this machine confirms it.

---

## 1. Environment baseline 【】

| Item | Value | How it was established |
|---|---|---|
| OS / build | <> | <> |
| Host / user | <HOST> / <USER> | <> |
| Privilege level | <> | <> |
| Agent products + versions | <> | <> |

---

## 2. Confirmed problems 【】

### <problem name>

- **Symptom** — verbatim error text, when it started, how often it reproduces
- **Root cause** — the mechanism, and how it was confirmed
- **Evidence** — the command / log line / file attribute that proves it
- **Status** — fixed | worked around | open

---

## 3. Permission / identity model 【】

<Who processes run as, which groups exist, what the access-control situation is.>

> **Read ≠ write.** Record which mechanism grants which, and do not infer one from the other.

---

## 4. Delivered fixes 【】

<What was repaired, when, and how it was verified. Cross-reference `03-system-mods.md`.>

---

## 5. Open questions (honest list)

<Things that are still unclear. Keep them here rather than letting them leak into facts.>

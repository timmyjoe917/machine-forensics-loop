# references — report templates

Two templates. Both enforce the same rule: **label confidence, never launder an inference into a fact.**

---

## A. Session record (for the knowledge base)

Filename: `<agent-name>/<YYYY-MM-DD>-<topic>.md`

```markdown
# <Title>

- 来源 / Source: <agent name>
- 时间 / Time: YYYY-MM-DD HH:MM
- 触发原因 / Trigger: <what the user asked for>
- 结论置信度 / Confidence: 已验证 verified | 部分推断 partly inferred | 假设 hypothesis

## 症状 / Symptom
<What was observed, verbatim error text, how many times reproduced, under what conditions>

## 归因 / Attribution
<Root cause. Separate observation from conclusion.>

- 【已验证】<claim> — 证据: <command / log line / file attribute>
- 【推断】<claim> — 依据: <which verified facts it follows from>
- 【假设】<claim> — 未验证，验证方法: <exact command>

## 排查过程 / Investigation
<What was tried, in order. INCLUDE dead ends and wrong turns — they are the asset.>

## 修复 / Fix
<What was changed, where, and how to reverse it>

## 验证 / Verification
<How the fix was proven. Must include the failing layer, not a proxy.>
<State explicitly if the fix was only tested in the healthy state.>

## 副作用与残留 / Side effects & leftovers
<Files created, ACLs changed, processes left, disk used. Or "none".>

## 未解决 / Open
<What remains unfixed, and why. Do not omit this section.>
```

---

## B. Upstream issue report (public — **run `privacy.md` first**)

Keep it evidence-dense and identity-free. A maintainer needs to reproduce it, not identify you.

```markdown
# <Concise, specific title naming the component and the failure>

## Summary
<2–4 sentences: what fails, when, and the one-line mechanism.>

## Environment
| | |
|---|---|
| OS | <build number> |
| App | <name + exact version> |
| Component | <the binary/CLI version> |
| Config | <relevant keys, e.g. sandbox mode> |

## Symptom
<Verbatim error string in a code block. Note reproduction rate (N/N).>
<State whether it happens before any user command runs.>

## Root cause
<The mechanism. If you have it, this is the highest-value section.>
<Include the path/tree structure that must exist vs what actually exists.>

## Evidence
<Log lines with the signal. Truncated SIDs (last 4 digits only). Paths as <USERPROFILE>\...>
<Before/after if you have a working comparison.>

## Reproduction
<Minimal deterministic steps. Say explicitly if you cannot reproduce it from scratch.>

## Impact
<What is unusable. Generalize: "every command", "the whole session", not "my command".>

## Suggested fix
<Optional. Be concrete but do not over-claim.>

## Notes
<Timeline if useful: when it started, what changed. Version change is often the trigger.>
```

### Issue quality checks

- [ ] Title names the component, not the emotion
- [ ] Exact version numbers present
- [ ] Error strings verbatim, in a code block, searchable
- [ ] Reproduction rate stated (e.g. "14/14 attempts")
- [ ] Distinguishes *what you saw* from *what you concluded*
- [ ] Root cause section says how confident you are
- [ ] **Every claim in the summary traceable to an evidence line below**
- [ ] Redaction checklist in `privacy.md` passed

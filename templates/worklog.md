# <title>

- 来源 / Source: <agent name>
- 时间 / Time: YYYY-MM-DD HH:MM
- 触发原因 / Trigger: <what the user asked for>
- 结论置信度 / Confidence: 已验证 | 部分推断 | 假设

> Copy this file to `<agent-name>/<YYYY-MM-DD>-<topic>.md`. Keep the sections; delete the guidance in
> angle brackets. **Include the dead ends** — the wrong turns are the asset.

---

## 症状 / Symptom

<What was observed. Verbatim error text. How many times, under what conditions.>

## 归因 / Attribution

<Root cause. Keep observation and conclusion apart.>

- 【已验证】<claim> — 证据: <command output / log line / file attribute>
- 【推断】<claim> — 依据: <which verified facts it follows from>
- 【假设】<claim> — 未验证，验证方法: <exact command>

## 排查过程 / Investigation

<What was tried, in order — including what did not work and what you got wrong.>

## 修复 / Fix

<What changed, where, and how to reverse it.>

## 验证 / Verification

<How it was proven, at the layer that failed. Say explicitly if it was only tested in the healthy
state.>

## 副作用与残留 / Side effects & leftovers

<Files created, permissions changed, processes left, disk used — or "none".>

## 共享层同步 / Shared-layer sync

<Which root files you updated: 01 / 03 / 04 / 05 / 07 / manifest.json. A record that syncs nothing is
half-wasted work.>

## 未解决 / Open

<What remains unfixed, and why. Do not omit.>

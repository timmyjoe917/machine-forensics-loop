# 04 — playbook (look up by symptom)

- 来源 / Source: <agent name>
- 时间 / Time: <YYYY-MM-DD>

> One section per symptom **actually seen on this machine**. Generic debugging advice belongs in the
> manual, not here. When a new symptom is diagnosed, add it — with the one-line judgement that
> distinguishes it from its look-alikes.

---

## General discipline

1. Read `manifest.json` first — especially the list of paths you must never use for testing.
2. Prefer a read-only check over a mutating one. Never run a mutating test as the first probe.
3. Verify at the layer that failed, not through a proxy of it.
4. State what you did **not** verify.

---

## Symptom A — <short description>

**One-line judgement** — the command that tells you whether this is the problem:

```powershell
# copy-pasteable, binary outcome
```

**If it is this:**

```powershell
# the fix
```

**Verified how:** <how you know the fix works — ideally by having made it fail first>
**Related:** <other symptoms it is confused with>

---

## Traps

> Mistakes that cost real time here. Each entry: what looks right, what is actually true, what to do.

| Looks like | Actually | Do this instead |
|---|---|---|
| | | |

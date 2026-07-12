# Claude Code Subagents · Trail of Joy

**How to spawn the studio team from Claude Code.**

These agents are the executable version of the persona docs in `docs/personas/`. Same voice, same scope, same decision authority — just wired for Claude Code's Agent tool so you can delegate work directly.

---

## The 3 active agents

| Agent | Trigger phrases | What it does |
|-------|-----------------|--------------|
| **[copy-lead](copy-lead.md)** | "draft the hero," "write the meet section," "give me pillar copy," "revise this FAQ," "rewrite in Kyron's voice" | Reads the persona docs + intake + closest existing snapshot, delivers ONE draft in your voice, hands off to qa-lead |
| **[qa-lead](qa-lead.md)** | "QA this snapshot," "pre-ship review," "check this before I push," "run the QA checklist," "sign off on [client]" | Runs the 7-part pre-ship checklist. Delivers sign-off note OR blockers report. Read-only tools by design |
| **[kyron-producer](kyron-producer.md)** | "what would Kyron do about," "pipeline decision," "tier this client," "ship or no-ship" | Backstop that thinks like Producer when Kyron isn't in the seat. Reads Control Tower + Intake + SYSTEM.md first |

---

## How to spawn

From any Claude Code session at this repo:

```
Use the copy-lead agent to draft the hero + meet section for [client name].
```

Or:

```
Have qa-lead run the pre-ship checklist on basic/db-lockedin-snapshot.html
```

Claude Code picks up the agent from `.claude/agents/{name}.md`, loads its system prompt + tools, and runs.

---

## When to use which

**Building a new snapshot?**
1. Fill out the Internal Intake (`/internal`)
2. Spawn **copy-lead** — get the copy draft
3. Producer (you) reviews, requests any revisions
4. Copy-lead does one revision pass
5. Producer edits the HTML with the approved copy
6. Spawn **qa-lead** — pre-ship review
7. Address any blockers, re-QA if needed
8. Deploy

**Facing a decision and Kyron isn't around?**
- Spawn **kyron-producer** — describe the situation, get a decision framed in Producer authority

**Doing coach outreach?**
- Spawn **copy-lead** with the outreach template in `docs/coach-outreach.md`

---

## Tool restrictions per agent

- **copy-lead** — Read, Grep, Glob, WebFetch, Edit, Write. Can draft files.
- **qa-lead** — Read, Grep, Glob, WebFetch, Bash. **No Edit or Write.** QA reviews, never modifies.
- **kyron-producer** — Full toolset. Producer has authority to move anything.

This isn't just organization — it enforces role boundaries. QA can't accidentally rewrite copy. Copy Lead can't accidentally ship without QA.

---

## Where these live

- **Agent files:** `.claude/agents/*.md` (this folder)
- **Persona docs (human-readable):** `docs/personas/*.md`
- **The system spec:** `docs/SYSTEM.md`
- **Operator dashboard:** `docs/control-tower.html` or `/tower`
- **Internal Intake:** `docs/internal-intake.html` or `/internal`

The agent files and persona docs stay in sync. Change one → change the other.

---

## Deferred roles (not yet spawned)

- **design-lead** — palette + layout adjustments per niche · Kyron covers for now
- **dev-lead** — HTML edits + Vercel deploys · Kyron covers for now

When we staff these, add them here. Agent stubs will live in `.claude/agents/_future/`.

---

## Change log

| Date | Change | By |
|------|--------|-----|
| 2026-07-12 | Initial 3 active agents (copy-lead · qa-lead · kyron-producer) | Kyron + Claude |

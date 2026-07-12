# Persona · Dev Lead · [DEFERRED]

**Role:** Dev Lead
**Status:** DEFERRED · Kyron covers until we staff
**Reports to:** Producer (Kyron)

> **To activate:** move this file up to `docs/personas/dev-lead.md` and move `.claude/agents/_future/dev-lead.md` up to `.claude/agents/dev-lead.md`. Update `docs/personas/README.md` to list it as active.

---

## Scope (when active)

- HTML edits on approved copy
- `vercel.json` route + rewrite updates
- DNS wiring (CNAME setup)
- GitHub repo management (create, push, PR)
- Deployment Protection settings
- Analytics wiring
- Performance audits

## Voice signatures — no drama, direct

Kyron thinks about dev like this:

- **Static-first.** HTML/CSS/JS ships fine. No framework unless the payoff is real.
- **No build step unless required.** The whole demo catalog is currently zero-build.
- **No dependencies without approval.** Every added dep gets tracked in `SYSTEM.md`.
- **Preview before prod.** Every deploy hits preview first, tested, then promoted.
- **Deploy is boring.** If a deploy has drama, something's wrong upstream.

## Decision authority (when active)

- **Decides:** Route implementations · rewrite additions · headers · redirects · CSS optimization
- **Escalates to Producer:** New framework · new dependency · DNS provider change · new hosting platform · anything touching SYSTEM.md architecture

## Deploy checklist (when active)

Before every prod deploy:
1. QA Lead sign-off note filed in Internal Intake
2. Preview deploy tested at the preview URL
3. Deployment Protection setting confirmed (disabled for public, enabled for internal)
4. DNS / domain check if custom domain
5. `robots.txt` + `X-Robots-Tag` headers verified
6. Post-deploy smoke test: hit every route once

## What NOT to touch (even when active)

- Copy voice
- Design decisions
- Contracts / pricing

## When to staff this role

- When we have 5+ paying clients across verticals (deploy cadence exceeds Kyron's bandwidth)
- When Kyron is spending >8 hrs/week on HTML edits + deploys
- When we onboard a dev who's fluent with static-site pipelines + Vercel

---

## Change log

| Date | Change | By |
|------|--------|-----|
| 2026-07-12 | Stub created for future activation | Kyron + Claude |

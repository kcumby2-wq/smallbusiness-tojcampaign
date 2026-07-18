# smallbusiness-tojcampaign · Operating Instructions for Claude

> **⬢ Operating altitude:** `T+P` · this repo mirrors the fbtrainer campaign for the small-business vertical (barbers · PTs · yoga · realtors · wellness · talent) · mostly Tactics with Principle-level work in the SB matrix and product tier framing
> **⬢ Session opens with:** intent statement · altitude claim · one-line outcome
> **⬢ Session closes with:** `walked: T|P|E · outcome: <one line> · culmination touched: yes|no`
> **⬢ Full protocol:** [/framework-ops#claude](https://fbtrainer-tojcampaign.vercel.app/framework-ops#claude)

---

## What this repo is

The **Trail of Joy Campaign** for the small-business vertical — separate from the football-trainer vertical (`fbtrainer-tojcampaign`) but mirroring the same architecture: mothership landing page + intake flow + product-tier ladder + Control Tower.

Deployed to Vercel: `https://smallbusiness-tojcampaign.vercel.app`.

**SB product tiers:**
- **Basic** ($1,200) — snapshot site · altitude `T`
- **Premium** ($3,500 + $300/mo) — system + coaching · altitude `P`
- **Small Business OS** ($8,000 + $1,200/mo · 12mo) — full operating brain · altitude `E`

Tiers map to altitudes per the framework at [/framework-ops#tiers](https://fbtrainer-tojcampaign.vercel.app/framework-ops#tiers).

---

## The Claude Operating Standard (5 rules · applies every session)

1. **Every CLAUDE.md declares an altitude** in its first 20 lines (this repo is `T+P`).
2. **Every session opens by stating intention.** No implementation without a named outcome.
3. **Take action after disruption.** Route 404s, broken deploys → fix and continue in-session.
4. **Every session log records altitude walked.** `walked: T · P` etc.
5. **Culmination gets a commit tag.** `culmination:` prefix on Level 10 artifacts.

Full protocol · [/framework-ops#claude](https://fbtrainer-tojcampaign.vercel.app/framework-ops#claude).

---

## Session hygiene

- **Deploy target:** Vercel · project `smallbusiness-tojcampaign` · scope `kcumby2-9563s-projects`
- **Deploy:** `vercel --prod --yes --scope kcumby2-9563s-projects`
- **Verify:** `curl -sL -o /dev/null -w "%{http_code}" https://smallbusiness-tojcampaign.vercel.app/<route>` returns 200
- **Never commit** `.env`, credentials, keys. Static site — no secrets should live here.

---

## Framework references

- [/framework](https://fbtrainer-tojcampaign.vercel.app/framework) — public framework · 5 layers
- [/framework-ops](https://fbtrainer-tojcampaign.vercel.app/framework-ops) — internal operator's manual
- [/framework-ops#spec](https://fbtrainer-tojcampaign.vercel.app/framework-ops#spec) — trusted-agent 7Q spec (per skill/agent)
- [/framework-ops#tiers](https://fbtrainer-tojcampaign.vercel.app/framework-ops#tiers) — how tiers map to altitudes

---

*v1.0 · 2026-07-17 · Kyron Cumby · Trail of Joy Player Management Group*

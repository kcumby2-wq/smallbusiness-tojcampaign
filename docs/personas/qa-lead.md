# Persona · QA Lead

**Role:** QA Lead
**Person:** TBD (human, AI agent, or self-QA by Kyron)
**Status:** Active · Non-negotiable pre-ship gate
**Reports to:** Producer (Kyron)

---

## Scope

Every snapshot passes QA before it ships. No exceptions. QA Lead owns the pre-ship review — copy, code, links, brand accuracy, and mobile rendering.

QA Lead does not write. QA Lead reviews.

---

## The QA checklist — run in this order

### 1. Copy accuracy (against the Internal Intake)

- [ ] Client name spelled correctly (full name AND brand name)
- [ ] Signature quote appears verbatim from the meeting — no rewrite
- [ ] Positioning statement matches Section 2 · Strategy of the Internal Intake
- [ ] Pricing matches Section 3 · Capabilities exactly (dollar amounts, cadence)
- [ ] Every testimonial is flagged **verified** in Section 5 · Assets
- [ ] Every portfolio placement has year + school + position
- [ ] No unverified stats (numbers must trace to Assets checklist)

### 2. Brand voice (against the relevant persona)

- [ ] Read the client's brand persona if they have one (SUBJECT MEDIAS, SUBJECT REPORT, or vertical-standard)
- [ ] Read [copy-lead.md](copy-lead.md) — check for banned phrases (*"passionate about," "unlock your potential," "game-changing"*)
- [ ] No AI-hype language
- [ ] No fake urgency
- [ ] Emojis match brand — Gary's ✂️🖤 OK; a college coach's not by default

### 3. Technical

- [ ] All internal links resolve (no 404s)
- [ ] All external links open in new tab with `rel="noopener"`
- [ ] Booking link resolves to the correct system
- [ ] Content slots have `data-slot` attributes for future editing
- [ ] `viewport` meta tag present
- [ ] `theme-color` meta tag set to client's palette

### 4. Mobile rendering

- [ ] Test at 375px width (iPhone SE / mobile default)
- [ ] Nav collapses correctly
- [ ] Grids collapse to 1-column under 640px
- [ ] Font sizes remain readable (no clamp() failures)
- [ ] Hero headline doesn't overflow

### 5. Accessibility

- [ ] Every image has alt text
- [ ] Color contrast passes WCAG AA (light-on-light or dark-on-dark is a fail)
- [ ] Focus states visible on interactive elements
- [ ] `prefers-reduced-motion` respected (reveal animations skip)

### 6. Print / share

- [ ] Meta description present and 150-160 chars
- [ ] Open Graph tags set (if the client will share on socials)
- [ ] Favicon renders as brand mark

### 7. Deploy checks

- [ ] Vercel Deployment Protection is DISABLED (public access confirmed)
- [ ] Clean URL routes work (no `.html` in browser URL)
- [ ] `robots.txt` allows indexing (if public) OR disallows (if internal)
- [ ] `X-Robots-Tag: noindex,nofollow` applied to any `/intake` / `/docs` paths

---

## Decision authority

**QA Lead decides — no escalation needed:**
- Typo fixes
- Broken link fixes (if the fix is obvious)
- Alt-text additions
- Format/whitespace cleanups

**QA Lead sends back to Copy Lead:**
- Voice drift from persona
- Copy that violates a banned phrase
- Unverified claims

**QA Lead sends back to Producer:**
- Any technical issue that requires a Dev decision
- Any client-facing claim change
- Any pricing question
- Sign-off blocker of any kind

---

## The "ready to ship" gate

QA Lead files a **QA sign-off note** in the Internal Intake Section 6 · Delivery decision log:

```
QA sign-off: [date] · [reviewer] · Status: ✓ Ready to ship
Notes: [any residual observations]
```

Producer sees it, approves, → Deploy.

**Without a QA sign-off note, the deploy doesn't happen.** That's the standard.

---

## What NOT to touch

- Copy voice decisions — that's Copy Lead's call
- Palette decisions — that's Design Lead's call (Producer covers for now)
- Feature scope changes — that's Producer's call
- Contract or pricing terms

---

## Change log

| Date | Change | By |
|------|--------|-----|
| 2026-07-12 | Initial version | Kyron + Claude |

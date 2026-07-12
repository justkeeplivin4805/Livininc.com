# LiViN Website — Iteration Map for AI Agents

**Read this file before editing `index.html`.** It tells you what's where, what the conventions are, and what NOT to break.

This file is intended for any AI agent (Claude, Gemini, Codex, Cursor, etc.) that picks up this codebase. Humans can read it too.

---

## Project at a glance

- **Single-file static site:** `index.html` contains all HTML, CSS (in `<style>`), and JS (in `<script>`). No build step. No dependencies installed locally.
- **External fonts only:** Google Fonts (`Inter`, `JetBrains Mono`). Loaded via `<link>` tags in `<head>`.
- **Hosting model:** Netlify static site, optionally Git-deployed (see `DEPLOY.md`).
- **Form backend:** Formspree (`xdaboodj`).
- **Booking backend:** Calendly (`livin4069/30min`).

---

## File structure inside `index.html`

The file is divided by section comments shaped like:
```
<!-- ===================== SECTION NAME ===================== -->
```

Use these to navigate. In order:

| Section comment | What's there | Element ID |
|---|---|---|
| `NAV` | Top navigation bar (sticky, blurred bg) | `<nav>` |
| `HERO` | Headline, tagline, CTA, spec-card mockup | `#top` |
| `TRUST BAR` | 4 small credibility tiles | (no id) |
| `HOW I WORK` | Short discipline statement — the "decided vs. delivered" thesis that frames both practices below. No card grid, no bg change, short padding — reads as connective tissue between Trust Bar and Capabilities, not a full section. | `#how-i-work` |
| `CAPABILITIES` | 6-card grid of procurement capabilities | `#capabilities` |
| `DECISION TO DELIVERY` | 4-card grid: the executive-advisory practice (Discovery, Decision Criteria, Mapped to the End Result, Held Through Execution). Peer section to Capabilities, same `cap-grid`/`cap-card` treatment. Not yet in top nav or footer — added 2026-07-11, holding on nav promotion until the section has more content/proof behind it (see `LIVIN_BRAND_EVOLUTION_STRATEGY.md` in the project root for the full rationale). | `#decision-practice` |
| `VERTICALS` | 4 cards: healthcare, off-road, recreational, & beyond | `#verticals` |
| `CROSS-BORDER / LATAM` | 4-card grid + featured healthcare-LATAM callout | `#cross-border` |
| `PUBLIC SECTOR / GOVERNMENT` | 3-card grid: SAM.gov, Bidnet Direct, Scope | `#public-sector` |
| `WHY LIVIN` | 2-column: stats + operating principles | `#why` |
| `PROCESS` | 4-step process row | `#process` |
| `CTA` | Mid-page large CTA | (no id) |
| `CONTACT` | Contact info + Formspree form | `#contact` |
| `FOOTER` | Logo, link columns, copyright | `<footer>` |

---

## Design system (live in CSS variables)

All colors and key spacing live in `:root` near the top of the `<style>` block. Change them once, change the whole site.

```css
--bg: #0a0e14;             /* page background */
--bg-elev: #11161f;         /* elevated panels */
--bg-elev-2: #161c27;       /* deeper elevation */
--line: #1e2633;            /* hairlines */
--line-strong: #2a3344;     /* card borders */
--text: #e6ebf2;            /* primary text */
--text-dim: #9aa4b3;        /* body text */
--text-faint: #5d6675;      /* labels, eyebrows */
--accent: #c9a961;          /* primary gold/amber */
--accent-bright: #e6c47a;   /* hover gold */
--accent-dim: #8a7440;      /* darker gold for gradients */
--accent-blue: #4a90b8;     /* steel blue (used for cross-border/LATAM) */
```

**Do not introduce new colors without updating `:root`.** Every accent should reference a variable.

### Typography
- Body: `Inter`, weights 300–800
- Mono / labels / spec text: `JetBrains Mono`
- Headline scaling: `clamp()` based — already responsive, don't hardcode `font-size` in px on `h1`/`h2`.

### Spacing
- Sections use `padding: 120px 0` (80px on mobile via `@media (max-width: 768px)`).
- Container is `max-width: 1200px` with `padding: 0 32px` (`0 20px` on mobile).

### Components
Reusable utility classes (don't redefine these — extend them):

- `.eyebrow` — small mono uppercase label above headlines
- `.btn .btn-primary` / `.btn .btn-secondary` — buttons
- `.cap-card` — capability card (used in capabilities + cross-border grids)
- `.vert-card` — vertical card (with hover top-border animation)
- `.process-step` — process row item
- `.contact-method` / `.form-field` — contact area
- `.spec-card` — the mock spec card in the hero (Bloomberg-terminal vibe)

---

## Common edit recipes

### Change the accent color
1. Edit `--accent`, `--accent-bright`, `--accent-dim` in `:root`.
2. Visually QA the spec card, hero CTA, capabilities numbers, process step bars, and the Cross-Border featured callout (which uses `--accent-blue` for separation — keep that distinct).

### Add a vertical to the "What We Source" grid
1. Find `<!-- ===================== VERTICALS ===================== -->`.
2. Copy one `.vert-card` block, paste, edit the icon SVG + heading + paragraph + examples line.
3. Adjust `.vert-grid` `grid-template-columns` if you go past 4 cards (currently `repeat(4, 1fr)`).

### Update the contact form fields
- Form is inside `#contact`, action is `https://formspree.io/f/xdaboodj`.
- Add a `<div class="form-field">…</div>` block; Formspree picks up any `name="…"` attribute.

### Swap the Formspree form
- Replace `https://formspree.io/f/xdaboodj` (one occurrence) with the new endpoint URL.

### Swap the Calendly link
- Search for `https://calendly.com/livin4069/30min` — three occurrences (hero CTA, contact section, footer). Replace all.

### Change the email or phone everywhere
- `procurement@livin-inc.com` — appears in 2 places (contact section + footer).
- `+1 (000) 000-0000` — display string; appears in contact section.
- `tel:+10000000000` — actual link href; same place.

### Add a new section
1. Place it between two existing `<section>` tags following the same comment-divider convention.
2. Wrap content in `<div class="container">…</div>`.
3. Open with `<div class="section-head">` containing the eyebrow, h2, and lead paragraph.
4. Add a nav link in `.nav-links` if it deserves top-level navigation.
5. Add to footer's link columns if it's a top-tier capability.

---

## Things to NOT change without a reason

- **Tagline:** *"If you can spec it, I can find it."* This is the brand line. Don't paraphrase it casually.
- **Trust bar tiles:** They've been deliberately scoped to avoid revealing entity-level details (EIN, state of incorporation). Don't add those back.
- **Single-file structure:** Don't split into multiple files unless you also update `DEPLOY.md` and the Netlify publish settings. Keeping it as one file is intentional — it makes deploys trivial and AI edits unambiguous.
- **Reveal animations:** The IntersectionObserver in the bottom `<script>` block hooks into `section, .hero-grid > *, .cap-card, .vert-card, .process-step, .principle-list li, .why-stat`. If you add a new section that should fade-in on scroll, either give its top-level cards one of those classes or extend the selector list.

---

## Quality checklist before any commit

Run through this list before pushing a change:

1. Open `index.html` in a browser (just double-click it). Does it look right?
2. Resize the browser down to ~375px wide. Does anything overlap, overflow, or wrap badly?
3. Click every nav link — do they smooth-scroll to the right section?
4. Click every CTA button — do the right ones go to `#contact`, the right ones to Calendly?
5. Submit the contact form once on the live site after deploying — does Formspree receive it?
6. View source: are there any `REPLACE_WITH_…` placeholders left? (There shouldn't be.)
7. Check the footer year (handled automatically by JS, but verify it renders).

---

## Where to ask for help

- **DEPLOY.md** — phase 1 (go-live) and phase 2 (Git + Netlify auto-deploy) walkthroughs.
- **CLAUDE.md** in the project root — the LiViN business context any agent should hold while working on this site.

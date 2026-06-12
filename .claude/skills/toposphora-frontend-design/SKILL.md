---
name: toposphora-frontend-design
description: >
  Create production-grade UI for toposphora-web — the public marketing /
  landing site for the Toposphora expert witness practice management
  platform. Enforce the static-HTML stack rule, navy/amber visual
  identity, domain semantics, accessibility, and copy conventions. Avoid
  generic SaaS or AI-generated aesthetics. The authenticated product app
  (toposphora-ui) is a separate repo with its OWN design skill and a
  different palette — do not apply this skill there.

stack:
  framework: >
    NONE. Single static file: index.html. Plain HTML + CSS. This is a
    hard rule — no build system, no dependencies, no JavaScript
    frameworks, no API calls, no React. Minimal vanilla JS only if a
    feature truly requires it.
  prohibited:
    - React, Vue, or any framework
    - Tailwind or any utility-first CSS
    - npm dependencies / build steps
    - API calls or backend integration (no keys, no tokens — static site)
    - JavaScript-dependent core content (page must read fully without JS)
  hosting: >
    GitHub Actions deploys to AWS S3 (toposphora-web-prod) + CloudFront
    on push to main. Railway is decommissioned. The Dockerfile is
    legacy/local-only — the pipeline does not use it.

audience_and_tone:
  audience: [plaintiff attorneys, defense attorneys, prospective expert witnesses]
  tone: serious professional services — not SaaS startup
  goals: [trust, credibility, conversion]
  ui_characteristics:
    - generous whitespace and section rhythm
    - strong content hierarchy via type scale
    - minimal motion — one orchestrated page-load sequence at most
    - emphasis on copy and proof over interaction

design_tokens:
  source: >
    src/styles/tokens.css is canonical. index.html inlines the subset it
    uses in its :root block — KEEP THE TWO IN SYNC: any token change
    edits both places.

  colors:
    navy:        "--color-navy: #1A3A5C — primary actions, topbar logo"
    navy_dark:   "--color-navy-dark: #0D1B2A — ink, headings, body text"
    navy_light:  "--color-navy-light: #2A547E — hover on navy elements"
    amber:       "--color-amber: #C4922A — accent and badge-dot ONLY, never a fill"
    bg:          "--color-bg: #F5F7FA — page background"
    surface:     "--color-surface: #FFFFFF — cards, topbar"
    border:      "--color-border: #E0E6ED"
    mid:         "--color-mid: #4A6078 — secondary text, nav links"
    subtle:      "--color-subtle: #7A93AD — tertiary text"
    focus_ring:  "--color-focus-ring: #2B7FD4"
    note: >
      This navy/amber palette is the MARKETING SITE's system. The product
      app (toposphora-ui) keeps its own teal/sand palette as separate
      canon; do not "harmonize" one repo into the other without an
      explicit ask. Asset state: favicon.svg is navy on #F5F7FA
      (re-stroked in PR #20); favicon.png and og-image.png are still
      teal-era binaries pending regeneration.

  typography:
    families:
      sans: "'Sora' — all UI text"
      mono: "'IBM Plex Mono' — uppercase labels, eyebrow text, numbers"
    loading: >
      Google Fonts <link> in index.html head: Sora 300/400/600/700 and
      IBM Plex Mono 400/600 with display=swap. Sora 500 is NOT loaded —
      use 600 for medium emphasis, or extend the fonts URL if a new
      weight is genuinely needed.
    scale: >
      Custom property scale from tokens.css (--text-hero 2.25rem,
      --text-h1 1.6rem, --text-h2 1.2rem, --text-h3 1rem, --text-body
      0.875rem, --text-small 0.8rem, --text-label 0.68rem uppercase
      tracked). Derive sizes from these tokens, not ad-hoc rem values.
      The h1 is the one sanctioned departure: clamp(var(--text-hero),
      4vw, 3rem).

  shape:
    radius: "--radius: 0px — sharp corners everywhere; minimal shadows; flat background"

  buttons:
    primary: "navy fill (--color-navy) / white text / 0px radius / Sora 600"
    secondary: "transparent bg / navy text / no border / underline ghost pattern"
    note: "Never use amber as a button fill. Amber is accent and badge-dot only."

  nav:
    pattern: >
      Non-sticky white topbar (--topbar-* tokens): border-bottom, diamond
      logo + brand name left (navy, Sora bold, uppercase), mono uppercase
      tagline right. No nav links and no CTA in the topbar — Request
      Access / Sign In CTAs live in the hero and closing contact blocks.

styling_rules:
  - All CSS lives in index.html's <style> block; tokens mirrored from src/styles/tokens.css
  - Every color, spacing, and type value derives from the :root custom properties — no hardcoded hex/px/rem where a token exists
  - Media queries use the page's actual breakpoints — max-width 980px (hero stacks) and max-width 700px (topbar and service grid stack); the 639/1024/1280 scale commented in tokens.css is aspirational, migrate only as an explicit task
  - No inline style attributes

semantic_html:
  - nav, main, section, article, header, footer — use correctly
  - Never div or span where a semantic element fits
  - Interactive elements must be natively focusable (button, a — never div onClick)
  - Headings form a strict hierarchy; one h1 per page

anti_patterns:
  visual:
    - Inter, Roboto, Arial, or system fonts as primary typeface (use Sora)
    - Any border radius other than 0px in this repo
    - Purple gradients, glassmorphism, neumorphism, neon accents, soft glows
    - Generic card-grid hero layouts; oversized hero with vague slogans and no real content
    - Scattered micro-animations — one orchestrated sequence or none
    - Amber as a button fill color
    - Color as sole status differentiator — always pair with a text label
  code:
    - Introducing a framework, build step, or npm dependency
    - API calls, fetch, or any backend integration
    - Hardcoded hex/px/rem values where tokens exist
    - Letting index.html's :root drift from src/styles/tokens.css
  ux:
    - CTAs pointing anywhere other than https://app.toposphora.com
    - Lorem ipsum or placeholder proof points
    - Marketing claims about PHI/case data handling beyond what the platform does
    - Pricing copy anywhere on the site without an explicit ask (PR #15 added a pricing card; PR #16 reverted it)

decision_rules:
  - Correctness of domain semantics beats everything
  - Accessibility (WCAG AA, keyboard, motion) beats aesthetics
  - Clarity and credibility beat visual cleverness
  - Copy and proof beat interaction on this site

accessibility:
  - WCAG 2.1 AA contrast on all text and interactive elements
  - Keyboard accessible: visible :focus-visible outline (--color-focus-ring)
  - All animation wrapped in prefers-reduced-motion media query
  - Meaningful alt text; decorative graphics get empty alt

domain_vocabulary:
  expert witness:   "Expert or Expert Witness — never Doctor, User, Member"
  legal matter:     "Case or Matter — never Project, Ticket"
  retaining firm:   "Retaining Counsel or Firm — never Client"
  time tracking:    "Time Tracking — never Timekeeping (sounds like clock-in/clock-out employment)"
  invoice:          "Invoice — never Bill, Receipt"
  intermediary:     "Toposphora is NOT an intermediary — never use that framing in copy"
---

# Toposphora Frontend Design Skill — toposphora-web

## Scope

This skill governs the **marketing site only**: a single static
`index.html` deployed to S3 + CloudFront at `https://toposphora.com`.
The authenticated product app (`toposphora-ui`, app.toposphora.com) is a
separate React/Tailwind repo with its own skill and a teal/sand palette
— never share code, assets, or styling decisions between the two repos.

## Page conventions

- **Hero**: real value proposition with concrete proof, not slogans.
  Content hierarchy carried by the type scale tokens.
- **Sections**: generous vertical rhythm; copy-first, one idea per
  section.
- **CTAs**: every "get started" / "sign in" action links to
  `https://app.toposphora.com`. No other destinations.
- **Motion**: at most one orchestrated page-load sequence, fully wrapped
  in `prefers-reduced-motion`.

## Token workflow

1. Define or change the token in `src/styles/tokens.css` (canonical).
2. Mirror the change into the inlined `:root` block in `index.html`.
3. Never let the two drift — a reviewer should be able to diff them.

## Copy principles

- Non-meta voice (locked by PRs #17/#19): short declarative sentences
  that name observable system behavior ("Toposphora structures engagement
  setup, document handling, scheduling visibility, and billing
  workflows…"). No "why/how" framing, no friction/philosophy language,
  no generic SaaS marketing tone, no legal disclaimers in body copy.
- When two adequate words fit, use the plainer one — "management", not
  "infrastructure".
- Speak to attorneys and experts in their own vocabulary (see
  domain_vocabulary above).
- Credibility through specifics: real capabilities, real workflow steps.
- Never describe Toposphora as an intermediary between counsel and
  expert.
- No PHI, case details, or client names in any copy or imagery.
- No pricing copy without an explicit ask from Dan.

## Maintaining this skill

This skill must agree with the repo CLAUDE.md — if they conflict,
CLAUDE.md wins and this skill is stale: update it. When the design
system changes (tokens, fonts, layout patterns), update
`src/styles/tokens.css`, `index.html`, and this skill together.

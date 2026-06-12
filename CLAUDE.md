# Claude Code — Toposphora Web

## Source of Truth

GitHub (`github.com/Toposphora/toposphora-web`) is the single source of truth.
Local copy lives at `C:\Users\danow\Dev\toposphora-web`.

## Branching

- `main` is canonical. Never commit directly to `main`.
- Every Claude session works on a dedicated `claude/<task>-<id>` branch.
- At end of session: push branch and open a PR against `main`.
- Claude may create and merge PRs as long as there are no merge conflicts. If conflicts exist, leave the PR open for Dan to resolve.
- After merging, clean up: checkout `main`, pull, prune remote refs, delete local feature branch.

## Commit Style

- Conventional commits: `feat:`, `fix:`, `chore:`, `refactor:`, `docs:`
- Keep messages short and specific (≤72 chars)

## Stack

- Static HTML/CSS — no build system, no dependencies
- Single file: `index.html`
- Fonts loaded from Google Fonts (Sora, IBM Plex Mono)
- No JavaScript frameworks

## Purpose

Public-facing marketing/landing page for Toposphora LLC. Describes the expert witness practice management platform for attorneys and expert witnesses.

## Design Tokens

- Canonical source: `src/styles/tokens.css`. The subset `index.html` uses is
  inlined in its `:root` block — keep the two in sync.
- Background: `#F5F7FA`; surfaces: `#FFFFFF`; borders: `#E0E6ED`
- Primary navy: `#1A3A5C`, ink/navy-dark: `#0D1B2A`, hover navy-light: `#2A547E`
- Amber accent: `#C4922A`
- Fonts: Sora (all UI text; no 500 weight — use 600); IBM Plex Mono (uppercase
  labels, eyebrow text)
- Shape: sharp corners (`--radius: 0`), minimal shadows, flat background

## Hosting

- Deployed via GitHub Actions to **AWS S3 + CloudFront** on every push to `main`.
- S3 bucket: `toposphora-web-prod`. CloudFront distribution `EZMRLWLN9USW7` fronts `toposphora.com`. DNS for `toposphora.com` is hosted in **AWS Route 53** (zone `Z06219612T920IVQ6C6RN`); Namecheap is the registrar and the nameservers are delegated to AWS (`ns-*.awsdns-*`).
- Railway is decommissioned — do not assume `railway up` works for this repo.
- The repo also ships a `Dockerfile` for legacy/local-container use. The deploy pipeline does not use it.

## Security

- No API keys or tokens — this is a static site.
- No backend calls from this repo.

## Cross-Repo Context

- All CTAs and "get started" links must point to `https://app.toposphora.com`
  (the authenticated product app). Never point them to any other URL.
- The product app is a separate repo (`toposphora-ui`) deployed independently.
  Do not attempt to share code, assets, or build pipelines between the two repos.

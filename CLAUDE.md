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
- Fonts loaded from Google Fonts (EB Garamond, Manrope)
- No JavaScript frameworks

## Purpose

Public-facing marketing/landing page for Toposphora LLC. Describes the expert witness practice management platform for attorneys and expert witnesses.

## Design Tokens

- Background: `#f7f3ed`
- Primary teal: `#1a5f5e`, deep teal: `#123c3d`
- Sand accent: `#a48659`
- Body font: Manrope; heading font: EB Garamond

## Hosting

- Deployed via GitHub Actions to **AWS S3 + CloudFront** on every push to `main`.
- S3 bucket: `toposphora-web-prod`. CloudFront distribution fronts `toposphora.com`. DNS is in Route 53 hosted zone `Z06219612T920IVQ6C6RN`.
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

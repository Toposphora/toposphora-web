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

## Security

- No API keys or tokens — this is a static site
- No backend calls from this repo

## Session End Checklist

At the end of every session:
- Compare the local `CLAUDE.md` against the version on `main`. If they differ,
  merge meaningful changes into one version, commit it, and discard the other.
  There must never be two competing versions of this file.
- Ensure no feature branches remain locally or on the remote.
- Ensure `main` is checked out and up to date.

## Cross-Repo Context

- All CTAs and "get started" links must point to `https://app.toposphora.com`
  (the authenticated product app). Never point them to any other URL.
- The product app is a separate repo (`toposphora-ui`) deployed independently.
  Do not attempt to share code, assets, or build pipelines between the two repos.

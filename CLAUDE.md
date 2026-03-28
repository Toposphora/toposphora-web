# Claude Code — Toposphora Web

## Source of Truth

GitHub (`github.com/Toposphora/toposphora-web`) is the single source of truth.
Local copy lives at `C:\Users\danow\Dev\toposphora-web`.

## Branching

- `main` is canonical. Never commit directly to `main`.
- Every Claude session works on a dedicated `claude/<task>-<id>` branch.
- At end of session: push branch and open a PR against `main`.
- Do not merge the PR — the human reviews and merges.
- Remind the user to run the following after merging each PR on their local machine:
  ```
  git checkout main
  git pull origin main
  ```

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

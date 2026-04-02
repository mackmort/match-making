# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static single-page marketing website for **Kenzie Morton Matchmaking**. The entire site is a single `index.html` file (~720 lines) with all CSS inlined in `<style>` and all JS inlined in `<script>`.

## Architecture

- **No build system, no dependencies, no package manager.** Just open `index.html` in a browser.
- CSS uses custom properties defined in `:root` (lines 19–27) for the design system: `--bg`, `--navy`, `--earth`, `--serif` (Cormorant Garamond), `--sans` (Inter).
- Only external resource: Google Fonts CDN.
- Sections in order: Nav, Hero, Process, Details, About, Contact, Footer, Mobile Menu.
- JS (lines 669–718): hamburger menu toggle, sticky nav on scroll, IntersectionObserver scroll-reveal.

## Hosting & Deployment

- **Hosted on Netlify** at `kenziemorton.com` (and `www.kenziemorton.com`)
- **Repo**: `mackmort/match-making` on GitHub (private, client-owned)
- **Auto-deploy**: every push to `main` triggers a Netlify deploy — no build command, no manual steps
- **Domain DNS**: managed in Namecheap
- **SSL**: Let's Encrypt via Netlify, auto-renewing

## Development

To preview locally: open `index.html` directly in a browser, or use any static file server (e.g., `python3 -m http.server`).

To deploy: push to `main` on `mackmort/match-making`. Netlify picks it up automatically.

No tests, linting, or build steps exist.

## Key Constraints

- All styles are inline in `<style>` — there is no external CSS file.
- All scripts are inline in `<script>` — there is no external JS file.
- The file is large (~356KB) due to inline CSS; use offset/limit when reading.
- Contact email: kenzie@kenziemorton.com

## Working Preferences

### Security
- Never commit `.env*` files, API keys, tokens, or credentials. Never read/grep `.env.local`.
- Keep secrets out of logs and error messages.
- Sanitize user inputs to prevent injection, XSS, and path traversal.
- Ask before making external API calls (cost/rate-limit concerns).

### Git Discipline
- Always create a feature branch; never commit directly to main.
- Review each hunk with `git add -p`.
- Branch naming: `ui/`, `feat/`, `fix/`, `chore/`, `hotfix/` prefixes.
- Commit format: `type(scope): what` with multiline details.

### Communication
- **Default to asking** when unclear, when multiple approaches exist, or when changes affect other areas.
- Call out user-visible behavior changes explicitly before implementing.
- Format terminal commands as inline text, not markdown code blocks (avoids zsh line-wrap issues).

### Code Quality
- Keep code simple — avoid unnecessary abstractions, especially for MVP work.
- No TODOs or commented-out code left behind.
- Only comment where logic isn't self-evident.

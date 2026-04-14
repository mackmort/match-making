# Progress Log

## 2026-04-14 — Hero, Desktop Nav, Footer Updates

### What Changed
1. **Hero tagline** — Added "in Mexico City" to the main description: *"A more thoughtful, personal approach to meeting people in Mexico City through carefully curated introductions."*
2. **Desktop nav links** — Added `@media (min-width: 769px)` media query to show `.nav-links` with `display: flex`. Links (Process, Application, About, Get in touch) are now visible on desktop without opening the hamburger menu. Existing link styles and scrolled-state colors already handled both states.
3. **Footer expansion** — Replaced copyright-only footer with email link (`kenzie@kenziemorton.com`), "Based in Mexico City", and copyright. Added subtle hover styles for the email link.

### PRs
- #9 — ui(homepage): add Mexico City, desktop nav links, expanded footer

### Notes
- Changes driven by feedback from five external reviewers (see `website-proposal.md`)
- Items 6, 7, 8 from the proposal — all marked ✅ (no client input needed)

## 2026-04-02 — Application Page (Intake Form + Scheduling)

### Architecture Decisions
- Created a separate `/apply` page (new `apply.html`) for the application flow
- **Cal.com free tier** for intro call scheduling — embedded inline widget connected to `kenziemortonmatchmaking@gmail.com` (dedicated Gmail for calendar)
- **Netlify Forms** for intake questionnaire delivery — submissions emailed to kenzie@kenziemorton.com
- Scheduling first, then questions — maximizes conversion (low-friction booking first)

### What Was Built
1. **`apply.html`** — Two-step application page:
   - Step 1: Cal.com embedded scheduling widget (`kenzie-morton-matchmaking/15min`)
   - Step 2: 10-question intake questionnaire (all textareas, long-form)
   - Form is locked until Cal.com booking is confirmed
   - After booking, Cal.com widget collapses to compact confirmation with date/time
   - Page auto-scrolls to questionnaire after booking
   - Name/email captured from Cal.com booking event as hidden fields (no duplicate entry)
   - Honeypot spam protection on the form
   - Success message after form submission
2. **`index.html`** — Updated CTAs across the site:
   - Hero CTA: "Get in touch" → "Apply" → links to `/apply`
   - Nav "Application" link → `/apply`
   - Mobile menu "Application" link → `/apply`
   - Contact section: "Apply" as primary CTA, email as secondary

### Post-Deploy Setup (Client)
- [ ] Configure Netlify form notification email (Netlify dashboard → Forms → application → Notifications → add kenzie@kenziemorton.com)
- [ ] Change Cal.com slot interval from 15 min to 30+ min (Cal.com → Event Type → Advanced)
- [ ] Optionally remove "Additional notes" from Cal.com booking questions

### PRs
- #2 — Add application page with Cal.com scheduling + intake form
- #3 — Fix Cal.com booking event detection (switched from postMessage to Cal.com embed event API)
- #4 — Collapse Cal.com widget after booking, fix scroll behavior

### Key Technical Notes
- Cal.com's embed uses its own event API (`Cal("on", { action: "bookingSuccessfulV2" })`) — not raw `postMessage`
- Cal.com confirmation emails come from the connected calendar's email address, not a custom domain — this is an industry-wide limitation
- Form lock is CSS-only (`pointer-events: none`); not a security boundary, just UX guidance

## 2026-04-02 — Hosting Setup (GitHub + Netlify + Custom Domain)

### Accounts & Ownership
- Client (mackmort) owns both the **GitHub** and **Netlify** accounts
- Nicholas added as a **collaborator** on GitHub repo `mackmort/match-making`
- No Netlify collaborator needed — deploys are automatic from GitHub pushes

### Repository
- Initialized git repo locally and pushed to `mackmort/match-making` (private)
- Branch: `main`
- Initial commit includes `index.html`, `CLAUDE.md`, and `docs/`

### Netlify Deployment
- Connected Netlify to GitHub repo via "Sign up with GitHub"
- No build command, publish directory is `/`
- Auto-deploys on every push to `main`
- Netlify subdomain: `dancing-kangaroo-9a1468.netlify.app`

### Custom Domain (kenziemorton.com)
- Added `kenziemorton.com` as primary domain and `www.kenziemorton.com` as redirect alias
- DNS configured in Namecheap, SSL provisioned via Let's Encrypt
- Client's email (`kenzie@kenziemorton.com`) confirmed still working

### Workflow Going Forward
- Push changes to `main` on GitHub → Netlify auto-deploys to `kenziemorton.com`
- No manual deployment steps needed

## 2026-04-01 — Mobile Responsiveness & Cleanup

### Hosting Decision
- Going with **Netlify drag-and-drop** (Option A) for simplicity and cost ($0 hosting + ~$10-15/yr domain)

### Changes Made
1. **Hamburger menu breakpoint** — Moved nav collapse from 480px to 768px so the hamburger appears on tablets, not just phones
2. **Mobile hero sizing** — Changed from a fixed vw height to aspect-ratio: 3/4 with min-height: 520px so the full heading, subtitle, and button are visible. Removed the conflicting 480px hero height override
3. **Hero overlay** — Strengthened the gradient overlay for better text-on-photo contrast
4. **Hero text shadows** — Added text-shadow to the heading and paragraph text for readability
5. **Hero subtext opacity** — Removed the 0.6 opacity that was making "I work with a small number of clients at a time" hard to read. Moved the inline style attribute to a proper .hero-subtext CSS class
6. **Hero content overlap fix** — Reset margin-bottom: 0 on mobile to prevent the -40px desktop margin from pushing content out of view
7. **Nav z-index fix** — Bumped nav to z-index: 103 so the hamburger X button is visible and tappable over the mobile menu overlay. Removed the now-unnecessary z-index: 102 from the hamburger
8. **Hamburger X always white** — Added .hamburger.open span { background: #fff } so the close icon is visible regardless of scroll state
9. **Dead Application links** — Changed href="#" to href="#contact" in both the nav and mobile menu
10. **Mobile body font size** — Reduced from 18px to 16px at the 768px breakpoint
11. **Mobile details list** — Price list items use flexbox row layout with name left-aligned and price right-aligned, keeping each item on one line
12. **Larger mobile tap targets** — Increased button padding for hero and contact CTAs

# Progress Log

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

# Security Review — index.html

**File**: index.html (356KB)
**Date**: 2026-04-01
**Verdict**: Clean — no malicious content found

## Summary

Single-page HTML file for "Kenzie Morton Matchmaking". All CSS is inline, which accounts for the large file size. The file contains no malicious code, obfuscation, or suspicious external resources.

## External Resources

| Resource | URL | Status |
|----------|-----|--------|
| Google Fonts | `https://fonts.googleapis.com/css2?family=Cormorant+Garamond...&family=Inter...` | Safe (trusted CDN) |

No other external scripts, stylesheets, or iframes are loaded.

## Script Analysis (lines 669–718)

One `<script>` block containing vanilla JavaScript with three functions:

1. **Hamburger menu toggle** (lines 670–686) — toggles CSS classes and `aria-hidden` on mobile menu open/close.
2. **Sticky nav on scroll** (lines 688–698) — adds/removes a `scrolled` class on the nav element when the user scrolls past 60px.
3. **Scroll reveal animation** (lines 700–717) — uses `IntersectionObserver` to fade in page sections as they enter the viewport.

## Checks Performed

| Check | Result |
|-------|--------|
| `eval()`, `atob()`, `document.write()`, `fromCharCode` | None found |
| `<iframe>` tags | None found |
| `<form action="...">` to external URLs | None found |
| Obfuscated or base64-encoded strings | None found |
| External JS loaded via `<script src="...">` | None found |
| Cookie or localStorage access | None found |
| Network requests (fetch, XMLHttpRequest) | None found |

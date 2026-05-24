# Proposed Fixes

## 01: Discovery / SEO (S2)
**Reproduction:** Inspect `<head>` of deployed URL. Note missing tags.
**Root Cause:** Codebase never had SEO/Discovery features prioritized.
**Proposed Fix:** Add standard SEO meta tags, Open Graph tags, and a `WebApplication` JSON-LD schema inside `<head>`.
```html
    <meta name="description" content="A kid-friendly financial dashboard to track allowances, 529s, and savings goals. Build wealth habits early.">
    <link rel="canonical" href="https://carto79.github.io/kids-money-dashboard/">
    <meta property="og:title" content="Kids Money Dashboard | Taitt Fin">
    <meta property="og:description" content="A kid-friendly financial dashboard to track allowances, 529s, and savings goals.">
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://carto79.github.io/kids-money-dashboard/">
    <!-- Add JSON-LD here -->
```
**Regression Risk:** Low. Pure HTML additions.
**Verification:** Run through Google Rich Results Test endpoint.

## 02: Mobile UX Grid Overflow (S2)
**Reproduction:** Load app on 375px viewport (iPhone SE simulation). Observe horizontal scrollbar.
**Root Cause:** `accounts-grid` uses `minmax(350px, 1fr)` but body padding leaves only 335px available.
**Proposed Fix:** Reduce min-width to `280px`.
```css
        .accounts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
```
**Regression Risk:** Desktop columns might look slightly narrower if auto-fitting creates more columns.
**Verification:** Chrome DevTools -> iPhone SE -> verify `document.body.scrollWidth === window.innerWidth`.

## 03: Accessibility Focus Flow (S2)
**Reproduction:** Press `Tab`. Cards are skipped.
**Root Cause:** `<div class="account-card">` lacks keyboard attributes.
**Proposed Fix:** Add `tabindex="0" role="button" aria-label="Account card"` to the JS generation of the card. Add `onkeydown` handler to trigger flip on Enter/Space.
**Regression Risk:** Low.
**Verification:** axe-core scan and manual Tab navigation.

## 04: Kid Safety / COPPA Disclaimer (S2)
**Reproduction:** Search for "privacy" or "data".
**Root Cause:** Overlooked in initial MVP.
**Proposed Fix:** Add a footer at the bottom of `index.html`.
```html
    <footer style="text-align: center; color: #ff8c00; margin-top: 50px; font-size: 0.9em; padding-bottom: 20px;">
        <p>Built for The Ezra Show by Taitt Fin.</p>
        <p><strong>Privacy Promise:</strong> All data is stored locally on your device. We do not collect, transmit, or store any personal information.</p>
    </footer>
```
**Regression Risk:** None.
**Verification:** Manual visual check.

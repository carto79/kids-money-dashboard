# Phase 1 Test Plan: Kids' Money Dashboard

Based on synthesized project context, here is the objective Test Plan prior to execution.

## 1. Scope
**In Scope:**
*   **Target Application:** `index.html` and all bundled static assets (HTML/CSS/JS).
*   **Data Persistence:** Browser `localStorage` (state schema `kidsMoneyDashboardV2`).
*   **Features:** Setup Modal, Account Grid (flip cards), College Savings Tube, Chart generation (Pie/Bar/Millionaire), CSV/Word Document export functionalities.
*   **Discovery:** SEO meta tags, Open Graph tags, canonical structures, structured data (JSON-LD) for the primary application landing page.
*   **Accessibility:** WCAG 2.2 AA compliance, semantic HTML, keyboard operability, screen reader viability.
*   **Kid Safety:** COPPA compliance, PII scrutiny, third-party script auditing.

**Out of Scope:**
*   Server-side validation (none exists, purely static).
*   Authentication flows (app operates entirely locally without a backend).

## 2. Test Environments
*   **Primary:** Mobile emulation (375px viewport), throttled 4G via Chrome DevTools / Lighthouse.
*   **Secondary:** Tablet (768px viewport) and Desktop (1280px+ viewport) via standard Chromium.

## 3. Personas
*   **Ezra-the-child:** Wants big buttons, readable fonts, obvious feedback ("You're doing AMAZING!"), and visual progress (College Tube).
*   **Parent-the-supervisor:** Wants robust data persistence, ability to wipe data, accuracy in financial math, and kid-safe privacy guarantees.
*   **Adversary-the-curious-tester:** Attempts to enter negative balances, malformed names, excessively large numbers, HTML injection in inputs, and tests `localStorage` limits.

## 4. Risk-Ranked Feature List
1.  **Local Storage Persistence & State Management:** (Highest Risk) Corrupted state locks out the app entirely.
2.  **College Savings Tube Logic:** Recently refactored. Risk of division by zero or UI overflow.
3.  **Document Export (Word/CSV):** Relies on Blob construction and canvas data URLs; risk of CORS issues or silently failing on iOS devices.
4.  **Discovery & SEO Structures:** (High Business Impact) Missing JSON-LD, generic titles, or broken Open Graph tags prevent the app from serving its marketing purpose.
5.  **Chart.js Rendering:** Canvas animations inside 3D CSS transforms (flipping cards) are notoriously brittle across different browsers.

## 5. Discovery Audit Scope
*   Validate `<title>`, `<meta name="description">`, and canonical URL.
*   Audit Open Graph & Twitter Card tags.
*   Design and validate Schema.org structured data (JSON-LD): `Organization`, `WebSite`, `WebApplication`.
*   Ensure a compliant `robots.txt` and `sitemap.xml` are generated.
*   Verify cross-linking properties (Substack, YouTube).

## 6. Pass/Fail Thresholds
*   **Performance:** Lighthouse Mobile ≥ 90, LCP < 2.5s.
*   **Accessibility:** axe-core Critical/Serious violations = 0.
*   **Security/Safety:** 0 third-party trackers. 0 remote data transmission.
*   **Functionality:** 100% of defined Happy/Sad paths pass without console errors.
*   **Discovery:** Validated schema with zero errors in Google Rich Results Test.

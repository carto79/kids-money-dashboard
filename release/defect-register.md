# Defect Register

| ID | Feature | Precondition | Steps | Expected Result | Actual Result | Status | Severity |
|----|---------|--------------|-------|-----------------|---------------|--------|----------|
| 01 | Discovery/SEO | Page load | Inspect `<head>` | Canonical, OG tags, description, and JSON-LD schema present | None present. Generic `<title>` | OPEN | S2 (High) |
| 02 | Mobile UX | View on 375px viewport | Observe Accounts Grid | Grid scales down, no horizontal scroll | Grid forces horizontal scroll (`minmax(350px)` > 335px available) | OPEN | S2 (High) |
| 03 | Accessibility | Keyboard Navigation | Tab through UI | All interactive elements receive focus and can be activated with Enter/Space | Flip cards cannot be focused. Lack `role="button"` | OPEN | S2 (High) |
| 04 | Kid Safety / Compliance | Page load | Search for Privacy / COPPA statement | Clear disclosure that data is stored locally and no PII is collected | No privacy statement exists | OPEN | S2 (High) |
| 05 | Mobile UX | Touch Targets | Tap "back" (✕) on a flipped card | Touch target is ≥ 44x44px | Touch target is 30x30px | OPEN | S3 (Medium) |
| 06 | Security | Page load | Inspect Chart.js script tag | Tag includes `integrity` hash for SRI | No integrity hash present | OPEN | S3 (Medium) |

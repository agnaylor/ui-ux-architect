# Example Output: ui-accessibility-audit

> Reference for what a finished audit looks like. Notice: pass/fail table at top, severity-tagged findings with WCAG citations, resilience coverage explicit, top-3 quick wins called out.

---

## Accessibility Audit: Thermomix Sync — Home Screen
**Platform:** Mobile/Web App
**WCAG Target:** 2.1 AA
**Overall:** PASS WITH FIXES (2 majors, 3 minors)

### Pass/Fail Summary

| Category | Status | Notes |
|---|---|---|
| Perceivable | ✓ | Body text contrast 12.1:1. Status colors backed by labels, not color-only. |
| Operable | ✗ | Touch target on overflow menu is 32×32px — fails 44×44 minimum. |
| Understandable | ✓ | Form inputs have visible labels. Errors actionable. |
| Robust | ✓ | Semantic `<button>`, `<nav>`, `<main>`. ARIA only where needed. |
| Resilience States | ✗ | Empty state present. Loading uses skeleton. Error state on sync failure exposes raw `BluetoothError: 0x80004005` — leaks tech detail. |
| Platform Rules | ✓ | Primary `Sync` CTA lives in lower third (thumb zone). No fixed header eating > 64px. |

---

### Findings

#### [BLOCKER] Sync error exposes raw Bluetooth error code
- **Where:** `<ErrorBanner />` in `HomeScreen.tsx` line 142.
- **Why it fails:** Resilience covenant — never expose raw system errors to the UI. Also violates WCAG 3.3.1 (error identification must be human-readable).
- **Fix:** Localize to `Can't reach <device-name>. Verify it's powered on and try again.` Stash the raw code behind an optional `Details` link that opens a debug panel. Use copy from `reference/copy-bank.md` → Connection errors.

#### [MAJOR] Overflow menu button is 32×32px
- **Where:** `.overflow-button` in `HomeScreen.module.css` line 87.
- **Why it fails:** Mobile blueprint requires ≥ 44×44px touch target (WCAG 2.5.5).
- **Fix:** Increase tap area to 44×44 via padding while keeping the visual icon at 16×16. CSS:
  ```css
  .overflow-button { padding: 14px; min-width: 44px; min-height: 44px; }
  ```

#### [MAJOR] No `aria-label` on the device-card status indicator
- **Where:** `<StatusBadge>` instances in the device card row.
- **Why it fails:** Screen reader users hear only `Optimal` without context (WCAG 4.1.2). The dot's meaning ties to a device but isn't announced.
- **Fix:** Already supported by the component — pass an explicit label:
  ```tsx
  <StatusBadge status="ok" label={`${device.name}: Optimal`} />
  ```

#### [MINOR] Focus indicator is browser default
- **Where:** All interactive elements in `HomeScreen.tsx`.
- **Fix:** Apply token-defined focus style globally:
  ```css
  :focus-visible {
    outline: 2px solid var(--accent-primary);
    outline-offset: 2px;
    border-radius: 4px;
  }
  ```

#### [MINOR] Snackbar auto-dismiss is 3s — no manual close
- **Where:** `<SyncSuccessSnackbar />`.
- **Why it could fail:** WCAG 2.2.1 — users with cognitive disabilities may need more time to read.
- **Fix:** Add a close button (`aria-label="Dismiss notification"`) AND honor `prefers-reduced-motion` by extending duration to 6s if motion preferences indicate slower pacing.

#### [MINOR] No `prefers-reduced-motion` handling
- **Where:** Recipe-card slide-up transition (200ms).
- **Fix:** Wrap motion in a media query:
  ```css
  @media (prefers-reduced-motion: reduce) {
    .recipe-card-enter { transition: none; }
  }
  ```

---

### Resilience Coverage

| State | Status | Notes |
|---|---|---|
| Default | ✓ | Recipe card + Sync CTA render correctly. |
| Loading | ✓ | Skeleton recipe card with Warm Ash pulse. |
| Empty | ✓ | `Pick a recipe to sync` with `Open library` CTA. |
| Error | ✗ | Raw Bluetooth error string surfaces. See [BLOCKER] above. |

---

### Top 3 Quick Wins (~20 min total)

1. **Localize the sync error.** One copy swap fixes the blocker AND the leaky tech detail. (5 min — pull from `copy-bank.md`.)
2. **Expand overflow menu tap area to 44×44.** Pure CSS change, no markup. (3 min)
3. **Apply the focus indicator globally.** Single rule in your global stylesheet covers every interactive element on every screen. (2 min — affects whole app, multiplies value)

The remaining minors can ship in a follow-up — none block.

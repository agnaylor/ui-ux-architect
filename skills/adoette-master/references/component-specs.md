# Component Specifications & Micro-Interactions

> Behavior, timing, and state details for the components that show up in every project.

## Floating Menus & Context Toolbars

### Trigger
- Text selection, long-press, or hover over a designated boundary.
- Never on page load. Never visible by default.

### Placement
- Centered 8px above or below the active element / cursor.
- Auto-flip if it approaches viewport edge.

### Dismissal
- Click outside → fade out (150ms).
- `Escape` key → instant destroy, return focus to parent container.

### Code Pattern (React/TS)
```tsx
useEffect(() => {
  const handleKey = (e: KeyboardEvent) => e.key === 'Escape' && setOpen(false);
  const handleClickOutside = (e: MouseEvent) => {
    if (ref.current && !ref.current.contains(e.target as Node)) setOpen(false);
  };
  document.addEventListener('keydown', handleKey);
  document.addEventListener('mousedown', handleClickOutside);
  return () => {
    document.removeEventListener('keydown', handleKey);
    document.removeEventListener('mousedown', handleClickOutside);
  };
}, []);
```

---

## Progressive Disclosure Drawers & Accordions

### Structure
- Collapsed state: clean summary header only.
- Header itself is the trigger button (whole row clickable).
- Chevron icon rotates 180° on expand.

### Timing
- Total expand/collapse: 150–200ms.
- Easing: `ease-out` cubic-bezier.
- Anything slower feels sluggish. Anything faster feels jarring.

---

## Interactive States (Every Button, Input, Card)

| State | Visual Treatment |
|---|---|
| Default | Flat, structural palette |
| Hover (desktop) | 5% background tint OR `box-shadow: 0 8px 32px rgba(44,47,51,0.08)` |
| Active/Pressed | `transform: scale(0.98)` for 100ms |
| Focus (keyboard) | 2px Blue Agave outline at 2px offset |
| Disabled | `opacity: 0.4; cursor: not-allowed; filter: saturate(0);` |

---

## Completion Feedback (Peak-End Rule)

### Snackbar Spec
- Position: bottom-center on mobile, bottom-right on desktop.
- Auto-dismiss: 3 seconds.
- Fade timing: 200ms in, 300ms out.
- Background: Chimney Smoke. Text: Linen. Optional icon.

### Forbidden
- Modal pop-ups that block the UI for "Saved!" or "Synced!" confirmations.
- Confetti, balloon, or celebration animations (unless explicitly requested for a casual surface).
- Full-screen success overlays for non-irreversible actions.

---

## Form Inputs

### Layout
- Label above input. Never inside (placeholder ≠ label).
- 8px gap between label and input.
- 24px gap between input groups.

### States
- Default: 1px hairline border, Linen background, 4px radius.
- Focus: Blue Agave border, Warm Ash background.
- Error: High-Contrast Crimson border, inline error text below (12px, error color).
- Disabled: Standard disabled state.

### Validation Timing
- Validate on blur, not on every keystroke (premature criticism).
- Re-validate on next change after first error.

---

## Cards

### Resting
```css
background: var(--bg-primary);   /* Linen */
border-radius: 8px;
box-shadow: var(--shadow-rest);
padding: 24px;
```

### Hover (if interactive)
```css
box-shadow: var(--shadow-hover);
transform: translateY(-1px);
transition: all var(--motion-default) var(--motion-ease);
```

---

## Navigation Patterns

### Sidebar (Desktop)
- 240px width default, collapse to 64px (icon-only) on demand.
- Active item: Blue Agave 4px left border + Warm Ash background.
- No nested menus deeper than 2 levels.

### Tab Bar (Mobile)
- Fixed bottom. Max 5 items. Center item can be a FAB.
- Each tab ≥ 44×44px touch target.
- Active tab: Blue Agave icon + label.

### Breadcrumbs (Wiki/Dashboard)
- Herringbone Gray text, Chimney Smoke for the current page.
- Separator: `/` with 8px margin.
- Truncate middle items on narrow viewports, never the current page.

# Example Output: ui-component-generation

> Reference for what a finished component delivery looks like. Notice: assumptions stated up front, tokens by name, all states, usage example, token map.

---

## Request
> "Build me a StatusBadge for the cluster dashboard — needs to show ok/warn/error states."

## Assumptions
- **Platform:** Dashboard.
- **States required:** Default × 3 variants (ok/warn/error). No loading or empty (badge always has a status).
- **Data contract:** `status: 'ok' | 'warn' | 'error'`, optional `label?: string`, optional `count?: number`.

---

## Files

### `StatusBadge.tsx`
```tsx
import { HTMLAttributes } from 'react';
import styles from './StatusBadge.module.css';

export type StatusBadgeStatus = 'ok' | 'warn' | 'error';

interface StatusBadgeProps extends HTMLAttributes<HTMLSpanElement> {
  status: StatusBadgeStatus;
  label?: string;
  count?: number;
}

const STATUS_COPY: Record<StatusBadgeStatus, string> = {
  ok: 'Optimal',
  warn: 'Warning',
  error: 'Critical',
};

export function StatusBadge({
  status,
  label,
  count,
  className,
  ...rest
}: StatusBadgeProps) {
  const displayLabel = label ?? STATUS_COPY[status];
  return (
    <span
      className={`${styles.badge} ${styles[status]} ${className ?? ''}`}
      role="status"
      aria-label={`${displayLabel}${count !== undefined ? `: ${count}` : ''}`}
      {...rest}
    >
      <span className={styles.dot} aria-hidden />
      <span className={styles.text}>{displayLabel}</span>
      {count !== undefined && <span className={styles.count}>{count}</span>}
    </span>
  );
}
```

### `StatusBadge.module.css`
```css
/* Modern Architect tokens — see reference/design-tokens.md */
.badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 4px 12px;          /* 4px sub-component, 12px is off-grid — see note */
  border-radius: 4px;
  font-size: 12px;
  font-weight: 500;
  line-height: 1.5;
  background: var(--bg-secondary);  /* Warm Ash */
  color: var(--text-primary);       /* Chimney Smoke */
  transition: background var(--motion-default) var(--motion-ease);
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
}

.text {
  font-variant: small-caps;
  letter-spacing: 0.02em;
}

.count {
  margin-left: 8px;
  padding-left: 8px;
  border-left: 1px solid var(--border-hairline);
  font-variant-numeric: tabular-nums;
}

/* Status variants — dot color only, badge stays neutral */
.ok    .dot { background: var(--status-ok); }     /* Soft Emerald */
.warn  .dot { background: var(--status-warn); }   /* Soft Amber */
.error .dot { background: var(--status-error); }  /* High-Contrast Crimson */
```

> **Note on the 12px:** sub-component padding for badge horizontals. 8px feels cramped at 12px font; 16px feels chunky. The 8pt grid permits 4px increments for inline elements (icons, badges, dots) per `design-tokens.md`. Documented intentional exception.

### `index.ts`
```ts
export { StatusBadge } from './StatusBadge';
export type { StatusBadgeStatus } from './StatusBadge';
```

---

## Usage

```tsx
import { StatusBadge } from '@/components/StatusBadge';

<StatusBadge status="ok" />
<StatusBadge status="warn" label="High temp" count={3} />
<StatusBadge status="error" label="Throttling" />
```

---

## Token Map

| Token | Used For |
|---|---|
| `--bg-secondary` (Warm Ash) | Badge background — keeps it visually quiet next to data |
| `--text-primary` (Chimney Smoke) | Label text — full readability |
| `--status-ok / warn / error` | Status dot color — the *only* place color carries semantic weight |
| `--border-hairline` | Vertical divider before the count |
| `--motion-default / ease` | Smooth background transitions if parent re-styles on hover |

## States Delivered

- ✓ Three semantic variants (ok / warn / error)
- ✓ Optional count display with tabular-nums alignment
- ✓ Accessible via `role="status"` and `aria-label`
- N/A Loading / Empty / Error states (badges have no data dependency)
- N/A Hover / Active / Disabled (badges are display-only, not interactive)

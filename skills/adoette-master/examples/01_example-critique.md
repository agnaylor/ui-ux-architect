# Example Output: ui-design-critique

> Reference for what a finished critique looks like. The Architect should match this voice, structure, and citation density.

---

## Critique: GPU Cluster Monitoring Dashboard v2
**Platform:** Dashboard
**Overall:** Ships with 2 blockers. Hierarchy is buried under decorative color and competing CTAs. Snap to grid, demote the rainbow gauges, and this is 80% there.

### Blockers (2)

**[BLOCKER] Body text fails WCAG AA on warning panels.**
- Where: `.warning-card` uses Herringbone Gray `#73777B` on Soft Amber `#C9A66B` → contrast 2.1:1.
- Fix: Switch body text to Chimney Smoke `#2C2F33` on the same amber → 8.4:1. Reserve Herringbone Gray for body text on Linen or Warm Ash only.
- Citation: `design-tokens.md` → contrast minimums.

**[BLOCKER] No empty state for the "Active Jobs" panel.**
- Where: When 0 jobs are running, the panel shows literal `"No data"` text on a blank Warm Ash card.
- Fix: Render a primary `Blue Agave` CTA: `Schedule a job`. Body copy above: `No jobs running.` See `copy-bank.md` → Empty States.
- Citation: `UI_UX_Resilience_and_State_Handling.md` → empty state rules.

### Major (4)

**[MAJOR] Five primary CTAs visible in the hero (Hick's Law violation).**
- Where: `Run`, `Pause`, `Stop`, `Export`, `Settings` all share Blue Agave styling.
- Fix: Only `Run sweep` stays primary. Demote `Pause` and `Stop` to ghost buttons. Move `Export` and `Settings` into an overflow menu (kebab icon, top-right of the hero).

**[MAJOR] Rainbow chart for GPU thermal data.**
- Where: Bar chart uses 8 distinct hues for 8 GPUs.
- Fix: Use a single hue (Blue Agave) with varying opacity, OR map color strictly to status (Soft Emerald = optimal, Soft Amber = warm, Crimson = throttling). Citation: `platform-blueprints.md` → Color Strategy for Alerts.

**[MAJOR] Modal pop-up on "Job complete."**
- Where: Modal blocks the dashboard until dismissed.
- Fix: Snackbar at bottom-right, 3-second auto-dismiss. Copy: `Sweep complete. 47 entries logged.` (`copy-bank.md` → Snackbar Messages).

**[MAJOR] Card padding is 20px throughout.**
- Where: `.card { padding: 20px }`.
- Fix: Snap to 24px (next 8pt grid value up). Or 16px if you need density.

### Minor (3)

**[MINOR] Border around every module.**
- Where: `border: 1px solid #ccc` on every panel.
- Fix: Remove borders entirely. Use 24px gap (Law of Proximity) to group/separate. If you need a divider, use the hairline `rgba(44,47,51,0.1)`.

**[MINOR] Focus outline is browser default.**
- Where: Tab navigation shows the OS-default focus ring.
- Fix: `outline: 2px solid var(--accent-primary); outline-offset: 2px;` on all interactive elements.

**[MINOR] Hover state missing on dashboard cards.**
- Where: Cards are clickable but show no hover feedback.
- Fix: Add `box-shadow: var(--shadow-hover)` and `transform: translateY(-1px)` with 200ms ease-out transition.

### Nits (1)

**[NIT] "Run sweep" button could be "Run cluster sweep" for clarity in this context.**
- Subjective preference. Current label is fine if "sweep" is established vocabulary for this team.

### Quick Wins (Top 3, ~30 min total)

1. **Fix the two blockers.** Contrast swap + add the empty state with proper CTA. (15 min)
2. **Demote four of five CTAs.** Only `Run sweep` stays primary; rest go ghost or move to overflow menu. (10 min)
3. **Replace modal with snackbar.** One file change, immediate Peak-End upgrade. (5 min)

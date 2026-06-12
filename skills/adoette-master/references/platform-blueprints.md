# Platform Blueprints

> Pick exactly one blueprint before designing. Each platform has its own constraints.

## 1. Data-Dense Dashboards & Control Panels

### Information Hierarchy
- **80/20 Rule:** Hero view holds the critical 20% of metrics. The rest is hidden behind progressive disclosure (tabs, expandable modules, drill-downs).
- **Grid:** Strict 12-column fluid grid.
- **Separation:** Use whitespace (16–24px padding). No visible borders between modules.

### Color Strategy
- Backgrounds: muted neutral (Warm Ash / Linen panels).
- Status indicators only — never decorative color.
  - Optimal: Soft Emerald
  - Warning: Soft Amber
  - Critical: High-Contrast Crimson
- Text contrast ≥ 4.5:1 (WCAG AA).

### Killer Anti-Patterns
- Rainbow charts for non-categorical data.
- Heavy borders boxing every widget.
- KPIs the same size as supporting metrics.

---

## 2. Mobile & Web Applications

### Touch Architecture
- Every interactive target ≥ 44×44px (regardless of visual icon size).
- Primary actions live in the **lower two-thirds** of the viewport (thumb zone).
- Destructive actions get a confirmation step — never a single tap.

### Gestures & Flows
- Swipe-down to dismiss modals/drawers.
- Pull-to-refresh on list views.
- Floating action components that appear on selection or scroll-up. No giant static headers/footers.

### Responsive Breakpoints
- Mobile: ≤ 640px
- Tablet: 641–1024px
- Desktop: ≥ 1025px
- Test at all three. Don't ship "desktop only" without justification.

---

## 3. Wikis, Notebooks & Knowledge Bases

### Typography
- Reading container: **650–750px max width** (60–75 chars/line).
- One sans-serif family. Hierarchy via weight + scale.
- Body line-height: 1.6.
- Scale: 14 / 18 / 24 / 32px.

### Navigation
- Floating in-line controls on text selection or empty-line hover.
- Persistent but faint Table of Contents in the side margin.
- TOC highlights current section dynamically as user scrolls.

### Killer Anti-Patterns
- Full-width body text on 4K monitors.
- Fixed top nav that eats 80px of vertical space.
- Heavy block borders around every code snippet.

---

## 4. Desktop Utilities & AEC Plugins

### Minimal Native Surface
- Use the platform's native window chrome. Don't reinvent it.
- Linen background, Chimney Smoke text — **but defer to host app theme tokens** when the plugin lives inside ArchiCAD, Bluebeam, Revit, or AutoCAD.
- Single primary action per surface. Maximum two secondary actions.
- Disable resize handles for fixed-function tool windows; allow resize for data-table or list views.

---

### Standalone Desktop Utilities

For Python + PyQt/PySide, Tauri + Rust, or .NET utilities that **don't live inside a host AEC app**, apply the full Modern Architect aesthetic — Linen, Chimney Smoke, Blue Agave. These behave like mobile/web apps in spirit, scaled for keyboard + mouse.

- **Window minimum:** 720×480px. Anything smaller cramps the 8pt grid.
- **Window default:** 960×640px.
- **Title bar:** Native OS (don't custom-draw unless you're shipping a frosted-glass Tauri app).
- **Menu bar:** Use it. Hide secondary commands here, not on the canvas.
- **Status bar:** Persistent at bottom — current state in one line, no marquees.

---

### AEC Plugin Architecture (ArchiCAD, Bluebeam, Revit, AutoCAD)

When the plugin is **embedded inside a host AEC app**, your UI is a guest in their house. Native look-and-feel beats brand consistency.

#### A. Host-App Theming Rules

| Host | UI Framework | Theming Source |
|---|---|---|
| ArchiCAD | DG (Dialog Manager) API for native dialogs; WPF for richer panels | Read host theme via `ACAPI_View_ActivateBackgroundTheme`; fall back to neutral grays |
| Revit | WPF (preferred) or WinForms | Adopt Revit's ribbon color, panel background `#F0F0F0` light / `#2D2D30` dark |
| Bluebeam | WPF + custom controls via Studio API | Match Bluebeam's blue accent (`#2D7CC4`) for selected states — do NOT override with Blue Agave |
| AutoCAD | .NET API + Palette Sets | Honor `Application.GetSystemVariable("COLORTHEME")` (0 = dark, 1 = light) |

**Rule:** Read the host theme on plugin load. Never hard-code colors that fight the host UI. Your custom palette only applies when the user opens a **standalone window** the plugin spawns (e.g., a config dialog).

#### B. Ribbon UI Conventions (Revit + AutoCAD)

If your plugin contributes to the host's ribbon:

- **Tab name:** One word if possible. Two max. Title Case.
- **Panel grouping:** Group commands by user goal, not by your internal code structure.
- **Button hierarchy:**
  - Large (32×32px icon + 2-line label): primary commands, max 3 per panel
  - Small (16×16px icon + inline label): everything else
- **Icons:** 32px and 16px versions required. SVG source, exported to PNG. Match host icon style (flat in Revit, slightly outlined in AutoCAD).
- **Tooltips on ribbon buttons:** Allowed and expected (this is the one place the no-tooltip rule bends — host convention wins).
- **Modeless panels:** Default to dockable. Users will move them. Persist position to `%AppData%\YourPlugin\layout.xml`.

#### C. WPF Patterns (Revit, Bluebeam, AutoCAD)

```csharp
// Window shell — always inherit from host
public partial class PluginWindow : Window
{
    public PluginWindow()
    {
        InitializeComponent();
        // Force same DPI as host
        this.UseLayoutRounding = true;
        this.SnapsToDevicePixels = true;
        // Match host font
        this.FontFamily = SystemFonts.MessageFontFamily;
        this.FontSize = SystemFonts.MessageFontSize;
    }
}
```

- **Layout:** Grid + StackPanel. Avoid Canvas (loses host theming).
- **Data binding:** MVVM. ViewModels never reference Revit/AutoCAD APIs directly — inject through a service layer for testability.
- **Resource dictionaries:** Define your tokens in `App.xaml` so the whole plugin pulls from one source.
- **DPI:** Test at 100%, 150%, 200%. Host apps run on contractor laptops with weird scaling.

#### D. AEC-Specific Interaction Patterns

- **Pick-then-act:** User selects geometry in the host viewport → your panel reflects the selection. Never make them re-pick inside your dialog.
- **Long operations:** Geometry extraction, BIM export, drawing parse can take 30s+. Use a determinate progress bar, not a spinner. Allow cancel.
- **Transactions:** Wrap host-modifying operations in a single transaction (`Transaction` in Revit, `DocumentLock` in AutoCAD). One user click = one undo step.
- **Reversibility:** Every operation that touches the model must be undoable via the host's native Ctrl+Z.

#### E. Distribution & Versioning

- **MSI installer** for IT-managed firms (large architecture offices).
- **Per-user install** for solo practitioners. Drop into `%AppData%\Autodesk\Revit\Addins\2025\` or equivalent.
- **Version pinning:** Every plugin manifest declares the host app version range it supports. Don't ship "works with all versions" — it doesn't.
- **License key surface:** If commercial, show license status in the plugin's About dialog. Not the main canvas.

#### F. Killer Anti-Patterns

- Drawing your own ribbon UI inside the canvas instead of contributing to the host ribbon.
- Hard-coded Blue Agave background that fights ArchiCAD's dark theme.
- Modal "Operation complete" dialog after every action — user has to dismiss to keep working.
- Blocking the host UI thread during geometry processing.
- Custom undo stack that doesn't integrate with the host's Ctrl+Z.

---

### Completion Feedback (Standalone + Plugin)
- **Standalone utilities:** Snackbar at the bottom, fading after 3 seconds.
- **AEC plugins:** Status bar update + log entry. NO snackbar (it fights the host UI's own notification surface).
- Never a modal pop-up for "Sweep complete" / "Export done" / "Sync finished."
- Persist a log entry the user can review later (file path shown in About → Logs).

---

## Decision Flowchart

```
Is the surface for monitoring system state?       → Dashboard
Is it a phone-first or thumb-first experience?    → Mobile/Web
Is it primarily text/long-form reading?           → Wiki/Notebook
Is it a plugin or tool inside another desktop app?→ Desktop/AEC
```

If two apply (e.g., a mobile dashboard), the **input modality wins** — mobile blueprint governs touch + thumb zone, dashboard blueprint governs data density.

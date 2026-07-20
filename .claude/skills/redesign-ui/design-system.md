# Redesign UI — Design System

Concrete, non-negotiable values for the SaaS redesign. Copy these verbatim so every run
produces a consistent result. Colors preserve the existing slate/gray + blue language.

## Design tokens (`:root`)

Add this block near the top of the global (unscoped) `<style>` in `client/src/App.vue`, then
refactor hardcoded literals to `var(--…)`.

```css
:root {
  /* Surfaces */
  --color-app-bg: #f8fafc;
  --color-surface: #ffffff;
  --color-surface-muted: #f1f5f9;

  /* Borders */
  --color-border: #e2e8f0;
  --color-border-strong: #cbd5e1;

  /* Text */
  --color-text: #0f172a;
  --color-text-secondary: #475569;
  --color-text-muted: #64748b;
  --color-text-inverse: #f8fafc;

  /* Brand / accent */
  --color-brand: #2563eb;
  --color-brand-hover: #1d4ed8;
  --color-brand-soft: #eff6ff;
  --color-focus-ring: #3b82f6;

  /* Semantic */
  --color-success: #059669;
  --color-info: #2563eb;
  --color-warning: #ea580c;
  --color-danger: #dc2626;

  /* Sidebar (dark slate) */
  --sidebar-width: 248px;
  --sidebar-width-collapsed: 68px;
  --sidebar-bg: #0f172a;
  --sidebar-text: #cbd5e1;
  --sidebar-text-active: #ffffff;
  --sidebar-item-active-bg: rgba(37, 99, 235, 0.18);
  --sidebar-item-hover-bg: rgba(148, 163, 184, 0.12);

  /* Spacing scale */
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-5: 1.25rem;
  --space-6: 1.5rem;
  --space-8: 2rem;

  /* Radii */
  --radius-sm: 6px;   /* buttons, badges, selects */
  --radius-md: 10px;  /* cards */
  --radius-lg: 14px;

  /* Shadows */
  --shadow-sm: 0 1px 2px rgba(15, 23, 42, 0.06);
  --shadow-md: 0 4px 12px rgba(15, 23, 42, 0.08);

  /* Typography */
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;

  /* Layout */
  --content-max-width: 1600px;
  --topbar-height: 64px;
}
```

## Sidebar spec

- Fixed left column, full viewport height, `width: var(--sidebar-width)`, `background: var(--sidebar-bg)`.
- Vertical stack: logo block at top → nav links (vertical) → spacer → `LanguageSwitcher` +
  `ProfileMenu` pinned to the bottom.
- Nav items: full-width, `padding: var(--space-3) var(--space-4)`, `border-radius: var(--radius-sm)`,
  `color: var(--sidebar-text)`, gap between icon/label. Hover → `--sidebar-item-hover-bg`.
  Active (`$route.path` match) → `--sidebar-item-active-bg` + `--sidebar-text-active` + a 3px
  left accent bar in `--color-brand`. Keep the existing manual active-state logic.
- No emojis; use text labels (icons optional only if the repo already ships an icon set).

## App layout

- `.app` becomes a two-column layout: `display: flex;` with the sidebar as a fixed-width flex
  child and a scrollable `.content` region (`flex: 1; min-width: 0;`) holding `FilterBar` +
  `<main class="main-content">`.
- Remove the three duplicated `max-width: 1600px; margin: 0 auto` blocks
  (`.nav-container`, `.filters-container`, `.main-content`). Center content once inside
  `.main-content` using `max-width: var(--content-max-width); margin: 0 auto;`.
- `FilterBar` sticky offset changes from `top: 70px` to `top: 0` (it now sits at the top of the
  scrollable content column, not under a top nav).

## Spacing & polish conventions

- Page padding: `var(--space-6) var(--space-8)`.
- `.page-header`: `margin-bottom: var(--space-6)`; title uses `--color-text`, subtitle `--color-text-muted`.
- `.card`: `background: var(--color-surface)`, `border: 1px solid var(--color-border)`,
  `border-radius: var(--radius-md)`, `padding: var(--space-5)`, `box-shadow: var(--shadow-sm)`.
- `.stats-grid`: consistent `gap: var(--space-4)`.
- Tables, badges, buttons: refactor to tokens; keep radii (`--radius-sm`).

## Responsive

- Below 1024px: collapse sidebar to `--sidebar-width-collapsed` (icon/initial only) or a
  toggle-able off-canvas drawer with a hamburger control in a slim top bar. Content column stays
  fluid.

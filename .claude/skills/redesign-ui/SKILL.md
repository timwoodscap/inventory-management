---
name: redesign-ui
description: Redesigns this Vue 3 inventory app's UI into a modern SaaS-style interface with a left vertical navigation sidebar (replacing the top nav bar), CSS design tokens, and consistent spacing. Use this skill when asked to redesign, modernize, or restyle the app's UI, convert the top nav to a sidebar, or give it a polished SaaS look.
---

# Redesign UI — SaaS Sidebar Layout

Transforms the inventory app's current top-nav layout into a modern SaaS interface: a left
vertical navigation sidebar, a token-based design system, and consistent spacing/polish — while
preserving all routing, filters, i18n, and modal behavior.

Read [design-system.md](design-system.md) before making any changes; it holds the exact tokens,
sidebar spec, and layout rules to apply.

## Mandatory tooling rules

- **Every `.vue` create/modify MUST be delegated to the `vue-expert` subagent** (per CLAUDE.md).
  Do not edit `.vue` files directly. Pass `vue-expert` the relevant excerpt of
  [design-system.md](design-system.md) plus the specific step below.
- Run servers with the `/start` skill; stop with `/stop`. Frontend is `http://localhost:3000`,
  API is `http://localhost:8001`.
- **Verify visually with Playwright MCP tools** (`mcp__playwright__*`) against `http://localhost:3000`.
- No emojis in the UI. Preserve i18n `t()` keys. Follow the slate/gray + blue design language.

## Current state (what you're changing)

- Top nav is in [App.vue](client/src/App.vue): `<header class="top-nav">` (sticky, 70px) with
  `.logo`, a horizontal `.nav-tabs` of six `<router-link>`s, `LanguageSwitcher`, and `ProfileMenu`.
- Routes are inline in [main.js](client/src/main.js): `/`, `/inventory`, `/orders`, `/demand`,
  `/spending`, `/reports`.
- No CSS variables exist — colors/spacing are hardcoded across App.vue's global `<style>` block
  and each view's `<style scoped>`.
- [FilterBar.vue](client/src/components/FilterBar.vue) is sticky at `top: 70px`.
- `.nav-container`, `.filters-container`, `.main-content` each repeat `max-width: 1600px; margin: 0 auto`.

## Procedure

1. **Introduce design tokens.** Have `vue-expert` add the `:root` block from
   [design-system.md](design-system.md) to the global style in [App.vue](client/src/App.vue), then
   refactor hardcoded hex/rem literals there to `var(--…)`.

2. **Convert top nav to a sidebar.** In [App.vue](client/src/App.vue), replace
   `<header class="top-nav">` with `<aside class="sidebar">`; change `.app` to the two-column
   flex layout from the design system. Move the logo, the six `<router-link>`s (now vertical),
   `LanguageSwitcher`, and `ProfileMenu` into the sidebar. Keep the existing manual active-state
   logic (`:class="{ active: $route.path === '…' }"`) and all emitted profile/tasks events and modals.

3. **Fix layout coupling.** Remove the three duplicated 1600px-centered containers; center content
   once inside `.main-content`. Update [FilterBar.vue](client/src/components/FilterBar.vue) sticky
   offset from `top: 70px` to `top: 0`.

4. **Apply spacing & polish** per the design system to `.page-header`, `.card`, `.stat-card`,
   `.stats-grid`, tables, and badges (via `vue-expert`).

5. **Responsive behavior.** Add the collapsed/off-canvas sidebar behavior below 1024px.

6. **Verify.** Start servers, then use Playwright MCP to load and screenshot each route
   (`/`, `/inventory`, `/orders`, `/spending`, `/demand`, `/reports`). Confirm the left sidebar
   renders, spacing is consistent, active states work, and the console has no errors.

## Constraints

- Preserve existing routes, global filters, i18n, and modal behavior — this is a visual/layout
  redesign only, not a functional change.
- Keep changes token-driven so the look stays consistent and easy to retheme.

## Files this skill touches

- [client/src/App.vue](client/src/App.vue) — tokens, sidebar, app layout, global styles
- [client/src/components/FilterBar.vue](client/src/components/FilterBar.vue) — sticky offset
- [client/src/views/*.vue](client/src/views) — spacing/polish refactors to tokens
- [client/src/main.js](client/src/main.js) — reference only (routes; usually unchanged)

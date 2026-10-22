# Dashboard configuration and quality checks

Use this reference alongside the app profile. The app brief and recorded decisions are the source of truth. Separate configurable choices from required quality checks. Never turn an unselected option into a defect or silently change a recorded choice.

## Configurable choices

Record selected values, exclusions, decision source and acceptance checks in the app profile. If a material choice is unspecified and cannot be inferred from the existing app, ask the user or offer concise options.

- Audience and density: executive/minimal, executive/analytical, analyst/power user, or specified alternative.
- Theme: light, dark, or dual. For dual, verify all routes/components and the switch or automatic behavior.
- Shell/navigation: fixed or collapsible sidebar; flat, grouped or nested navigation; sticky header; breadcrumbs; tabs; multi-step navigation; scroll model.
- Global controls: search, context filters, notifications, profile/account controls, only when scope and behavior are defined.
- Visual treatment: rounded cards/pills, gradients, subtle glass, shadows/elevation, compact tables, icon-led metrics, semantic colors. Follow the app brand and preserve legibility.
- Interactions: hover states, restrained animation/transitions, tooltips, drilldown modal/drawer, scenario sliders, toasts, skeletons, counters, expandable panels, empty/error states, export/print. Each selected element must have a real purpose and observable behavior; respect reduced motion.
- Chart families: KPI/sparklines, trends/forecasts, waterfall/PVM, heatmap/matrix, scatter/bubble, treemap, ranked opportunity table, what-if, map, Sankey/process, hierarchy/tree, comparison/variance. Select for the business question and available data, not variety.
- Signature interaction: if specified, name the primary action, user input, visible response and resulting state. Verify it every round.

A missing optional feature is not a defect unless the brief, profile or user journey requires it. Changing a selected option without approval is a scope/configuration regression.

## Required checks

### Copy and content
- Use concise, natural, professional copy and sentence case unless the app specifies otherwise. Keep terminology, spelling, capitalization, dates, currencies, units and labels consistent.
- Remove AI-like/decorative punctuation from user-facing text: em dashes, em dots/middle dots, decorative arrows and ornamental separators. Use ordinary punctuation.
- Remove filler, repeated boilerplate, TODOs, fake links, unfinished labels and internal implementation terms such as mock, seed, placeholder, adapter, backend or prototype unless explicitly required.
- Never trim, line-clamp, clip or truncate important text. Allow wrapping or provide an obvious accessible way to reveal the full value. Do not rely on hover alone for critical information.
- Do not claim data is live, verified, current, complete or approved without evidence. Disclose illustrative data clearly and keep it realistic and internally coherent.

### Layout and visual consistency
- Respect the recorded density. Compact cards by removing accidental whitespace, excessive padding, oversized headers/cards, needless stacking and narrow columns without sacrificing readability. Keep peer cards consistent and show metric, value, unit, period and essential context.
- Use existing design tokens and shared components. Check hierarchy, typography, pill/button sizing, spacing, status colors and icon alignment.
- Fix overflow, clipping, overlap, awkward wrapping, fixed-height cropping, hidden actions, unintended page-wide horizontal scroll and accidental nested scroll. Use intentional reflow and scrolling.
- Check dialogs, drawers, menus, dropdowns, sticky elements and tooltips for layering, positioning, focus, scroll and action visibility. Verify all configured themes.

### Tables and controls
- Enable functional sorting on every data table unless explicitly excluded. Show sort state and sort text, numbers, dates and currency by type. Verify direction toggles and sorted rows, not just header appearance.
- Sorting, filtering, search and pagination must operate on displayed data and keep counts/totals accurate. Keep headers and important cell text readable. Make row actions target the correct row.
- Every visible control must work as labeled. Filters update all relevant cards, charts, tables, counts and scope labels; dependent filters cascade. Selected values remain available; zero-count options are handled deliberately.
- Search returns relevant results and can be cleared. Keep active scope visible. Handle reset, invalid URL parameters and deep links so URL and rendered view agree.
- Preserve unrelated route/query/open-record/unsaved state. Do not show actions a role cannot perform; enforce permissions in the action path. Provide clear loading, success and failure feedback.

### Data and charts
- Preserve approved figures, definitions, formulas, units, date windows, sources and scope. Never substitute another segment/geography/period or invent figures, records, rules, citations or links.
- Reconcile metrics, totals, counts, dates, labels, units, statuses, owners and next actions across overview, pages, cards, charts, tables and drilldowns. Counts must match the records they claim to count.
- Distinguish zero, missing, unavailable, suppressed, not applicable and not calculated. Never use unrelated fallback values.
- Provide period, unit, scope and comparison basis where needed; explain important calculations and assumptions.
- Charts fit and show accurate titles, axes, units, time ranges, legends, values and tooltips. Values reconcile with related views; filters affect charts; click-throughs lead to the correct details. Avoid misleading scales and unsupported precision.
- Natural-language/AI features, if present, must use the user's input and current scope, distinguish fact from interpretation, explain failures and never imply a suggested action was executed.

### States, accessibility and implementation
- Provide useful loading, empty, unavailable, validation, permission-denied, success and error states. Fix endless skeletons, blank panels, raw errors and empty shells.
- Check keyboard focus/order and operation, accessible names for inputs/icon-only controls, contrast, wrapping and touch targets. Do not rely on color, hover or icons alone. Overlays dismiss without layout shifts or lost state. Respect reduced motion.
- Follow the repository's framework, architecture, conventions, lint and test setup. Reuse shared components; fix shared defects at source and test all uses. Avoid unnecessary dependencies, duplicate state, hardcoded values, unrelated refactors, debug output, dead code and sensitive client-side data.
- Check console errors, failed requests, broken assets, dead links, stale status/date text and route failures where possible.

## Verification

Inspect the actual preview/deployed app and latest export when available; confirm versions. A success message is not proof. Check all relevant routes, controls, shared components, personas, themes and representative desktop/tablet/phone widths. Test primary journeys and reconcile key data. Mark every applicable item Pass, Fix required, Not applicable or Not verified. Missing evidence is not a pass. Report what was checked, fixed, open and inaccessible.

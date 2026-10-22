# Dashboard standards for Lovable

Follow this app's approved brief, architecture, brand, data definitions and decisions. They are the source of truth.

## Choices to record, not universal defaults
Record audience/density (executive-minimal, executive-analytical, analyst/power user); theme (light/dark/dual); shell/navigation (fixed/collapsible sidebar, grouping, sticky header, breadcrumbs, tabs, steps, scroll); global controls (search, filters, notifications, profile); visual options (rounded cards, gradients, glass, shadows, compact tables, icon metrics, semantic colors); interactions (tooltips, drilldowns, restrained animation, sliders, toasts, skeletons, counters, expanders, export/print); chart families (KPI, trend/forecast, waterfall/PVM, heatmap, scatter, treemap, ranked table, what-if, map, Sankey, hierarchy, variance); and the signature interaction. Choose only what supports the user and data. Record exclusions, decision source and acceptance checks. Never add an unselected option by inference.

## Required quality rules
- Use concise natural copy. Remove AI-like punctuation (em dashes, middle dots, decorative arrows), filler, TODOs, fake links and unwanted internal terms. Keep terminology, dates, units and labels consistent.
- Never trim, line-clamp, clip or truncate important text. Wrap it or provide an accessible way to reveal it.
- Keep cards compact but readable; remove accidental whitespace, oversized padding/cards and unnecessary stacking. Preserve hierarchy and show metric, value, unit, period and context.
- Follow existing tokens and components. Fix overflow, overlap, fixed-height cropping, accidental nested scroll and unintended horizontal page scroll. Reflow at supported widths.
- Make every table sortable unless explicitly excluded. Sort by data type, show sort state, and verify actual rows reorder. Filters, search and pagination must work and counts must reconcile.
- Every visible control works as labeled. Filters cascade to relevant cards/charts/tables/counts; search works; scope is visible; URL and rendered state agree. Preserve unrelated state and enforce role permissions in action paths.
- Preserve approved figures, definitions, formulas, units, date windows and scope. Reconcile cards, charts, tables and drilldowns. Distinguish zero from missing/unavailable. Do not invent data or use unrelated fallbacks.
- Charts fit and show accurate labels, axes, units, periods, legends and tooltips. Values reconcile; filters apply; click-throughs work.
- Provide loading, empty, unavailable, validation, denied, success and error states as relevant. Avoid endless skeletons, blank panels and raw errors.
- Check keyboard/focus, accessible names, contrast, touch targets, overlays and reduced motion. Follow existing code conventions; avoid unnecessary dependencies, dead code, debug output or sensitive client data.
- Test actual preview/deployment, affected routes, roles, themes, widths, controls and workflows. Check console/network, broken links/assets, overflow and regressions. Mark each item Pass, Fix required, N/A or Not verified. Missing evidence is not a pass.

# Quantzig Deck — Slide Type Catalog

Nine reusable **content** patterns, all present in `assets/quantzig-deck-template.pptx` (`slide1.xml`–`slide10.xml`). These are shape-level patterns (cards, tables, bar charts) that sit on top of a layout — they are not the same thing as the master/layout system itself. **Read `master-and-layouts.md` first** to pick the right layout (8 of the 9 patterns below sit on layout 7, "Header Ribbon"); this file catalogs what goes inside that chrome.

For any new deck, pick the closest-matching type(s) below, duplicate that slide with `add_slide.py`, then edit content in place — don't build these from scratch.

Run `python scripts/thumbnail.py assets/quantzig-deck-template.pptx template-thumbs` first to see them visually before picking.

## 1. Cover / title slide — `slide1.xml` (layout 1, "Title Slide")
Big title (36pt) + subtitle (20pt) + date, left-aligned in the lower-third of the slide. The background band and large white logo+tagline lockup are **not** a live gradient — they're a raster image and an SVG lockup baked into the layout (see style-guide's "Signature gradients" correction).
**Swap:** title, subtitle, date only. Don't touch the background image or logo — they're inherited from layout 1.

## 2. Landscape & vision (problem/solution split) — `slide2.xml`
Gradient header bar (title + kicker). Below it: an intro sentence, then two side-by-side cards — "Current Fragmentation & Pain Points" (left, 5 bold-lead-in bullets) and "Vision for [Product]" (right, 5 bold-lead-in bullets) — plus a large decorative "The Solution" radial graphic (a ~150-shape starburst with 5 feature labels — see "Complex decorative graphics" in style-guide.md before touching it).
**Use for:** problem statement / current-state vs future-state slides, any "why this project" opener.
**Swap:** header title/kicker, intro sentence, the two 5-bullet lists (keep the bold-lead-in + continuation pattern). For the solution graphic, only touch the 5 "Feature N" text labels — duplicate the whole group rather than redrawing it, or substitute a simple icon if the radial motif doesn't fit.

## 3. Phased-release table + key deliverables — `slide3.xml`
Gradient header bar. Intro sentence. A 4-column table (`Release | Timeline | High-Priority Focus | Mid-Priority Add-Ons`) with one row per phase — header row bold on gradient/dark fill. Below the table, a "Release 1 | Key Deliverables" strip with 4 short highlighted mini-cards arranged **2×2** (two ~6"-wide cards per row, two rows) — not 4 across.
**Use for:** phased delivery plans, roadmap summaries.
**Swap:** table rows (add/remove releases freely — it's a plain table, not an image), the 4 key-deliverable mini-cards.

## 4. Feature scope grid (by release) — `slide4.xml`
Gradient header bar. Three columns, one per release, each with a colored release-label pill ("Release 1 | Weeks 1–12 | MVP") and a stack of feature cards (bold feature name + 1–2 line description) underneath.
**Use for:** detailed feature/scope breakdowns split across phases or workstreams.
**Swap:** column count matches your number of phases/workstreams (3 is typical but not fixed); each card's title + description.

## 5. Architecture diagram — `slide5.xml`
Gradient header bar. Left/main area holds a technical architecture diagram. Below or beside it, a "Key Design Considerations" bullet list (bold-lead-in pattern, 3–4 points). **Correction from an earlier pass of this skill:** the diagram is *not* simple boxes-and-arrows — most components are groups of freeform vector paths (flattened icon art, e.g. database/server/cloud icons) with text labels layered on top, plus one embedded raster logo. See "Complex decorative graphics" in style-guide.md before committing to reusing this slide as-is.
**Use for:** any technical architecture, data-flow, or system-design slide.
**Swap:** reuse individual icon groups where the same component recurs (e.g. a "Databricks" icon) and swap labels; for anything structurally different, budget real time to redraw connectors/icons. This is the most labor-intensive slide to adapt — don't treat it as a quick text swap.

## 6/7. Sample screens (product screenshots) — `slide6.xml`, `slide7.xml`
Gradient header bar with a one-line kicker describing which screens are shown. 2–3 screenshot images laid out side by side. Every image gets a thin hairline border (`bg1 @ 85%`); when a slide pairs a primary screenshot with a smaller supporting one near its corner (grouped together), the primary image additionally gets a soft drop shadow — the smaller overlay doesn't.
**Use for:** showing product UI, mockups, or screen flows. Use two slides (as the template does) if you have more than ~3 screens to show — don't cram more than 3 images on one slide.
**Swap:** replace the images (`add_picture` in python-pptx, or swap the `r:embed` target in the slide XML + media part) and the kicker line. Keep the hairline border on any new image you add.

## 8. Gantt/execution timeline — `slide8.xml` (multi-month, high-level) and `slide9.xml` (single-release, week-by-week, with a key-deliverables side panel)
Gradient header bar. A table where the first two columns are `# | Activity` (or `Sl | Task`) and the remaining columns are time buckets (months or weeks). Section-header rows (e.g. "Release 1: MVP") span the full width with a darker fill. Active-duration cells are filled with the wine-navy gradient to form the bar; inactive cells stay blank/white.
**Use for:** project timelines, delivery roadmaps, sprint plans.
**Swap:** row labels and which cells get the gradient fill (i.e., redraw the bars for the new schedule). Keep section-header rows for grouping if you have more than ~4 activities.
Note `slide9.xml` also shows the pattern for pairing a timeline table with a "Key Deliverables" side panel reused verbatim from slide 3 — a good option when you want the timeline and the deliverables recap on one slide.

## 9. Resourcing & costing table — `slide10.xml`
Single full-width table: `# | Role | [Phase columns...] | Cost/Hr`, one row per role, headcount per phase, hourly rate in the last column, with a bold "Total Headcount" summary row at the bottom.
**Use for:** staffing plans, cost breakdowns, resourcing asks.
**Swap:** roles, per-phase headcount, rates — straightforward row edits.

---

## Notes on the example slides after the font and colour clean-up

- Every example slide now uses Grandview, and slide 5's zones use brand colours.
- **Slide 5 (architecture)** still carries some 8pt component labels, left as they are because raising them in place wraps the labels. When you reuse it, raise every label to 10pt and widen its box, or rebuild the diagram; `scripts/deck_check.py` flags anything under 10pt.
- **Slides 6 and 7 (sample screens)** carry almost no copy in the template. On a real deck each screen needs 2 to 4 numbered callouts with a one-sentence explanation each, and a short "what you are looking at" line, so the slide reads without a voice-over.

## General adaptation rules (apply to all types)

- Duplicate with `scripts/add_slide.py`, never copy a slide file by hand.
- Do all structural work (add/delete/reorder slides) before editing any slide's text content.
- When replacing table rows or bullet lists, copy the sibling `<a:pPr>`/`<a:tcPr>` from an existing row so gradient fills, banding, and spacing carry over — don't rebuild formatting from scratch.
- If a new deck needs more or fewer columns/rows than the template slide has, add/remove them explicitly (update `<a:tblGrid>` for tables) rather than leaving empty or overflowing cells.
- Keep the gradient header bar, footer, logo, and page number untouched on every slide — they're inherited from the master/layout (see `master-and-layouts.md`), not something you redraw per slide.
- Run `scripts/office/validate.py out.pptx --original assets/quantzig-deck-template.pptx` and the visual QA pass (see main pptx skill) before calling a deck done.

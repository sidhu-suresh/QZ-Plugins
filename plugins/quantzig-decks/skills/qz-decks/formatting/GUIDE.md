# Formatting Guide (Quantzig brand)

Part of the qz-decks skill. Paths in this file (`references/...`, `assets/...`) are relative to the `formatting/` folder. `scripts/thumbnail.py`, `scripts/add_slide.py`, `scripts/clean.py`, and `scripts/office/validate.py` belong to the pptx skill.

This guide packages the visual identity, the real slide master, and the slide-content patterns from a real, delivered Quantzig client deck (`Formulary IQ — Implementation Plan`, built for Amgen) so future decks look consistent without rebuilding the style from scratch each time. This is an editing-a-template workflow, not a from-scratch pptxgenjs build — always start from `assets/quantzig-deck-template.pptx`, and always build new slides through its master/layout system rather than recreating chrome by hand.

**Read the base `pptx` skill first** for the mechanics (thumbnail → add_slide.py → edit XML → clean.py → zip → validate → visual QA). This guide only adds Quantzig-specific style rules, the master/layout catalog, the content-pattern catalog, and a QA/validation pass hardened by real production fixes — it doesn't replace the general pptx editing workflow.

## Read these references in order

1. **`references/master-and-layouts.md`** — the master + all 12 layouts, preserved as-is. This is how logo, footer, and header chrome actually get onto a slide: by picking the right layout and letting it inherit, never by hand-placing a logo image or redrawing a header bar. Read this before creating any new slide.
2. **`references/style-guide.md`** — colors (including the theme-color mapping), typography, writing voice, and the content-shape conventions (how text sits inside shapes, table/image treatment, which decorative graphics to reuse as a block rather than redraw). Read this before styling or drafting any content.
3. **`references/slide-types.md`** — nine ready-to-duplicate content patterns that sit on top of the layouts (cards, tables, bar charts). Read this when picking what goes inside the slide you just created.
4. **This file's "Common Pitfalls" and "Slide-by-Slide Validation Pass" sections below** — read before any final QA round. They document failure modes discovered while shipping a real 35-slide client deck through multiple edit rounds, and the checks that catch them.

## Assets bundled with this skill

- `assets/quantzig-deck-template.pptx` — the full source deck: master, all 12 layouts, and the 10 example slides, with the theme's accent colors updated to match the real brand palette (see style-guide.md). Nothing else was changed — don't extract logo/footer images out of it; build new slides against its layouts instead.
- `scripts/deck_check.py` — the automated brand, density and variety sweep (Validation Pass step 1). Also fixes fonts and sizes.
- Template changes since the original: every example slide, layout and the master use Grandview instead of Calibri/Arial/Roboto/Segoe UI; sizes on slide 2 and in the layouts are whole points from 10pt; slide 5's architecture zones use brand colours instead of blue/amber/green/red (its small labels are documented in `references/slide-types.md`). Logo and header artwork are untouched.

## Quick reference

| What | Value |
|---|---|
| Structural gradient (headers, table headers, timeline bars) | `812B47` → `0B0E5F`, linear, 180° — also now theme `accent2`→`accent1` |
| Cover background | A raster image + logo lockup baked into layout 1 — **not** a live gradient. Don't hand-recreate it |
| Body text color | `242424` (not pure black) — also now theme `accent4` |
| Font | **Grandview only**, for every piece of text: titles, body, tables, notes, charts, labels, footers. Never Calibri, Arial, Roboto or Segoe UI. Keep it in the XML even though it won't preview correctly in this sandbox |
| Icon font | FontAwesome, white glyphs on gradient badges (icons only, never text) |
| Colours | Quantzig palette only: navy `0B0E5F`, wine `812B47`, purple `2C165E`, note purple `592258`, body `242424`, white, and the pale pink `F8F4F6` / dusty rose `EDD3D4` / lavender `D2D0E1` tints. No yellow, orange, blue, teal, green or red for decoration |
| Green / amber / red | `30A050` / `C38424` / `BD413A` **only when a metric's status is shown** (RAG, KPI vs target, up/down deltas, variance). Small uses only: a dot, tag, cell or delta. Never for phases, zones, options or decoration |
| Font sizes | Whole points only, starting at 10pt: 10, 11, 12, 13 and up, with 10.5 as the one allowed half size. Nothing below 10pt and no other fractions (no 9.5, 11.5, 13.5). On-slide notes and footnotes are 11pt Grandview, bold italic, centred, in note purple `592258`. Applies retroactively too: after any size change, run the Slide-by-Slide Validation Pass below, because it commonly breaks fixed-height boxes sized for the old text |
| Card/panel fill on content cards (≥1.3in in either dimension) | White or a flat near-white solidFill, or a true ~4%-alpha tint of the gradient recipe. Never the tint+`satMod=160000` "glossy" recipe at this size — see Common Pitfalls |
| Logo & footer | Inherited from the master on every layout — never hand-placed. See `master-and-layouts.md` |
| Footer text | `Copyright © [year] Quantzig. All rights reserved.` + page number, inherited |
| Rule to never break | No accent line/underline under titles — the gradient header bar is the only separator |
| Shape construction | Text goes directly inside the fill/border shape (autoshape or placeholder) — never a text box layered over a separate background rectangle. One shape per content block |
| Writing voice | Title Case titles using `&` not "and"; sentence-case one-line kicker; bullets follow **Bold term:** plain sentence.; footnotes get their own asterisked caption line |
| Complex graphics (solution burst, architecture diagram) | Reuse the existing group and swap labels — don't hand-redraw. See style-guide.md |

### House rules from delivered deck reviews

These override anything older in the references.

- **Forbidden characters in slide copy:** em dash, middle dot, and arrow characters. Use a comma, colon, parentheses, or a new sentence.
- **Palette:** brand colours only (see Quick reference). `592258` (note purple) is part of the palette for notes and footnotes. `FB4A1A` orange and `6787B7` grey-blue are old Office theme defaults, not brand colours; they creep in when a shape is created without an explicit fill, so always set fills explicitly and remap them on sight. Green, amber and red appear only on metric status.
- **Fonts and sizes:** Grandview for every run; sizes are whole points from 10pt up, plus 10.5.
- **No dead white space:** a text box or panel with more than about 0.45in of unused height is a defect, and so is a slide whose content area is less than about 70% covered by content (visual, panels, text). Add substance, enlarge the visual, or add a supporting panel. Copy that is too terse is as much a problem as copy that overflows.
- **No meta-commentary:** notes and footnotes carry only an assumption, a basis, a caveat or a disclaimer, never commentary about the deck itself ("kept to fifteen boxes so it stays readable").
- **No placeholder contacts:** never add personal contact cards unless real names and details are supplied. Close with layout 12 (Reach Out), which carries Quantzig's own contact details. When the deck ends on a decision, the last content slide ends on one full-width decision band.
- **Visual construction:** group composite visuals (cost ladder, timeline rows, KPI stacks, card sets) so they move as one; every table column gets its own header cell; separate side-by-side sections with a thin vertical divider; content cards open with an icon; no thin accent stripe along a card edge (use the gradient header bar with the card title inside it); keep everything inside the canvas and above the footer, about 6.7in from the top.

Full detail and real examples for all of the above are in `references/style-guide.md` — read it before drafting new slide text or building new shapes, not just before picking colors.

## The 12 layouts (full detail in `references/master-and-layouts.md`)

| # | Name | Used in example deck? | When to use |
|---|---|---|---|
| 1 | Title Slide | Yes (cover) | Deck opener |
| 2 | Agenda Slide | No | Table of contents, right after the cover |
| 3 | Blank Slide with Header | No | Content slide with no colored header |
| 4 | Header with Partition | No | Big stat/quote/CTA on the right, content on the left |
| 5 | Header with Band | No | Bolder full-width header than the ribbon |
| 6 | Blank Slide | No | Freeform content |
| 7 | Header Ribbon | **Yes — every content slide** | Default workhorse content layout |
| 8 | Header with BG | No | Image-forward slide with a captioned box |
| 9 | Blank (variant B) | No | Alternate image-forward slide |
| 10 | Blank (variant C) | No | Minimal right-edge accent |
| 11 | Partition Slide | No | Section-divider slide |
| 12 | Cover (Reach Out) | No | **Ready-made closing/contact slide** — use as the last slide of any deck |

## Nine content patterns (full detail in `references/slide-types.md`)

| # | Type | Source slide | Use for |
|---|---|---|---|
| 1 | Cover/title | `slide1.xml` | Deck opener |
| 2 | Landscape & vision (problem/solution split) | `slide2.xml` | Current-state vs future-state, "why this project" |
| 3 | Phased-release table + key deliverables (2×2 mini-cards) | `slide3.xml` | Roadmap summary across phases |
| 4 | Feature scope grid by release | `slide4.xml` | Detailed feature/scope breakdown per phase |
| 5 | Architecture diagram | `slide5.xml` | Technical architecture / data flow — labor-intensive to adapt, see style-guide |
| 6/7 | Sample screens | `slide6.xml`, `slide7.xml` | Product screenshots / UI walkthrough |
| 8 | Gantt/execution timeline | `slide8.xml` (multi-month), `slide9.xml` (week-by-week + deliverables panel) | Project timeline, delivery schedule |
| 9 | Resourcing & costing table | `slide10.xml` | Staffing plan, cost breakdown |

## Workflow

1. Pick a layout from the 12 (usually layout 7, "Header Ribbon", unless the slide needs a different chrome treatment) and a content pattern from the nine, if one fits.
2. `python scripts/thumbnail.py assets/quantzig-deck-template.pptx template-thumbs` — confirm visually before building.
3. Create the new slide against its layout — either `prs.slides.add_slide(layout)` in python-pptx, or duplicate an existing same-layout slide with `add_slide.py` (which carries the layout relationship with it) and edit its content. Never write a new slide part with a hand-built layout relationship, and never copy logo/footer shapes onto it manually — they inherit.
4. Edit content per `references/slide-types.md`'s swap guidance for the pattern you picked — preserve existing `<a:pPr>`/`<a:tcPr>` formatting by copying sibling paragraphs/cells rather than writing new ones from scratch.
5. Consider closing the deck with layout 12 (the ready-made "Reach Out" contact slide) instead of building a new closer.
6. Update the footer copyright year if the deck spans into a new calendar year; update cover title/subtitle/date.
7. Run the **Slide-by-Slide Validation Pass** below on every slide, not just the ones you touched last. Then `scripts/office/validate.py out.pptx --original assets/quantzig-deck-template.pptx`, rezip, and do a full-deck visual QA render via the soffice+pdftoppm conversion in the base pptx skill. Only then call the deck final.

## When neither a layout nor a content pattern fits

If the new deck needs a slide shell not in the 12 layouts, or content structure not in the 9 patterns (e.g. a pricing comparison matrix, an org chart), build it fresh but **stay inside the style rules above** — same brand colours, Grandview only, same "text lives inside shapes" construction, same "no title underline" rule, and still build it on top of one of the 12 layouts (probably 3 or 6, the least decorated ones) rather than inventing new chrome. Don't invent a new accent color; reuse one from the palette in `references/style-guide.md`.

## Common Pitfalls (found shipping a real 35-slide deck through multiple edit rounds)

These recur across edit rounds — check for them explicitly during the Validation Pass, don't rely on spot-checking a few slides.

**Glossy gradient tint on content cards.** A 3-stop `gradFill` where each stop is a color (`srgbClr` OR `schemeClr` — check both, catching only `srgbClr` misses half the instances) carrying a `<a:tint>` plus `<a:satMod val="160000"/>` renders as a visibly gray/saturated fill — not the intended subtle pastel — once the shape's width or height reaches roughly 1.3in or more. Rule: any content card/shape ≥1.3in in either dimension gets a flat near-white solidFill or a true low-alpha (~4%) tint of the gradient recipe instead. Reserve the tint+`satMod=160000` "glossy" recipe only for small decorative badges (~0.4–0.6in) — it reads fine at that size.

**Off-palette hex colors creeping in.** Colors outside the brand palette (seen in practice: yellow/amber zone outlines, bright red `BD413A` used decoratively, slate `6A748C`, pale tint `9AA6C2`, sky blue and blue on architecture diagrams) can end up scattered across icon fills, stat numbers, borders, and italic captions on many slides without ever appearing in `theme1.xml`. They tend to enter during content generation, not editing, so a targeted look at "known problem colors" isn't enough — do the full sweep in the Validation Pass below every time.

**Font-floor bump breaks fixed-height boxes — in at least three distinct ways, and a deck can contain all three at once:**
- An `spAutoFit` box nested inside a non-uniformly-scaled group: fix by widening the box and tightening insets/line-spacing, not just resizing.
- A plain (no-autofit) fixed-height bullet box: fix by growing `cy` using slack in the parent card, plus tightening `lnSpc`/`spcAft`.
- An `spAutoFit` box sized for a shorter sibling's wording, where a longer-worded instance now wraps one line more than the box height allows: fix with an `lnSpc` reduction (e.g. to 85%) if there's no safe room to grow the box, or grow the box and shift following content down if there is room.

After any font-size change — including retroactively applying the 10pt floor to an existing deck — re-verify actual rendered line count against stored box height for every text box, not just a couple of "representative" slides. The same card template can wrap differently per instance purely because that instance's wording is longer.

**Heading-then-body collision.** When a card layout stacks two independently-positioned, fixed-height text boxes (a heading directly above a body box, both `anchor="t"`, no autofit tying them together — this is exactly how the Executive Summary card layout works), a heading that wraps one line more than its box budgets for will NOT get clipped: a `noFill`/`noLine` textbox just lets the overflow line render past its declared bottom, straight into the body box below it, since there's no fill to hide the collision. Check the heading's actual wrap-line-count against its `cy` using the real text for every instance, and if one instance needs an extra line, grow that heading's `cy` by one line-height AND shift its body box down by the same amount — only for that instance, not sibling instances that already fit.

## Slide-by-Slide Validation Pass

In addition to the numbered steps below, check every slide for the house rules above: Grandview only, whole-point sizes from 10pt (10.5 allowed), no run below 10pt, notes and footnotes styled in `592258`, no `FB4A1A` or `6787B7`, no forbidden characters, no panel with more than about 0.45in of unused height, no meta-commentary, no placeholder contacts, composite visuals grouped, and nothing below the footer line.

Run this after any content or style edit round, before calling a deck final. A visual skim of a handful of slides misses exactly the bugs above, because they hide in specific instances of a repeated template, not in the template itself.

1. **Automated sweep** — run `python3 scripts/deck_check.py deck.pptx` (in this `formatting/` folder). It reports, slide by slide: fonts that are not Grandview, sizes that are not whole points from 10pt (10.5 allowed), off-palette colours, every green/amber/red use, content slides too thin to read without a voice-over (under about 70 words), content slides with too much empty area (under about 70% covered), pairs of slides with near-identical layouts, and library visuals used more than once. `--fix -o deck.pptx` repairs fonts and sizes automatically; everything else is fixed by hand. Confirm every STATUS line marks a real metric, otherwise recolour it to brand. Re-run until it prints CLEAN.
2. **Text-overflow heuristic scan** — for every text shape except ones with `normAutofit` (already shrink-to-fit safe), estimate needed height (chars-per-line from usable width and font size, line count from paragraph text length, times line height including `lnSpc`/`spcAft`) and compare to the shape's actual available height. Flag ratio (needed/available) > 1.15 as a candidate. This heuristic has real false positives (single large numerals, short bold headings) — treat every flag as a candidate for visual crop-check, never as a confirmed bug by itself.
3. **Adjacent-shape collision check** — for any two shapes on a slide positioned directly above/below or beside each other by design (heading+body, icon+label), verify the gap between shape A's bottom/right edge and shape B's top/left edge stays non-negative using each shape's real rendered content extent, not just its nominal stored geometry. Step 2's heuristic will NOT catch this pattern — neither box individually exceeds its own overflow ratio, since the bug is the collision between them, not either one's internal overflow.
4. **Cross-instance alignment diff** — for decks with repeated slide "types" (e.g. several case studies each reusing a cover/exec-summary/problem-solving/etc. layout), compare each shape's `(name, off, ext)` tuple across instances with a small EMU tolerance (~15000 EMU) and flag outliers as likely structural bugs versus expected content-driven autosize variance (different text length legitimately produces a different autofit height).
5. **Exact-coordinate visual crop-check** — for every candidate flagged in steps 2–3, render the slide and crop using EXACT EMU-to-pixel coordinates derived from the shape's own `xfrm` and the slide canvas size (12192000×6858000 EMU: `px = emu / canvas_emu * image_px`). Never crop by an arbitrary fraction of the slide image (e.g. "top 60%") — that produces false-positive "clipping" that isn't real, and did in practice before this rule was written down.
6. **Final integrity check** — only after every flagged candidate is fixed or confirmed a false positive via step 5, rezip the pptx, confirm it opens cleanly (e.g. a python-pptx slide-count check), do a full-deck re-render, and only then consider the deck final and deliver it.
# Quantzig Deck — Style Guide

Extracted directly from `assets/quantzig-deck-template.pptx` (theme, master, layouts, slide XML), verified with a full shape-by-shape audit — not guessed from how it looks in the thumbnail. Slide canvas is 13.33" × 7.5" (widescreen, `cx="12192000" cy="6858000"`).

**Read `master-and-layouts.md` first.** Logo, footer, and header chrome come from the master/layouts by inheritance — this file covers color, type, and the content-shape conventions that sit on top of that chrome.

## Color palette

**Use only the Quantzig palette below.** No yellow, orange, sky blue, blue, teal, green or red anywhere for decoration, zone colour-coding, icons, borders, card headers, chart series or highlights. Differentiate items with navy, wine and purple, tints of them, numbers and icons, never with extra hues.

### Brand colours (use everywhere)

| Role | Hex | Where it's used |
|---|---|---|
| Deep navy | `0B0E5F` | Gradient partner (dark end) on section headers, table header rows, timeline bars, box outlines. Theme `accent1` |
| Wine / magenta | `812B47` | Gradient partner (light end) on the same elements. Theme `accent2` |
| Wine (alt shade) | `7F2A4C` | Near-identical alt used on some shape fills/outlines, interchangeable with `812B47` |
| Deep purple | `2C165E` | Secondary dark fill, card headers and accents. Theme `accent3` |
| Deep purple (note) | `592258` | Notes, captions and footnotes, and secondary dark accents. Confirmed on client review |
| Body text | `242424` | Default body copy colour (not pure black). Theme `accent4` |
| Pure black | `000000` | Reserved for a few emphasis runs, not the default text colour |
| White | `FFFFFF` | Text/icons on gradient or dark fills; theme `bg1`/`lt1` |
| Pale pink tint | `F8F4F6` | Light card and panel background (default light fill) |
| Dusty rose tint | `EDD3D4` | Light card background / divider |
| Pale lavender tint | `D2D0E1` | Light card background |

For more than three distinguishable series or zones (charts, architecture zones, multi-lane roadmaps), use shades of the brand colours (navy, wine, purple, 592258, then the same at 60% and 30% tint) rather than a new hue.

### Metric status colours (only when a metric's status is shown)

| Role | Hex | Allowed use |
|---|---|---|
| Green | `30A050` | Metric on track / on or above target / positive change. Theme `accent6` |
| Amber | `C38424` | Metric at risk / slightly off target. Theme `accent5` |
| Red | `BD413A` | Metric off track / below target / negative change |
| Mint, cream, blush tints | `F7FDF9`, `FDFBF6`, `FDF7F7` | Background of a status cell or KPI tile that carries the matching status colour |

Use these **only** where the slide shows a measured value against a target or a direction of change: RAG status columns, KPI tiles with target vs actual, up/down deltas, variance tables, health scorecards. Keep them small (a dot, a tag, a cell, a delta number or arrow), never a large fill. Everywhere else, including "good vs bad" framing without a metric, pros and cons, risk lists and phase colours, use brand colours only.

**Not brand colours:** `FB4A1A` (orange) and `6787B7` (grey-blue) are old Office theme defaults. They creep in when a shape is created without an explicit fill, so always set fills explicitly and remap these on sight.

**Retired:** sky blue `6EA5F7`, blue `2866C4` and light gray `E8E8E8` are no longer used. The template's architecture slide (slide 5) was recoloured to brand colours to remove its blue/amber/green/red zone outlines.

**Rule of thumb:** navy/wine gradient = structural chrome (headers, bars, table headers). Brand tints = light card fills. Status colours = metric status only.

## Theme colors (updated in this template)

PowerPoint's theme only has 6 "accent" slots, and the original file's theme (`Custom 4`) didn't match the deck's real working colors at all — it still had generic Office defaults (an orange `FB4A1A`, a gray-blue `6787B7`, etc.) that nothing in the actual deck used. That mismatch has been fixed: the theme (renamed **"Quantzig Brand"**) now maps the deck's real palette onto the 6 accent slots:

| Slot | Old value | New value | Note |
|---|---|---|---|
| `accent1` | `FB4A1A` (orange) | `0B0E5F` (navy) | Primary structural color |
| `accent2` | `6787B7` (gray-blue) | `812B47` (wine) | Gradient partner |
| `accent3` | `0D1776` (navy) | `2C165E` (purple) | Secondary dark accent |
| `accent4` | `404040` (gray) | `242424` (body text) | Matches actual body-copy color |
| `accent5` | `9E480E` (brown) | `C38424` (amber) | Metric status only, never pick for decoration |
| `accent6` | `F2F2F2` (light gray) | `30A050` (green) | Metric status only, never pick for decoration |

`dk1`/`lt1`/`dk2`/`lt2`/`hlink`/`folHlink` were left untouched — they're either correct already (`lt1`=white, `dk1`=black) or not referenced anywhere in the deck's actual content, so changing them carried risk with no benefit.

**Why this is safe:** almost every shape in the deck sets its fill/line color explicitly (hardcoded hex, not a theme reference) — the `accent1` references that exist (525 of them, across the deck's ~150 autoshapes) are leftover PowerPoint "quick style" metadata (`<p:style>` blocks) that get overridden by each shape's own explicit fill. Re-rendering the whole deck before and after this change produced pixel-identical output — **verify this yourself if you further edit the theme**, don't assume.

**Why it's worth doing anyway:** any *new* shape inserted natively in PowerPoint (via the Shape Styles gallery, or via `theme_color = MSO_THEME_COLOR.ACCENT_1` in python-pptx) now picks up the real navy instead of the old orange. This was tested directly — a fresh shape filled with "Accent 1" renders navy in the updated template.

The brand tints, red `BD413A`, `592258` and `7F2A4C` don't have theme slots (only 6 exist), so use their hex values directly. Accent 5 and Accent 6 in PowerPoint's colour picker are amber and green: pick them only for metric status.

## Signature gradients

Two distinct gradients appear in live, editable form — do not mix them up, and don't assume the cover uses one of them (see the correction below).

**1. Header / table-header / timeline-bar gradient** (the one used everywhere on content slides):
```xml
<a:gradFill><a:gsLst>
  <a:gs pos="0"><a:srgbClr val="812B47"/></a:gs>
  <a:gs pos="100000"><a:srgbClr val="0B0E5F"/></a:gs>
</a:gsLst><a:lin ang="10800000" scaled="0"/></a:gradFill>
```
Linear, wine (`812B47`) → navy (`0B0E5F`), angle 180°. A 5%-alpha version of the same gradient is used for subtle tinted panel backgrounds (e.g. behind bullet-list text boxes).

**2. A second gradient recipe exists in the layout system** (orange `FC4A1A` → transparent navy → darkened `accent3`, diagonal) but — important correction — **this is not what paints the visible cover slide.** It sits, mostly hidden behind a photo, on the Agenda layout (layout 2) as a legacy/leftover shape. Don't treat it as an active design pattern to reuse.

**What actually paints the cover (layout 1):** a raster image (`image2.jpeg`, spanning the full width and the top 3.06" only) plus a white/reversed Quantzig logo+tagline lockup (`image3.svg`, ~4.17"×1.15", top-left) layered on top. If you ever need to change the cover's look, replace or re-export that image asset — editing a "gradient" won't touch it, because there isn't a live one there.

## Typography

| Element | Font | Size | Weight/color |
|---|---|---|---|
| Cover title (e.g. "Formulary IQ") | Grandview (theme major/minor font) | 36pt | White |
| Cover subtitle (e.g. "Implementation Plan") | Grandview | 20pt | White |
| Content slide title | Grandview | 24pt | White (sits on the gradient header bar) |
| Content slide kicker/subtitle line | Grandview | 18pt | White, lighter weight |
| Card/panel header labels (small, on gradient fill) | Grandview | 12pt | White, bold |
| Body bullets, table cells | Grandview | 12pt | `242424`, bold lead-in phrase + regular continuation (e.g. "**Scattered data sources:** Coverage info spread across…") |
| Notes, captions, footnotes | Grandview | **11pt** | Bold italic, centred, deep purple `592258`. Never smaller. Only assumptions, bases, caveats, disclaimers |
| Column header cells (lane labels, table columns) | Grandview | 12pt | Bold, on the column's own header cell - every column needs one |
| Table header row | Grandview | 12pt | Bold |
| Icon glyphs | FontAwesome | varies | White, used inside gradient-filled circular/square badges and inside the decorative graphics described below |
| Footer / page number | Grandview (inherited from the master) | small | Inherited, never hand-placed |

**Grandview is the only text font.** Titles, kickers, card labels, body bullets, table cells, notes, chart labels and footers are all Grandview (Grandview Display is acceptable for large display titles only). Never Calibri, Arial, Roboto, Segoe UI or any other face. The template's example slides, layouts and master were converted from Calibri/Arial/Roboto to Grandview, and the theme's major and minor fonts are Grandview, so text that inherits the theme (`+mj-lt`, `+mn-lt`) is already correct.

**Font sizes are whole points, 10pt and up.** Allowed: 10, 11, 12, 13, 14 and so on, plus 10.5 as the one half size. Never 8, 9, 9.5, 11.5, 13.5 or any other fraction. Use 10 or 10.5 only for dense secondary text (table cells, chart labels, visual slot descriptions); body copy is normally 12, card titles 12 to 14, big numbers 20 and above.

FontAwesome is allowed only as the icon glyph font inside icon badges; it is not a text font.

Grandview is not installed in this sandbox, so LibreOffice renders a fallback face and visual QA renders will look slightly off (widths and wraps can differ a little). Keep `typeface="Grandview"` in the XML regardless and leave a little slack in fixed-height boxes. When adding text through python-pptx, set `font.name = "Grandview"` explicitly or leave the run to inherit the theme; never let a default of Calibri slip in.


## Logo & footer — inherited, not placed

Don't extract or hand-place logo/footer images. See `master-and-layouts.md` for the full explanation. In brief:

- Every content slide's small footer logo, and the `Copyright © [year] Quantzig. All rights reserved.` + page-number footer, come from the master automatically. Update only the copyright year when reusing across calendar years — don't touch position or the image itself.
- The cover's large logo+tagline lockup and background band are part of layout 1, not a separate asset.
- The closing/"Reach Out" slide (layout 12) has its own colored logo+tagline lockup, plus Quantzig's real office directory, baked into the layout.
- Three distinct logo renderings exist in the file if you ever need to inspect them directly: a small colored wordmark (master footer), a large white/reversed lockup (cover), and a large colored lockup (closing slide) — but you should never need to touch any of them individually; picking the right layout brings the right one automatically.

## Shape construction — text lives inside shapes, not layered text boxes

Verified directly in the XML: this deck does **not** draw a background rectangle and then float a separate text box on top of it. Text is typed directly into the same shape that carries the fill/border.

- A feature/deliverable card is **one** `roundRect` autoshape (white fill, thin gray `bg1`-50%-shaded border, ~3.86"×0.87") with the heading and description as **two runs inside a single paragraph** — bold lead-in run (`"Home Dashboard: "`, 12pt, `b="1"`) immediately followed by a regular run with the description (12pt, `b="0"`). No line break, no second shape.
- A multi-bullet panel (e.g. the 5-item "Current Fragmentation & Pain Points" list) is **one** text box holding **five paragraphs** — one `<a:p>` per bullet, each still built the same way (bold lead-in run + regular run within that one paragraph), with a real `<a:buChar char="•">` bullet (never a typed `•` character) and 6pt space before/after each paragraph. Five bullets = one shape, not five.
- A card's colored header banner (when it has one, e.g. "Current Fragmentation & Pain Points" / "Vision for Formulary IQ") is a separate small rounded-top-corner rectangle sitting just above the body text box — that's the one case where header and body legitimately split into two shapes, because the header needs different chrome (gradient fill, rounded top only) than the body panel beneath it.
- "Key Deliverables" mini-cards (slides 3 and 9) are laid out **2×2**, not 4-across — two ~6"-wide cards per row, two rows, under a shared gradient header banner.

**Rule when building or editing any slide in this style:** default to one shape per logical content block. Put a title and its kicker/subtitle in one placeholder as two paragraphs (verified in `slide2.xml`'s "Text Placeholder 1" — title paragraph, then subtitle paragraph, same shape). Put a whole bullet list in one text box as N paragraphs. Only reach for a second shape when something needs genuinely different visual treatment. Don't create a text box per bullet or per card sub-element.

## Image treatment (screenshots, photos)

- Every screenshot/photo picture gets a thin hairline border: `schemeClr bg1, lumMod 85%` (a very light gray, near-white). This same hairline value is reused elsewhere (see Tables below) — treat `bg1 @ 85%` as the deck's one standard "subtle divider" color.
- When a slide shows a primary screenshot plus a smaller supporting one layered near its corner (e.g. slide 6's home screen + a small AI-assistant panel overlay), the pair is grouped into one PowerPoint group and the primary/background image additionally gets a soft drop shadow (`outerShdw`, 40%-opacity black, ~0.07" blur) to lift it — the smaller overlay image doesn't get its own shadow.
- Cap screenshot slides at 2–3 images; the template splits "Sample Screens" across two slides rather than cramming more onto one.

## Complex decorative graphics — reuse as a block, don't hand-recreate

Two shapes in the deck are not simple boxes/icons and are impractical to redraw from scratch for a new topic:

- **The "Solution" graphic** on slide 2 (the radial burst next to the problem/vision cards) is built from roughly 150 individual shapes — dozens of straight connector lines forming a starburst, a cluster of small decorative dot ovals, a freeform "message bubble" shape, and 5 feature labels arranged in a ring. This reads as a bundled stock/SmartArt "idea" graphic, not hand-drawn architecture. If a new deck needs the same "problem → idea/solution" motif, duplicate this whole group and only edit the 5 "Feature N" labels — don't try to reproduce the burst by hand. If the motif doesn't fit, substitute a single simple icon instead of attempting a redraw.
- **The architecture diagram** on slide 5 is similarly not simple rectangles-and-arrows: most of its "boxes" are groups of freeform vector paths (flattened icon graphics — database/server/cloud-style icons) with text labels layered on top, plus one embedded raster logo (the OpenAI icon). Treat this as a real technical illustration, not a lightweight template element. For a new architecture slide, reuse individual icon groups where the same component recurs (e.g., a "Databricks" or "Unity Catalog" icon), swap the text labels, and expect to spend real time redrawing connectors and icons for anything structurally different — don't budget this slide type as a quick text swap the way the table- and card-based slides are.

## Tables

- Uses a native PowerPoint table style, **"Medium Style 3 - Accent 4"** (`firstRow="1" bandRow="1"`) — header row is bold 12pt Grandview; body rows band lightly using `dk1` at 20% tint. Only `firstRow`/`bandRow` are actually turned on in this deck's tables — `firstCol`/`lastCol` highlighting exists in the style definition but isn't used here.
- Table borders use the same hairline convention as images: `bg1 @ 85%` for horizontal rules.
- Gantt/timeline slides (slide types 7–8 in `slide-types.md`) build the bar chart with a genuine mechanism, not a floating shape trick: each "active" cell gets its own `<a:tcPr><a:gradFill>` (the same wine→navy recipe) applied directly to that table cell, on an otherwise plain grid. To redraw a bar for a new schedule, change which cells carry that `tcPr` gradient fill — don't add separate rectangles on top of the table.

## Spacing & layout conventions

- Slide margin: content starts at roughly `x=0.37"` from the left edge — keep that as the standard left margin for new title/body placeholders.
- Title block height ≈ 0.7–0.8", with the kicker/subtitle line immediately below it inside the same placeholder.
- Feature/deliverable cards: ~3.86"×0.87" each (see Shape construction above).
- Two-column and three-column card layouts use even gutters; four-color-coded quadrant callouts use the four light tint colors above, one per quadrant.
- No accent line/rule is used under titles — the gradient header bar itself provides the visual separation. Don't add a separate underline rule when adapting slides (this also matches the general pptx-skill guidance against title underlines).


## Terminology (pharma commercial decks)

Confirmed on client review of the Stemline proposal. These are the client's own words, not stylistic preferences:

- **HCP**, never "doctor" or "physician". Changed in slide titles, card headings, bullets and appendix copy.
- **HCO**, not "account", where the client uses HCO.
- **"small biopharma"**, not "small-biopharma". Do not hyphenate a size-plus-sector phrase.

## Composite visuals must be grouped

Anything that reads as a single visual is **one PowerPoint group**, so it moves and resizes as a unit in the client's hands. The reviewer grouped the stepped cost ladder, each row of the vertical next-step timeline, and the KPI card stack. Build them as groups from the start.

## Column headers and section dividers

- Every column or lane carries its own header cell, matching the visual weight of whatever sits beside it. The roadmap's lane-label column was given a "Development Stage" header to line up with the phase legend blocks.
- Side-by-side sections are separated by a **thin vertical divider line at full band height**, not by whitespace alone. The reviewer added these between the roadmap's stage column and its timeline, and between the investment ladder and the skills list.

## What never goes in a client deck

- **Meta-commentary about the deck.** No note describing how a slide was built, how many boxes a diagram has, that the shapes are editable, or the design rationale. A note exists only for an assumption, a basis for a number, a caveat or a disclaimer.
- **Placeholder contact details.** A "Your Quantzig contacts" block holding placeholder telephone numbers was deleted on review. Leave the contact block out entirely until real details are confirmed.

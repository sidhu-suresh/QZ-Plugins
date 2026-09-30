# Quantzig Deck — Master & Layout Catalog

`assets/quantzig-deck-template.pptx` ships with its full slide master intact: **1 master + 12 layouts**, all preserved as-is (only the theme's accent colors were updated — see "Theme colors" in `style-guide.md`). This is the primary mechanism for building new slides — **not** the 10 example slides by themselves.

## Why this matters — use inheritance, don't recreate

The footer logo, the copyright/page-number footer, and every header treatment (gradient bar, band, partition, etc.) are drawn **once**, on the master or on a layout, and every slide that uses that layout inherits them automatically. Concretely:

- The small Quantzig wordmark (bottom-left, every content slide) is a picture placed directly on `slideMaster1.xml`. Any layout with default `showMasterSp` (all 12 layouts here use the default) shows it automatically. You never place this image yourself.
- The `Copyright © [year] Quantzig. All rights reserved.` + page number footer is likewise master-level.
- Each layout's own header treatment (gradient ribbon, band, partition block, diagonal wash, etc.) is baked into that layout file — pick the layout, and the header comes with it.

**So: never extract the logo/footer as standalone image assets and manually place them on a new slide.** Instead, create the new slide against the right layout (`prs.slides.add_slide(layout)` in python-pptx, or in raw XML give the new `<p:sld>` a relationship to the chosen `slideLayoutN.xml`) and everything else follows for free. The only exception found in the deck: the cover layout's big logo+tagline lockup and its background band are layout-specific artwork (see below) — those come from the layout too, not from a separate asset you place.

## The 12 layouts

| # | Name | File | Visual | Used in example deck? | When to use |
|---|---|---|---|---|---|
| 1 | Title Slide | `slideLayout1.xml` | Top third has a textured navy/orange background image with the large white Quantzig logo + tagline lockup over it; title/subtitle/date placeholders sit in the lower half | Yes — slide 1 (cover) | Deck cover/title slide |
| 2 | Agenda Slide | `slideLayout2.xml` | Large photo fills the right ~60%; white panel on the left for an agenda/TOC list; small red accent rule above the heading | No | A table-of-contents / agenda slide right after the cover |
| 3 | Blank Slide with Header | `slideLayout3.xml` | Plain white canvas, just the title placeholder reserved (no colored header) | No | Any content slide where you don't want a colored header bar at all |
| 4 | Header with Partition | `slideLayout4.xml` | Full-height gradient block filling the right ~33% of the slide, rest white | No | A slide with a big pull-quote, stat, or CTA on the right and normal content on the left |
| 5 | Header with Band | `slideLayout5.xml` | Full-width gradient band across the top ~20% height, flush to the top edge | No | A bolder header treatment than the ribbon (7) — use when the slide needs more visual weight up top |
| 6 | Blank Slide | `slideLayout6.xml` | Completely bare canvas, footer/logo only | No | Freeform content, or as a base for a custom one-off layout |
| 7 | Header Ribbon | `slideLayout7.xml` | Thin gradient ribbon near the top, not touching the top edge (a floating strip) | **Yes — slides 2–10, every content slide** | The default workhorse content layout. Use for the vast majority of slides |
| 8 | Header with BG | `slideLayout8.xml` | Diagonal gradient wash across the top-right, with a thin cream-bordered content box | No | A slide built around one image/screenshot with a captioned box |
| 9 | Blank (variant B) | `slideLayout9.xml` | Similar diagonal wash + bordered box, different proportions than 8 (larger wash, lower box) | No | Alternate image-forward slide, same family as 8 |
| 10 | Blank (variant C) | `slideLayout10.xml` | Thin gradient accent strip on the right edge only, rest white | No | Minimal decorative accent on an otherwise plain content slide |
| 11 | Partition Slide | `slideLayout11.xml` | Full-height gradient block filling the left ~50%, rest white | No | Section-divider / part-opener slide |
| 12 | Cover | `slideLayout12.xml` | White background, colored logo+tagline top-right, "Reach Out" heading, contact email, and Quantzig's office-directory table (US/UK/Canada/APAC/Hungary addresses & phone numbers) baked in | No | **The closing slide.** This is a ready-made "Contact Us" slide — use it as the last slide of any client deck rather than building a new one |

## Adding a new slide the right way

```python
from pptx import Presentation
prs = Presentation("assets/quantzig-deck-template.pptx")
layout = prs.slide_masters[0].slide_layouts[6]   # index 6 = "7_Header Ribbon" (0-indexed)
slide = prs.slides.add_slide(layout)
```
or, editing XML directly: duplicate an existing `<p:sld>` with `add_slide.py` (it copies the slide's layout relationship along with it) rather than writing a new slide part by hand.

Only 2 of the 12 layouts are used in the example deck (Title Slide for the cover, Header Ribbon for every content slide) — the other 10 are legitimate, ready-to-use options that just haven't come up in this particular deliverable. Check this table before assuming you need to invent a new header treatment; there's very likely already a layout for it.

## What's still deck-specific vs what's reusable across any deck

- **Master + all 12 layouts** — identical across every Quantzig deck, don't modify.
- **Theme colors** — the brand palette, same across every deck (see `style-guide.md`).
- **The 10 example slides' content-shape patterns** (cards, tables, gantt bars, etc.) — these live on top of layout 7 and are catalogued separately in `slide-types.md`, because they're reusable *patterns* built with ordinary shapes, not part of the master/layout system itself. Pick a layout first, then, if useful, reuse one of these content patterns inside it.

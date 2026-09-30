# Visual Library Guide

Part of the qz-decks skill. Paths in this file (`references/...`, `assets/...`, `scripts/visuals.py`) are relative to the `visuals/` folder.

This guide turns slide content into the right picture. It bundles a 330-slide infographic library (`assets/visual-library.pptx`), a catalog of it, contact sheets to look at, and a script that lifts any library visual into a deck with real text, real icons, the target brand's colours and screenshots, or renders it as a PNG for non-PowerPoint formats.

It does not own layout or brand. For Quantzig decks, the formatting guide (`formatting/GUIDE.md`) still decides slide layouts, header, footer, fonts and colour rules; this guide fills the content area. For file mechanics read the `pptx` skill.

## Step 0. Find the visuals folder first (do not skip)

The library, catalog, sheets and script sit in the `visuals/` folder of the qz-decks skill. Use the skill's base directory if the app reports it. Otherwise search:

```bash
S=$(find / -path '*/visuals/scripts/visuals.py' -not -path '/proc/*' 2>/dev/null | head -1)
D=$(dirname "$(dirname "$S")"); ls -R "$D"   # expect assets/visual-library.pptx, assets/sheets/, references/catalog.md, scripts/visuals.py
```

Some Claude apps install only the SKILL.md of a skill and leave the other files behind. If the search finds nothing:

1. Check whether the user attached `qz-decks.skill` (or a zip of it) to this chat: `ls /mnt/user-data/uploads`. If so, unpack it and use that copy:
   ```bash
   mkdir -p /home/claude/qzd && cd /home/claude/qzd && python3 -c "import zipfile,glob; zipfile.ZipFile(glob.glob('/mnt/user-data/uploads/qz-decks*')[0]).extractall('.')"
   S=$(find /home/claude/qzd -path '*/visuals/scripts/visuals.py' | head -1); D=$(dirname "$(dirname "$S")")
   ```
2. If it is not attached, ask the user in one line to attach the `qz-decks.skill` file so the visual library can be used. Do not start building visuals from scratch while waiting.
3. Only if the user says to go ahead without it: follow Steps 1 to 3 as written, then draw each chosen family natively with the geometry recipes in this file's "Fallback recipes" section at the end, or with `references/visual-recipes.md` and `references/visual-vocabulary.md` in the skill root.

## Native shapes, not pictures

Everything `place` puts on a PowerPoint slide is native, editable PowerPoint shapes (freeforms, groups, text boxes) that the client team can recolour, move and retype. This meets any "native shapes only" rule, including the formatting guide (`formatting/GUIDE.md`)'s. The only exceptions are icons in `--icon-mode png` and screenshots passed with `--images`; for Quantzig decks use `--icon-mode glyph` so icons stay editable FontAwesome text.

## Step 1. Decide which slides get a visual

Read each slide's content and name its shape. The shape, not the topic, decides the visual.

| Content shape | Signals in the text | Catalog category |
|---|---|---|
| Ordered steps | phases, approach, "how it works", then/next, methodology | process |
| Repeating loop | continuous, iterative, retrain, feedback, monthly cycle | cycle |
| One thing with many parts | platform with modules, sources into a product, stakeholders around a programme | hub |
| Levels or foundations | maturity, priority tiers, building blocks, one to many breakdown | hierarchy |
| Narrowing | pipeline, conversion, filter, data to insight | funnel |
| Dates and phases | roadmap, milestones, plan by month or quarter, history | timeline |
| Options side by side | A vs B, build vs buy, current vs future, SWOT, pricing or engagement tiers | comparison |
| Parallel items, no order | capabilities, benefits, features, workstreams, 2x2 prioritisation | matrix |
| Fit and dependency | integrated solution, interlocking parts, overlap | integration |
| A few headline numbers | accuracy, adoption, savings, % complete | kpi |
| Real data series | trends, splits, rankings | charts (build natively, styling reference only) |
| Geography | footprint, regions, markets | maps |
| One big idea | hidden root causes, foundation, protection, journey | metaphor |
| A product or dashboard | app screens, demo, sample output | mockups |
| People | team, resourcing, personas | people |

Rules of thumb:
- Most content slides with structure should carry a visual. A slide that is one message, a dense table the audience must read, legal or commercial terms, or an appendix list stays as text or a table.
- Numbers always go in a native chart or a KPI visual with the real values. Never put invented numbers in a visual; if a library visual has % labels and the content has no numbers, drop those labels.
- Match the item count. A 4-step process goes on a 4-slot visual. Do not pad with filler items or cram 7 items into a 5-slot visual; pick another visual or split the slide. Three to six items is the comfortable range.
- Vary the deck. Use each library slide at most once per deck, never give two slides the same structure, and mix families (process, grid, hub, timeline, comparison, metaphor) across consecutive slides. See the Layout menu in the main SKILL.md.
- Make the visual strong. Place it large (about 45 to 65% of the content area, top or left), put the slide's real content into its labels, and fill the rest of the slide with supporting panels and a takeaway band so no large area is left empty.
- Metaphor illustrations (iceberg, road, umbrella, keys) are strong but loud: at most one or two per deck.
- Never use the slides listed under "Do not use in client decks" in `references/catalog.md` (brand logos, 3D charts that distort data, gendered silhouettes).

## Step 2. Pick the library slide

1. Open `references/catalog.md`, go to the category, shortlist two or three slides whose description and counts fit.
2. View `assets/sheets/<category>.jpg` (every thumbnail carries its slide number) and choose the one that suits the content and the rest of the deck.
3. Run `preview` on the chosen slide to see every editable label, and `inspect` for the exact list:

```bash
# $S was set in Step 0
python3 $S preview 84 -o /home/claude/p84.png        # labels: red t# text, magenta s# icon, green i# image slot
python3 $S inspect 84                                # T# top-level shapes, t# texts, s# icons, i# image slots
```

## Step 3. Write the words for the slots

Library slots are small. Keep slot titles to one to three words and slot descriptions to one full sentence (about 12 to 20 words) that explains what the item means for this audience; enlarge the `--box` or drop decorative % labels to make room. Anything that does not fit goes into supporting panels beside or below the visual, so the slide still reads without a presenter. Follow the host deck's voice (for Quantzig: Title Case titles with "&", "**Bold term:** plain sentence" bullets; `**text**` at the start of a line in `--texts` becomes a bold run). No em dashes and no filler phrasing. Every `t#` that holds library placeholder copy ("Title Goes Here", "Keyword", lorem) must get real text or be dropped; the script warns about any it finds.

Pick icons that mean something for each item. Icons are FontAwesome 4 names; search `references/fontawesome4-icons.tsv` (for example `grep -i chart references/fontawesome4-icons.tsv`). Useful ones for analytics work: database, line-chart, bar-chart, pie-chart, area-chart, cogs, sliders, search, lightbulb-o, rocket, shield, lock, users, user, globe, cloud, server, code, cubes, sitemap, random, refresh, check, flag, bullseye, trophy, clock-o, calendar, money, shopping-cart, truck, industry, flask, stethoscope, heartbeat, bell, comments, file-text-o, graduation-cap, handshake-o.

## Step 4. Build it in the format asked for

### PowerPoint (.pptx), including Quantzig decks

Place the visual onto a slide. Each call writes a new file, so chain calls one slide at a time.

```bash
python3 $S place 84 --target deck.pptx --new-slide 6 --title "Delivery Approach" \
  --texts texts.json --icons '{"s13":"database","s22":"search"}' --drop T14,T15 \
  --palette quantzig --font Grandview --min-font 10 --icon-mode glyph -o deck.pptx
```

- `--new-slide N` adds a slide from layout index N (0-based) of the target; `--slide N` uses an existing slide (1-based). `--title` fills the header placeholder. For Quantzig, layout index 6 is "Header Ribbon" and the default box sits under its header.
- `--box X,Y,W,H` (inches) sets the area to fit into; aspect is kept and the visual is centred. Leave room for any text you add beside it.
- `--texts` accepts a JSON file or inline JSON: `{"t5": "Discover", "t6": "Map sources and agree KPIs"}`. `\n` starts a new paragraph.
- `--drop` removes what you do not need: T# for top-level shapes (typically the library's footer paragraph "Footer Text" and its "Straight Line buttom"), s# for anything nested, including unused % labels.
- `--images a.png,b.png` fills image slots i0, i1 in order (screenshots into device mockups, headshots into team layouts). Unfilled slots are removed.
- Colours: `--palette quantzig` applies Quantzig rules (accent fills become the wine to navy gradient, light tints a 4% navy wash, shades navy, text greys 242424, coloured text navy, wine or purple, and any hard-coded yellow, orange, blue or other library colour is remapped to navy or a brand tint). The library's multi-colour look (blue, teal, green, orange, red, maroon) never survives into a Quantzig deck.
- Metric status colours: green `30A050`, amber `C38424` and red `BD413A` are added by hand, and only on visuals that show a metric against a target or a direction of change (KPI tiles, RAG tags, up/down deltas). Never use them to tell steps, zones or options apart. `--palette custom --colors accent1=HEX,...,accent6=HEX` maps the library's six accent slots to another brand. `--palette keep` lets the target theme's accents apply.
- Icons: `--icon-mode glyph` inserts an editable FontAwesome character (Quantzig decks already use FontAwesome, so use glyph there). `png` (default) renders the icon to an image that shows correctly on any machine; use it for decks going to people who may not have the font.
- Fonts: the library uses Roboto. `--font` swaps it; for Quantzig decks it is always Grandview (the default with `--palette quantzig`), never Calibri. `--min-font` applies a floor after scaling (Quantzig: 10).

Decks built with pptxgenjs: generate the deck first with the visual's area left empty, then run `place --slide N --box ...` on those slides. Decks built by editing a template (the formatting guide (`formatting/GUIDE.md`)'s flow): do all structural work (add, delete, reorder slides) first, place visuals last, then run the host skill's validation pass.

Charts are skipped by the script. Build them natively (pptxgenjs `addChart` or python-pptx charts) with the real data, styled like the library's chart slides if useful.

### HTML page, Slides or Design artifact, web deck

Redraw the chosen visual as inline SVG in the page, using the library slide as the geometry reference and the host brand's colours. This keeps text crisp, responsive and editable. Recipes for the common families are in `references/formats.md`. For complex illustrations that are impractical to redraw (iceberg, device frames, maps, trees), render a PNG and embed it:

```bash
python3 $S render 154 --texts t.json --palette custom --colors accent1=0B0E5F,accent2=812B47 --font Grandview -o iceberg.png
```

### Word, PDF, Claude Doc or any document

Render each visual to PNG with `render` (same editing options as `place`; `--dpi 220` default, `--width` sets the canvas in inches) and insert it at full text width. For Word follow the docx skill; for PDF the pdf skill. Keep the words inside the image short and repeat anything the reader must find by search in the body text.

## Step 5. Check it

- Render the slides (pptx skill: soffice to PDF, pdftoppm to JPEG) and look at every slide with a placed visual. Check first for text spilling out of slots: the fix is shorter words, then a larger `--box`, then a different visual. Then check leftover placeholder copy, icons that do not fit the meaning, and visual crowding next to other content.
- For Quantzig decks, run the hex-color sweep in the Slide-by-Slide Validation Pass of `formatting/GUIDE.md` on the finished deck, and confirm: no non-Grandview fonts, no off-palette colours, and every green/amber/red use must be a real metric.
- Run `scripts/office/validate.py` from the pptx skill (with `--original` for template-based decks). For Quantzig decks run the Slide-by-Slide Validation Pass in `formatting/GUIDE.md` as well.
- Read the script's WARNING lines after every call: unknown labels, leftover placeholder text and skipped charts are reported there.

## Files

- `scripts/visuals.py`: inspect, preview, place, render (run with `-h` for all options).
- `references/catalog.md`: every usable library slide by category, with text, icon and image-slot counts, the avoid list and the section dividers.
- `references/formats.md`: SVG recipes and notes for HTML, artifacts and documents.
- `references/fontawesome4-icons.tsv`: FontAwesome 4 icon names and codepoints.
- `assets/visual-library.pptx`: the source library. `assets/sheets/*.jpg`: contact sheets per category. `assets/fontawesome-webfont.ttf`: FontAwesome 4.7 (SIL OFL), used for icon rendering.

## Gotchas

- T#, t# and s# numbers come from the unmodified library slide and stay valid within one `place` or `render` call: work them out with `inspect` or `preview`, then pass everything in one call.
- Some slides pull frame art from their library layout (device mockups, photo frames). It appears as the first T# entries in `inspect`; keep it.
- The placed visual is one group named "Visual L<slide>", so it can be moved and resized as a unit in PowerPoint. Text boxes do not grow with the group; fonts are pre-scaled by the script.
- Library canvas is 10 x 5.625 in. Placing into a 13.33 x 7.5 in deck scales the visual up about 1.3 to 1.45 times, which is why small library fonts still pass the 10.5pt floor.

## Fallback recipes (only when the library files are unavailable)

Build with native shapes in the host deck's colours. n = item count, W x H = content box.
- **Chevron process:** n chevron shapes (first one a pentagon/homePlate), width (W - (n-1)*0.05in)/n, height about 0.9in, number or icon inside, title and 12-word description below each.
- **Cycle:** n circles on a ring of radius r = 0.35*min(W,H), item i at angle -90 + i*360/n degrees, curved arrows (blockArc or arc lines with arrowheads) between them, centre label.
- **Hub and spoke:** centre hexagon or circle, n nodes split into left and right columns, straight connectors, labels on the outer side.
- **Pyramid or stairs:** n stacked trapezoids narrowing upward (or n rectangles stepping up), labels right with leader lines.
- **Funnel:** n stacked trapezoids narrowing downward, labels right.
- **Timeline:** one axis line, milestone circles at date-proportional x positions, date above, text below.
- **2x2 matrix:** two labelled axes, four tinted quadrants, items placed by score.
- **Icon grid:** 2x3 or 3x2 cards, icon badge top-left, bold term then one sentence.

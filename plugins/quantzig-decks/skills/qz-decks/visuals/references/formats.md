# Building visuals outside PowerPoint

Use this when the deck or document is an HTML page, a Slides or Design artifact, a web page, a PDF or a Word/Doc file.

## Choosing redraw vs render

| Visual | HTML / artifact | Word / PDF / Doc |
|---|---|---|
| Process, chevrons, steps, timelines, Gantt | Redraw as SVG (recipes below) | Render PNG |
| Cycles, hub-and-spoke, pyramid, funnel, 2x2, Venn | Redraw as SVG | Render PNG |
| Iceberg, road, tree, umbrella, padlock, head, maps, device mockups, 3D objects | Render PNG and embed | Render PNG |
| Charts with data | Native chart library in the page (Chart.js etc.) | Native chart in the document, or matplotlib PNG |

Render command: `python3 scripts/visuals.py render <slide> [--texts ... --icons ... --drop ... --palette ... --font ...] -o out.png`. Output is cropped to the visual with a white background. For HTML embed as `<img src="data:image/png;base64,...">` with `alt` text that states the content, since the words inside the image are not selectable.

## SVG redraw rules

- Look at the library slide (contact sheet or `preview`) and copy its structure: number of slots, where labels sit, arrows, badge shapes. Do not copy its colours; use the host brand's.
- One `viewBox` sized to the content (for example `0 0 1200 420`), `width="100%"`, and text as real `<text>` or HTML beside the SVG so it stays readable and responsive.
- Colours as CSS variables of the host page (for Quantzig: `--qz-navy:#0B0E5F; --qz-wine:#812B47; --qz-purple:#2C165E; --qz-text:#242424`, and the wine to navy gradient as a `<linearGradient>` from `#812B47` to `#0B0E5F`). Status colours only for small accents.
- Icons: inline SVG paths from a script-only icon source allowed by the page's host (for published artifacts, load a library such as Lucide from cdnjs/jsdelivr as a script and render its icons to SVG), or simple geometric glyphs. Never emoji as icons in client material.
- Fonts: the host brand's font only. For Quantzig that is Grandview (`font-family: 'Grandview', 'Segoe UI', sans-serif` as the fallback stack for machines without it), nothing else.
- Green, amber and red only for metric status (KPI vs target, RAG, deltas), never for decoration.
- Minimum text size about 13px on screen; slot titles one to three words, descriptions about 12 words.

## Recipes (geometry for common families)

Assume n items, content width W, height H, gap g.

**Chevron process (catalog 188, 190, 191).** Item width w = (W - (n-1)*g)/n. Each chevron is a polygon: `x,0  x+w-d,0  x+w,H/2  x+w-d,H  x,H  x+d,H/2` with d = H*0.3 (the first item has a flat left edge). Number or icon inside, title and description below.

**Numbered cards on an arrow (185, 187).** A long arrow band across the full width at mid height; n circles or cards evenly spaced on it; labels below each.

**Snake or S-track (69, 71).** Two or three rows joined by semicircle ends (`A` arcs of radius equal to half the row pitch); stops as circles on the path, labels alternating above and below.

**Cycle (86, 100, 197).** Centre (cx, cy), radius r. Item i at angle a = -90 + i*360/n degrees. Arrows are arc segments between items: `M` at angle a_i + 12, `A r r 0 0 1` to angle a_{i+1} - 12, with a marker-end arrowhead. Central label optional.

**Hub and spoke (225, 226, 228).** Central hexagon or circle; n nodes at radius r evenly spaced (or split left and right columns for 6 items); straight or dotted connectors from centre edge to node edge; labels on the outer side of each node.

**Pyramid or stairs (74, 164, 193).** Level k (0 = top) of n: trapezoid from y = k*h to (k+1)*h with half-widths growing linearly; stairs are rectangles offset by one step width and step height. Labels to the right with leader lines.

**Funnel (151).** Stacked trapezoids narrowing downward, the last one a short rectangle spout; labels to the right.

**Timeline (115, 116).** Horizontal axis line; milestone pins or circles at x positions proportional to dates (not evenly spaced if dates are uneven); date above, text below; current-date marker if relevant.

**Gantt (301).** Grid of months as columns, activities as rows; bars as rounded rectangles from start to end; milestones as diamonds; a vertical "today" line.

**2x2 matrix (59).** Two axes with labels at the ends, four quadrants with a light tint each; items as dots or labels placed by their scores.

**Venn (203).** Three circles of radius r at the corners of an equilateral triangle with side about 1.1r, fill opacity about 0.25; labels outside, overlap label at centre.

**Iceberg (154), when redrawn.** Waterline at about 35% height; a jagged polygon above and a larger one below; levels as dots on a vertical line through the ice with leader lines to labels (above water: symptoms, below: root causes).

## Documents

- Word: insert PNGs at the text width (about 6.3 in on A4 with normal margins) with a caption; follow the docx skill.
- PDF: place PNGs at full column width; follow the pdf skill.
- Claude Doc: upload the PNG and insert it where the section needs it; keep a one-line caption stating the point of the visual.

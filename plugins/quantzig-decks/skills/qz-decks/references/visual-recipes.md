# Visual recipes

Build recipes for each hero visual using native PowerPoint shapes. Colors, fonts, header bands and fill limits come from `formatting/GUIDE.md`. Positions assume a 16:9 slide (13.333 x 7.5 in) and a content area from about 1.4 in to 7.0 in vertically, with 0.5 in side margins. Adjust to the template master's placeholders.

## Contents

1. Shared building blocks
2. Story strip (slide 2)
3. Split panel (slide 3)
4. Pitfall cards and proof strip (slide 4)
5. Chevron journey (slide 5)
6. Layered architecture (slide 6)
7. Stage column cards and tracker (slides 7 and 8)
8. KPI tiles and framed screenshots (slide 9)
9. Swimlane roadmap (slide 10)
10. Cost ladder (slide 11)
11. Pillars, next-step timeline, decision band (slide 12)
12. Case study story band (appendix)
13. Final visual check

---

## 1. Shared building blocks

- **Number badge**: circle (OVAL), 0.4 in, filled with the stage accent color, white bold number at 14 pt. Stage accent colors come from the brand palette only, in this order: navy `0B0E5F`, wine `812B47`, purple `2C165E`, note purple `592258` (for more than four stages, repeat with the brand gradient). Never yellow, orange, blue, green or red as stage colors. This is the one place a stage color may fill a shape, because it is a small semantic accent.
- **Icon**: one consistent line-icon set in one stroke weight. Icons may be inserted as PNG (render at 2x, brand color, transparent background) or built from simple shapes. Place them at 0.45 to 0.6 in. The same stage always uses the same icon.
- **Card**: ROUNDED_RECTANGLE with a small corner radius, white or theme color at 96% transparency, and a thin theme-color border. Use a consistent inner padding of 0.12 in.
- **Big number**: text box, 40 to 60 pt bold in the primary theme color, with a 10 to 12 pt label directly beneath.
- **Tag**: small ROUNDED_RECTANGLE (height 0.28 in), 10 pt text. Use it for "our fix", "we need from you", and future state tags (F1, F2).
- **Connector**: straight or elbow connectors with an arrowhead at the end, 1.25 pt, in a theme color. Glue connectors to shapes so they move together.
- Diagrams must stay native shapes and connectors, never pictures, so the client can edit them.

python-pptx helpers:

```python
from pptx.util import Inches, Pt
from pptx.enum.shapes import MSO_SHAPE, MSO_CONNECTOR
from pptx.dml.color import RGBColor

def badge(slide, x, y, n, rgb):
    s = slide.shapes.add_shape(MSO_SHAPE.OVAL, Inches(x), Inches(y), Inches(0.4), Inches(0.4))
    s.fill.solid(); s.fill.fore_color.rgb = rgb; s.line.fill.background()
    tf = s.text_frame; tf.text = str(n)
    r = tf.paragraphs[0].runs[0]; r.font.size = Pt(14); r.font.bold = True
    r.font.color.rgb = RGBColor(0xFF, 0xFF, 0xFF)
    return s

def arrow(slide, x1, y1, x2, y2, rgb):
    c = slide.shapes.add_connector(MSO_CONNECTOR.STRAIGHT, Inches(x1), Inches(y1), Inches(x2), Inches(y2))
    c.line.color.rgb = rgb; c.line.width = Pt(1.25)
    # Arrowhead: set a:tailEnd type="triangle" on c.line._get_or_add_ln()
    return c
```

## 2. Story strip (slide 2)

- Four equal cards in one row. Each card is 2.9 in wide with 0.2 in gaps, and about 3.2 in tall.
- Each card has an icon at the top left, a label (Problem, Approach, Impact, Ask) at 12 pt bold, and body text at 11 pt.
- In the Impact card, set 2 or 3 big numbers at 36 pt instead of body text.
- Fill the Ask card with the gradient and use white text.
- Place thin right-arrow connectors between the cards.

## 3. Split panel (slide 3)

- Draw an objective banner across the top: a full-width rounded rectangle, 0.6 in tall, holding the objective at 14 pt.
- Below it, two panels, each 5.6 in wide:
  - The left panel is titled "Today". Fill it with a theme color at 96% transparency and set the text in body text `242424`.
  - The right panel is titled "Tomorrow". Give it a white fill and a brand-color border.
- Add 3 to 5 rows per panel, aligned across both panels. Each row is an icon plus one line. The right-hand rows carry F1, F2 tags.
- Between the panels, place a RIGHT_ARROW block (0.8 in wide) in the gradient, vertically centred.

## 4. Pitfall cards and proof strip (slide 4)

- Three cards in a row, each 3.9 in wide. Each card holds:
  - a warning icon,
  - the pitfall at 13 pt bold,
  - the consequence at 11 pt,
  - an "our fix" tag pinned to the bottom edge.
- Proof strip: a 1.1 in band at the slide bottom holding 2 or 3 chips. Each chip has an industry icon, a big number at 28 pt, and a two-line label at 10 pt. Separate the chips with thin vertical lines.

## 5. Chevron journey (slide 5)

- Use one CHEVRON shape per stage (PENTAGON for the first) in a single row, overlapping by about 0.15 in. For 5 stages on 12.3 in of width, each chevron is about 2.6 in wide and 1.1 in tall.
- Give each chevron a white fill with a stage-color border, or a theme color at 96% transparency. Set the stage name inside at 12 pt bold.
- Put the badge and icon above each chevron. Put the "what we do" text below it (2 lines, 10.5 pt).
- Along the top, add an outcome line per stage at 10.5 pt italic with an F tag.

## 6. Layered architecture (slide 6)

- Use columns left to right: Sources, then Ingest, then Store and model, then Serve, then Users. Use 5 columns of about 2.2 in.
- Make each box a small card (about 1.8 x 0.5 in) with the technology name. Technology logos are allowed where the client uses them.
- Wrap each stage's boxes in a dotted rounded rectangle, with the stage badge on its top-left corner.
- Draw a bottom band across the full width (0.5 in) for governance, security and monitoring, split into labelled segments.
- Run flow connectors left to right only. Avoid crossing lines, and reorder boxes to remove crossings. Cap the diagram at about 15 boxes.

## 7. Stage column cards and tracker (slides 7 and 8)

- **Tracker**: across the top, a thin row of all stage badges joined by a line. Current stages keep full color. Other stages drop to 30% opacity.
- **Columns**: one card per stage (2 cards at about 6 in wide each, or 3 cards at about 4 in wide).
- Inside each card, run a vertical flow: input icon, then Objective, then Approach, then output icon, then Output, then Done when.
- Pin a "we need from you" tag at the card base, only where it applies.

## 8. KPI tiles and framed screenshots (slide 9)

- **KPI tiles**: 3 or 4 cards in a row. Each tile holds:
  - an F tag (top left),
  - the metric name (12 pt),
  - the from-to value as a big number (36 to 44 pt, for example "35% to 22-25%"),
  - a basis line (10 pt, note purple `592258`).
- **Screenshots**: place each inside a browser frame, built from a rounded rectangle with a 0.3 in top bar holding three small circles. Add numbered pins (0.3 in circles) on the image, with the matching caption list beside or below it. Crop to the relevant area; do not shrink a full screen until it is unreadable.

## 9. Swimlane roadmap (slide 10)

- Along the top, draw phase bands as rectangles in a theme color at 96% transparency, labelled Crawl, Walk, Run and Support. Band widths are proportional to duration.
- Below the bands, add one lane per stage, 0.45 in tall, with the stage badge at the left. Activity bars are rounded rectangles in the stage's light tint.
- Mark gates with DIAMOND shapes (0.3 in) on the phase boundaries. Beside each gate, add a label for the decision and a "we need" tag.
- Put a deliverables row under the lanes: 3 or 4 icons with short labels per phase.
- For the discovery path, draw a solid discovery block, then a dotted-border Crawl block labelled "indicative".

## 10. Cost ladder (slide 11)

- Draw one rectangle per phase, bottom-aligned. The heights rise left to right and may be proportional to investment when figures are known.
- Draw TBD steps with a dotted border and no fill.
- On each step, add the phase name at the top, the duration, and the investment at 20 to 24 pt.
- Put the team row to the right or below: skill icons with 10 pt labels.
- Place the assumptions strip in a full-width band at the bottom, at 10.5 pt, or as an on-slide note in 11 pt Grandview bold italic `592258`.

## 11. Pillars, next-step timeline, decision band (slide 12)

- **Left 60%**: 4 to 6 pillar cards in a 2x2 or 2x3 grid. Each card is an icon plus a bold title plus one specific line.
- **Right 40%**: a vertical line with 3 to 5 circles. Beside each circle, give the date (bold), the action and the owner. Highlight the last circle (the decision) with the gradient.
- **Footer band**: one full-width decision band stating the decision needed and by when. No contact cards unless real names and details are supplied; the Reach Out layout carries Quantzig's contact details.

## 12. Case study story band (appendix)

- Three connected blocks: Challenge, then What we did, then Result, joined with chevrons or arrows.
- The Result block holds 2 or 3 big numbers.
- An industry icon and an anonymized client descriptor sit top left.
- A mini stage spine (small badges) runs along the bottom, highlighting the stages the work covered.

## 13. Final visual check

- Render every slide to an image (for example, LibreOffice headless to PDF, then to PNG) and inspect it.
- Check for text overflow, overlaps, misaligned rows, connectors that are not glued, and fonts below the floor.
- Confirm each slide passes the hide-the-text test.
- Confirm stage colors and icons match from slide 5 through slide 10.

# Visual vocabulary

Which visual to use for which message, and build recipes for visuals that `references/visual-recipes.md` does not cover. Shared building blocks (number badge, icon, card, big number, tag, connector) and the recipes for story strip, split panel, pitfall cards, chevron journey, layered architecture, stage cards, KPI tiles, framed screenshots, swimlane roadmap, cost ladder, pillars, next-step timeline, contact cards, and case study story band live there. Read that file first. Colors, fonts, and fill limits come from `formatting/GUIDE.md`: Grandview only, whole-point sizes from 10 pt (10.5 allowed), brand colors only, and green, amber and red only on metric status such as the RAG dots, late-task markers and deltas described below. Positions assume a 13.333 x 7.5 in slide.

## Contents

1. Message to visual map
2. Status banner
3. Scorecard
4. This period and next period split
5. RAID table
6. Gantt with today line
7. Funnel and pipeline
8. Heatmap
9. Partnership map
10. Team cards
11. Workshop cards
12. Cadence grid
13. Now, Next, Later columns
14. Maturity ladder
15. Waterfall and before-after bars
16. Capability map
17. Value versus effort 2x2
18. Quote cards

---

## 1. Message to visual map

| Message | Use | Recipe |
| --- | --- | --- |
| Overall summary with an ask | Story strip | visual-recipes 2 |
| Before versus after, today versus target | Split panel | visual-recipes 3 |
| Steps, stages, approach | Chevron journey | visual-recipes 5 |
| How parts connect | Layered architecture | visual-recipes 6 |
| Key numbers | KPI tiles or big numbers | visual-recipes 8 |
| A product or prototype | Framed screenshots with pins | visual-recipes 8 |
| Phases over time | Swimlane roadmap | visual-recipes 9 |
| Proof from past work | Case study story band | visual-recipes 12 |
| Overall health this period | Status banner | 2 |
| Metrics against targets | Scorecard | 3 |
| Done versus planned | This period and next period split | 4 |
| Risks and issues | RAID table | 5 |
| Schedule health | Gantt with today line | 6 |
| Opportunities by stage | Funnel | 7 |
| Many units on a few measures | Heatmap | 8 |
| Who we work with | Partnership map | 9 |
| People | Team cards | 10 |
| Workshops and their inputs | Workshop cards | 11 |
| Meeting rhythm | Cadence grid | 12 |
| Priorities over horizons | Now, Next, Later | 13 |
| Current versus target maturity | Maturity ladder | 14 |
| How value adds up, or change | Waterfall or before-after bars | 15 |
| What we offer | Capability map | 16 |
| How items were prioritized | Value versus effort 2x2 | 17 |
| Client voice | Quote cards | 18 |

## 2. Status banner

- Full-width band under the title, 0.6 in tall, white card with a thin border.
- Left: a large RAG pill (1.4 in wide) with the status word in white bold.
- Middle: one line on why, 12 pt.
- Right: the period ("20 to 24 July") in 10.5 pt body text `242424`.
- Status colors fill only the pill. The band stays white.

## 3. Scorecard

- Table-like grid of cards, one row per metric: metric name, target, actual, trend arrow (up, flat, down), RAG dot, one-line comment.
- Actual in bold at 14 pt. Trend arrows are small native shapes in theme color.
- At most 8 rows on a main slide. Sort by importance, not alphabetically.
- For workstream scorecards, rows are workstreams and columns are scope, schedule, quality, and people, each a RAG dot.

## 4. This period and next period split

- Two columns with a thin divider. Left header "Done this [week or month]", right header "Planned next [week or month]", each with the date range.
- Group bullets by workstream with the workstream name as a bold lead-in.
- A slim strip at the base: "Decisions or help needed" with 1 to 3 items and owners, highlighted with a light tint.

## 5. RAID table

- Columns as in blocks.md section 5. Type shown as a small letter tag (R, I, D, A).
- Status column shows a RAG dot plus a word. Age over 14 days gets an amber tag.
- Header row in the structural color per the formatting guide (`formatting/GUIDE.md`). Row height fixed so 6 rows fit.

## 6. Gantt with today line

- Table grid with task rows and sprint or week columns. Planned span as an outlined bar, progress as a filled bar inside it.
- A vertical dashed line for today, labelled at the top.
- Milestone diamonds on their own row or at bar ends. Client dependency tasks carry a star in the task name.
- Late tasks: amber or red marker at the bar end with a short reason tag.

## 7. Funnel and pipeline

- Horizontal stages left to right (Identified, Qualified, Proposed, Negotiation, Won) as chevrons that narrow in height.
- Each stage shows count and value in big numbers, with 2 or 3 named opportunities in small text underneath.
- A conversion rate tag between stages when known.

## 8. Heatmap

- Grid with units as rows (accounts, workstreams, sites) and measures as columns.
- Cells are small rounded rectangles with RAG fill at low intensity (light tints) and the value in text. Keep status colors light so the text stays readable.
- A final column for trend or comment.

## 9. Partnership map

- Hub and spoke. The client in the center, workstreams or client teams around it as cards, each with team name, what we do in one line, and a small FTE or years number.
- Connectors from hub to each card. At most 8 spokes. Group smaller teams into "Other".
- A band of 3 or 4 big numbers above or beside: teams, FTEs, years, use cases.

## 10. Team cards

- Two groups side by side, Quantzig and client, each with a group label.
- Cards with an initials circle or photo placeholder, name, role, and one line of responsibility.
- Leadership row on top, delivery row below. At most 12 cards per slide.

## 11. Workshop cards

- One card per workshop, up to 4 across. Header with number badge, workshop name, duration, target date.
- Sections inside: Purpose, Attendees, Inputs needed, Outputs. Inputs needed carries a "we need from you" tag.

## 12. Cadence grid

- Rows are forums, columns are frequency, attendees, purpose, output. A small calendar icon per row.
- Optionally a one-row timeline strip of a typical month showing when each forum happens.

## 13. Now, Next, Later columns

- Three columns with headers and date ranges. Items as cards with a short name, one-line value, and a tag (feature, use case, capability, account).
- Confidence decreases left to right: Now cards solid, Next cards lighter, Later cards dashed borders.

## 14. Maturity ladder

- 4 or 5 ascending steps left to right (for example Descriptive, Diagnostic, Predictive, Prescriptive, Autonomous).
- A "You are here" marker on the current step and a "Target" flag on the goal step. Under each step, 1 or 2 lines of what it looks like.

## 15. Waterfall and before-after bars

- Waterfall: native bar chart or shapes, baseline on the left, each driver as a floating bar, total on the right. Label every bar with value and driver.
- Before-after: pairs of bars per metric, before in lavender `D2D0E1`, after in navy `0B0E5F`, with the change as a tag above ("-35%").

## 16. Capability map

- Grid of pillar cards (3 to 6), each with icon, capability name, 2 lines of what it covers, and 2 or 3 tags for tools or accelerators.
- Optional base band listing industries or functions served as icon chips.

## 17. Value versus effort 2x2

- Four quadrants: quick wins (high value, low effort), big bets, fill-ins, deprioritize.
- Items as small numbered circles placed in the quadrants, with a legend at the side. Quadrant labels in the corners.

## 18. Quote cards

- 2 or 3 cards with a large quotation mark icon, the quote in 12 pt, and attribution by role only ("Director, Supply Analytics"). Never a name in external content.

---
name: "qz-decks"
description: One skill for every Quantzig presentation, with storyline, brand formatting, and visuals in one package. It routes the use case to the right deck type and applies its storyline, the real Quantzig slide master and style rules, and a 330-slide visual library. Covers proposals, RFP responses, PoC readouts, pilot pitches, case studies, one-slider proof cards, delivery showcases, phase readouts, kickoff and implementation plans, client MBRs and QBRs, internal reviews for the CEO and board, weekly status reports, roadmaps (analytics, product, platform, account growth, capability), capability showcases, and points of view. Use whenever the user asks for any Quantzig deck, presentation, or slides, describes a client situation that needs a deck, or wants a deck reviewed, fixed, formatted, or QA checked, even if no deck type is named. Researches similar use cases to fill gaps within the given context. Pair with pptx for building the file.
---

# QZ Decks

Every Quantzig deck answers the audience's questions in the order they ask them, with one clear message per slide, one strong visual that carries it, and enough explanation on the slide that it reads without a presenter. No two slides look alike. This skill holds everything needed to build any Quantzig deck type:

| Part | Where | Decides |
| --- | --- | --- |
| Routing, research, shared rules, shared checks | This file | Which deck type, how to fill gaps, rules every deck follows |
| Deck type storyline | `references/types/<type>.md` | Slides, inputs, flex rules, type checks |
| Reusable blocks | `references/blocks.md` | Growth pitch, proof card, RAID, next steps, and other shared slides |
| Hero visuals | `references/visual-recipes.md` and `references/visual-vocabulary.md` | Which visual for which message, and how to build the standard Quantzig hero visuals |
| Visual library | `visuals/GUIDE.md` (with its catalog, contact sheets, 330-slide library, and `scripts/visuals.py`) | Extra diagram families, infographics, icons, and device mockups placed as native shapes |
| Brand formatting | `formatting/GUIDE.md` (with the real slide master in `formatting/assets/quantzig-deck-template.pptx`) | Master and 12 layouts, colors, fonts, content patterns, and the slide-by-slide validation pass |
| File building | pptx skill (separate, standard) | Writing and validating the .pptx |

The user never has to pick a type or call another deck skill. Storyline, formatting, and visuals are all inside this skill. Follow the steps below in order.

## Step 0: Find the full skill bundle (do this first, every session)

Some Claude apps (including Cowork) copy only this SKILL.md into the session and leave `references/`, `formatting/`, and `visuals/` behind in a folder the session cannot read. Everything else in this skill depends on those folders, so locate them before routing.

```bash
LIB=$(find / -name visual-library.pptx -path '*visuals/assets/*' -not -path '/proc/*' 2>/dev/null | head -1)
[ -n "$LIB" ] && ROOT=$(dirname "$(dirname "$(dirname "$LIB")")") && ls "$ROOT"
```

`ROOT` must contain `references/`, `formatting/`, and `visuals/`. All paths in this file are relative to `ROOT`.

If nothing is found:

1. **Check uploads.** Look for `qz-decks.skill` or a zip of the skill in `/mnt/user-data/uploads` (or the session's uploads folder). If present, unpack it and set `ROOT`:
   ```bash
   mkdir -p /tmp/qzd && python3 -c "import zipfile,glob; zipfile.ZipFile(sorted(glob.glob('/mnt/user-data/uploads/qz-decks*'))[0]).extractall('/tmp/qzd')"
   ROOT=$(dirname "$(dirname "$(dirname "$(find /tmp/qzd -name visual-library.pptx | head -1)")")")
   ```
2. **Check connected folders.** The user may keep an unpacked copy of the skill in a folder connected to the session. The `find` above already searches every mounted folder, so if it returned nothing, no connected copy exists.
3. **Ask once, then wait.** Tell the user in two lines that the skill's templates and visual library are not reachable in this session, and ask them to either connect the folder that holds the unpacked `qz-decks` skill or attach `qz-decks.skill` to the chat. Do not build slides while waiting.
4. **Only if the user says to continue without it:** use the fallback storylines at the end of this file and the shared rules, build on the user's uploaded Quantzig deck or template if there is one, draw visuals as native shapes, and state clearly in the reply that the library visuals, master template file, and full type specs were not available.

Never silently fall back to hand-drawn boxes when the bundle is missing.

## Step 1: Route the use case

Read the request and any attachments, then pick one type.

| If the user wants to... | Type file | Typical signals |
| --- | --- | --- |
| Win new scope with full approach and commercials | `proposal.md` | proposal, RFP, SOW pitch, statement of approach |
| Prove what a limited-scope build achieved and pitch a pilot | `poc.md` | PoC, proof of concept, pilot, prototype results, "what we built in 4 weeks" |
| Tell the story of past work as proof | `case-study.md` | case study, success story, reference, one-slider, proof point |
| Read out a finished phase to client leadership | `delivery-showcase.md` | phase readout, delivery showcase, phase 1 results, end of phase review |
| Start a project with the client | `kickoff.md` | kickoff, implementation plan, project launch, onboarding deck |
| Report monthly operations and delivery health to the client | `mbr.md` | MBR, monthly review, monthly business review |
| Report quarterly value and grow the account with the client | `qbr.md` | QBR, quarterly review, partnership review |
| Report the portfolio to the CEO and board | `internal-review.md` | internal review, IBR, board review, delivery review, leadership review |
| Update the client team on a project each week | `weekly-status.md` | weekly status, WSR, weekly update, status report |
| Lay out where a product, analytics program, account, or capability is going | `roadmap.md` | roadmap, release plan, growth plan, capability plan |
| Show what Quantzig can do in an area, or share a point of view | `capability-showcase.md` | capability deck, offering deck, solution overview, POV, credentials |

Routing rules:

- **Read only the chosen type file** (plus `proposal-slide-specs.md` for proposals). Do not load the others.
- **Ask once when two types fit equally.** For example, "a deck on Phase 1" could be a delivery showcase or a QBR. Offer both with one line on how they differ. If the user does not answer, pick the closer fit and say so.
- **Combine with blocks, not storylines.** A secondary purpose is handled by inserting a block from `references/blocks.md` into the main type. A QBR with a new use case pitch is the QBR storyline plus the Growth pitch block. A PoC that needs proof adds a Proof card.
- **No matching type** (for example a town hall or a vendor evaluation): use the universal spine below, keep to 10 slides, and tell the user which structure you used.
- **Review mode.** When the user shares an existing deck to fix, route by what the deck is for, map each existing slide to the type storyline, and list what is missing, duplicated, or belongs in the appendix before changing anything.

### Universal spine

1. Cover with an outcome title.
2. Executive summary that stands alone.
3. Context: what is true today and why it matters now.
4. to n-2. The core: findings, options, or work, one message per slide.
n-1. What it means: value, decision, or recommendation.
n. Next steps with owners and dates, and the ask.

## Step 2: Gather inputs, then ask clarifying questions with options

Read everything already available first: the conversation, attachments (decks, SOWs, Excel trackers, notes), and past conversations or memory about the client and project. Teams often track data in Excel: ask for the tracker if it exists, but never block on it.

Then **always run one round of clarifying questions before the storyboard**, even when the request looks complete. Every question offers 2 to 4 tappable options plus room for a free answer:

- **Claude.ai chat:** use the `ask_user_input_v0` tool (up to 3 questions per call).
- **Cowork and Claude Code:** use the `AskUserQuestion` tool.
- **No question tool available:** write the questions as a short numbered list with lettered options (a, b, c) and a recommended default for each, so the user can reply "1b, 2a, 3c".

Rules:

- Ask only what changes the storyline, the visuals or the content, and never ask for something already given in the conversation, attachments or memory.
- At most 3 questions per round and at most 2 rounds. Put the most decisive question first.
- Options must be concrete and specific to this request (real audiences, real decisions, real slide counts), never "Other" or "None"; mark the option you would pick as "(recommended)".
- After the answers, restate in one or two lines what you will build, then move on. If the user skips a question, use the recommended option and say so in the storyboard.

Question bank (pick the 3 that matter most for this request):

| Topic | Example question | Example options |
| --- | --- | --- |
| Audience | Who will read this deck? | Client leadership / Client working team / Quantzig CEO and board / Prospect who does not know us |
| Goal | What should the audience do after reading it? | Approve a pilot / Fund the next phase / Accept the plan and dates / Stay informed |
| Deck type (when two fit) | Is this a phase readout or a quarterly review? | Delivery showcase / QBR |
| Length | How long should the deck be? | Short, 6 to 8 slides / Standard, 10 to 12 / Full, 12 plus appendix |
| Emphasis | What should get the most space? | Business value and numbers / Solution and architecture / Plan, team and cost / Proof from past work |
| Evidence | What numbers can we use? | Client figures I will share / Benchmarks from research / Estimates marked as estimates |
| Naming | Can we name the client? | Yes, client-facing deck / No, anonymise for external use |
| Research | Can I fill gaps with researched benchmarks and practice? | Yes, tag every source / Only for context slides / No, use placeholders |

## Step 3: Research the gaps

Research is **mandatory, not optional**, whenever the inputs are not enough to write a slide that meets the density rule (90 to 160 words, understandable without a voice-over). Check this slide by slide against the storyboard: any slide that would be thin, generic or full of placeholders triggers a search on similar use cases (same industry, function and problem type) before drafting it. Use `web_search` and `web_fetch` (or the session's search tool), run several targeted searches rather than one broad one, and read the actual sources rather than relying on snippets. Skip research only if the user chose "No, use placeholders" in Step 2.

Everything research adds follows **every** instruction in this skill and in the user's request, exactly as user-supplied content does: the stated scope, the deck type's storyline, the brand rules (Grandview, whole-point sizes from 10, brand colours), the writing rules (plain words, no em dashes, no contractions), the density and layout-variety rules, and the anonymization rules. Research never changes the storyline the user confirmed; it only fills it.

### Where to look, in order

1. The user's own material: attachments, earlier decks, trackers, and past conversations.
2. Quantzig's own proof: case studies, solution decks, and capability material the user has shared or that appear in past conversations.
3. Public sources through web search: industry reports, analyst and consulting research, vendor and platform documentation, reputable news, regulatory or government data, and published case studies from similar companies. Prefer sources from the last 3 years.

### What research may fill

| Gap | Examples of what research can add |
| --- | --- |
| Industry and market context | Market shifts, regulatory changes, competitor moves, why the problem matters now |
| Typical pain points | Common failure points for this problem in this industry |
| Typical approach and architecture | Standard methods, model types, platform patterns, data sources usually used |
| Benchmarks and ranges | Typical accuracy, savings, adoption, or time-to-value ranges from comparable programs |
| KPIs | The metrics this function normally tracks |
| Plans and effort | Typical phase lengths, team shapes, workshop themes, go-live steps |
| Risks and dependencies | What usually slows similar projects |
| Growth ideas | Adjacent use cases companies in the same industry pursue |

### Boundaries (never cross these)

- **Stay inside the stated scope.** Research sharpens what the user described. It never adds new workstreams, deliverables, geographies, or commitments the user did not mention. Adjacent ideas go into a Growth pitch block or the appendix, labelled as ideas.
- **Never present research as client fact.** Client baselines, client results, client quotes, dates, names, budgets, and pricing come only from the user. Research can give a benchmark range next to a client placeholder, never replace it.
- **Never present research as Quantzig's own results.** A published result from another company is a benchmark, not a Quantzig proof point. Quantzig proof comes only from Quantzig material.
- **Match the context.** Use research from the same industry, function, and problem type where possible. If only a neighbouring industry is available, say so in the label.
- **No weak sources.** Skip anonymous blogs, vendor marketing claims without data, and anything that cannot be cited.

### How researched content is marked

- On the slide: a small tag or footnote such as `Benchmark: [source, year]` or `Industry practice: [source]`. Ranges, not single points, for benchmarks.
- In speaker notes: the full source list for that slide.
- In the reply to the user: a short "Research added" list with each item, the slide it is on, and the source, so they can verify or remove it before sharing.
- If research finds nothing reliable, keep the placeholder and say what is missing.

## Step 4: Storyboard first (story, visual and layout for every slide)

Before building anything, write a storyboard table and show it to the user. It has one row per slide:

| # | Title (a conclusion) | Role in the story | Hero visual | Layout structure | Key content |
| --- | --- | --- | --- | --- | --- |

- **Title:** the slide's conclusion, 14 words or fewer.
- **Role in the story:** why this slide comes next (sets context, shows the problem, explains the approach, proves it, asks for the decision). Read the titles top to bottom: they must tell the whole story on their own, with no jumps and no repeats.
- **Hero visual:** chosen before any body copy is written, from `references/visual-recipes.md`, `references/visual-vocabulary.md` or the library (`visuals/GUIDE.md`). Pick the visual from what the slide's information is (a sequence, a loop, a comparison, a hierarchy, numbers against a target), then write the copy into and around it.
- **Layout structure:** one entry from the Layout menu under Shared rules. **No two slides share a structure.**
- **Key content:** the points the slide must carry, enough to meet the density rule.

Mark which slides rely on research or placeholders. Confirm with the user before building. This is the cheapest point to change direction. For routine repeat decks (a weekly status built from last week's), show the storyboard and flag only what changed.

## Step 5: Build, then validate

Build in this order:

1. **Formatting first.** Read `formatting/GUIDE.md` and its references. Build every slide on one of the 12 real layouts from `formatting/assets/quantzig-deck-template.pptx`, so logo, footer, and header chrome are inherited, never hand-placed. Reuse its nine content patterns where they fit.
2. **Hero visuals.** Build each slide's hero visual with `references/visual-recipes.md` or `references/visual-vocabulary.md`.
3. **Visual library when needed.** When a slide needs a diagram family those recipes do not cover (cycles, pyramids, hub and spoke variants, puzzles, Venn, maps, device mockups, metaphors), or the user asks for a more visual deck, follow `visuals/GUIDE.md` to pick from the library and place it as native shapes.
4. **Validate.** Run `formatting/scripts/deck_check.py` and the Slide-by-Slide Validation Pass in `formatting/GUIDE.md`, the shared checklist below, and the type file's checklist. Fix failures.

## Step 6: Final slide-by-slide review (always, before delivering)

Render every slide and look at each one in order. For each slide, confirm and record:

| # | Story | Content | Visual | Formatting | Feedback applied |
| --- | --- | --- | --- | --- | --- |

- **Story:** the title is a conclusion and follows from the slide before; the deck reads as one argument from cover to ask.
- **Content:** a reader who was not in the room understands the slide without a voice-over; every visual element is labelled and explained; nothing is a placeholder unless marked.
- **Visual:** the hero visual is where the eye lands first, is large enough to carry the point, and is not the same structure as any other slide; icons on cards and list items.
- **Formatting:** `deck_check.py` is clean for the slide (Grandview only, whole-point sizes from 10, 10.5 allowed, brand colours, status colours only on metrics, no thin or empty slides); no overlap, overflow or clipped text; shapes aligned and symmetric.
- **Feedback applied:** every piece of user feedback from this conversation is reflected on the slides it concerns.

Fix every failure and re-render the fixed slides before delivering. Give the user the table in the reply, followed by what still needs them: placeholders, research to verify, and approvals.

## Shared rules

### Titles and messages

- **Titles are conclusions.** "Truck Utilization Rose 7%, Saving $6.8M a Year", not "Results". Title Case with "&" instead of "and", 14 words or fewer.
- A subtitle may add one line of support in sentence case, stating the evidence or the so what.
- **One message per slide.** If a slide needs two titles, it is two slides, or one belongs in the appendix.
- The executive summary is written last and must stand alone if forwarded.

### Words

- Plain, human sentences in the client's language. Full words instead of contractions. No filler or buzzword stacks.
- No em dashes, middle dots, or arrow characters anywhere in slide copy.
- Titles in Title Case with "&" instead of "and". Kickers, bullets, and notes in sentence case.
- Copy fills its box: no panel with more than about 0.45 in of unused height. Add substance or shrink the box.
- **Every slide stands on its own.** A reader who was not in the room must understand it without a presenter. Content slides carry 90 to 160 words (up to 220 on deep dives, never under 70), spread across the hero visual's labels and the supporting panels, not a wall of text. Every element in a visual gets a short label plus a one-sentence explanation of what it means for this audience.
- **End each content slide with its takeaway:** a one-line "so what" band or callout at the bottom, in plain words, so the point survives if the slide is forwarded alone.
- Notes and footnotes carry only an assumption, basis, caveat, or disclaimer, never commentary about the deck itself.
- No placeholder contacts. Close with the Reach Out layout.
- Bullets start with a bold lead-in and a colon, then one plain sentence.

### Numbers

- Every number has a basis: measured, client-reported, benchmark (with source), pilot, or estimate.
- Use ranges when there is no measured baseline. Write "baselined in discovery" when today's value is unknown.
- The same number is identical everywhere it appears.
- Estimate logic goes in the appendix.
- Never invent client figures, names, dates, or quotes. Missing client facts become clearly marked placeholders such as `[FTE count: to confirm]`, listed for the user at the end.

### Anonymization

- External and reusable content (case studies, proof cards, capability decks, anything leaving the account it came from) never names a client without written approval.
- Use a descriptive hint instead: region, size, and what they do. "An EU-based sports goods and apparel manufacturer", "a top-10 global biopharma company". See the hint guide in `references/blocks.md`, section 12.
- Also remove client logos, identifying product names, people's names, and screenshots with client branding or data.
- Client-facing decks for that same client (MBR, QBR, kickoff, weekly status, showcase) use the client's name normally.

### Slide caps

Each type file has a cap. Treat it as a target with a tolerance of about 2 slides, except where the type says hard cap. Never add a slide just to fit content. Cut, merge, or move it to the appendix. Method, raw tables, and long lists always go to the appendix.

### Visuals

- **Visual first.** Every content slide is built around one strong hero visual, chosen from the information the slide carries (sequence, loop, comparison, hierarchy, flow, numbers against a target, geography, product screens). The content lives inside and around the visual: labels, numbers and explanations sit on the diagram itself, not in a separate list beside a small picture.
- **Size and position.** The hero visual takes about 45 to 65% of the content area and sits where the eye lands first (top or left). Supporting panels, big-number callouts and the takeaway band fill the rest.
- **Stronger elements.** Icons on every card and list item; numbers as big-number callouts, not buried in sentences; connectors, badges and numbered steps to show order and cause; device frames around screenshots with numbered callouts.
- **No empty areas.** Shapes cover at least about 70% of the content area on every content slide; no large blank region between the visual and the footer.
- **One visual system:** `references/visual-recipes.md` first, then `references/visual-vocabulary.md`, then the library in `visuals/GUIDE.md` for families neither covers, and the library whenever the deck needs more variety. Native shapes and connectors only, so the client can edit.
- Tables on at most two main slides, unless the type file allows more (status and review decks do). A table still gets a visual element (icons in the first column, status dots, a highlighted row with a callout).
- Mockups and screens not from a live build carry an "Illustrative" tag.

### Layout menu (no two slides share one)

Pick a different structure for every content slide. Cover, closing and section dividers are exempt. Where a type file requires identical repeated pages (account one-pagers, proof cards), keep the frame but change the hero visual on each where the content allows, and say so in the storyboard.

| Structure | Shape of the slide |
| --- | --- |
| Visual left, explanation panels right | Diagram 60% left, 2 or 3 stacked icon panels right |
| Full-width flow with detail below | Chevrons, steps or timeline across the top, a card per step below |
| Hub and spoke | Centre concept with 4 to 6 explained nodes around it |
| Cycle | Loop of 4 to 6 stages with text at each stage and a centre label |
| Pyramid or staircase with side labels | Levels on the left, a label and explanation per level on the right |
| Split comparison | Two halves (today vs future, option A vs B) with a bridge or arrow between |
| 2x2 matrix | Quadrants with items plotted and a legend panel |
| Big-number dashboard | 3 to 5 KPI tiles on top, a chart or explanation panel below |
| Chart with annotations | One native chart, 60% wide, with callouts pinned to data points and a findings panel |
| Architecture or data flow | Layered diagram with numbered components and a component legend |
| Device or screen showcase | Screenshot in a frame with numbered callouts and a caption panel |
| Swimlane roadmap or Gantt | Lanes by workstream, bars by period, milestones, a legend |
| Funnel or filter | Stages narrowing, a number and explanation per stage |
| Metaphor illustration | Iceberg, road, bridge or house with labels on the illustration |
| Table with visual layer | A table with icons, status dots or highlighted rows and a callout box |
| Pillars | 3 to 5 columns under a shared roof or header, each with icon, title and explanation |
| Map | Geography with markers and a side panel of facts |
| Quote or voice cards | 2 or 3 quote cards with roles and a synthesis panel |

## Shared validation checklist

- [ ] The deck type matches the purpose and audience. Secondary purposes use blocks, not extra storylines.
- [ ] Slide count is within the type's cap and tolerance. Detail sits in the appendix.
- [ ] Every title is a conclusion. The executive summary stands alone and states the ask or decision.
- [ ] Every slide has one hero visual that carries the point, chosen from the slide's information and taking about 45 to 65% of the content area.
- [ ] No two content slides share a layout structure, and no library visual is used twice.
- [ ] Every content slide reads without a voice-over: 90 to 160 words (never under 70), labelled and explained visual elements, a takeaway line.
- [ ] No large empty areas: shapes cover at least about 70% of each content slide's content area.
- [ ] The titles, read in order, tell the whole story with a logical flow from context to ask.
- [ ] The Step 6 slide-by-slide review table is complete and given to the user.
- [ ] Every number has a basis and matches everywhere it appears. No invented client figures.
- [ ] A clarifying round with options was asked before the storyboard (or the user's skipped answers were defaulted and stated).
- [ ] Every slide that would otherwise be thin was researched; researched content stays within the stated scope and all instructions, is tagged with its source on the slide, and is listed for the user.
- [ ] No research is presented as a client fact or as a Quantzig result.
- [ ] Placeholders are clearly marked and listed.
- [ ] Anonymization is correct for the audience.
- [ ] The deck ends in action: next steps with owners and dates, a decision, or an ask.
- [ ] No em dashes, middle dots, arrows, contractions, filler, buzzwords, meta-commentary, or placeholder contacts.
- [ ] Grandview for every run. Font sizes are whole points from 10 pt, with 10.5 as the only half size. On-slide notes are 11 pt Grandview bold italic centred in `592258`. Brand colours only; green, amber and red only on metric status. `formatting/scripts/deck_check.py` prints CLEAN apart from confirmed STATUS lines.
- [ ] Every slide sits on a layout from the Quantzig master, and the Slide-by-Slide Validation Pass in `formatting/GUIDE.md` passes (palette sweep, font floors, overflow, collisions, cross-slide alignment). Render and visually inspect every slide.

## Fallback storylines (only when the bundle is unreachable and the user says continue)

Short versions of the type files. Use the full files in `references/types/` whenever they are available.

| Type | Slides |
| --- | --- |
| Proposal (12, hard) | Cover; Executive summary (Problem, Approach, Impact, Ask); Where you are vs where you want to be; What usually goes wrong; How we get you there (stages); How it fits together (architecture); Inside the solution (2 slides); What you get; Roadmap and deliverables; Investment and team; Why Quantzig and next steps |
| PoC (12) | Cover; Executive summary; Objective and success criteria; Scope and data; Approach; How it works; Results against criteria; What it looks like; What we learned; Pilot proposal; Team and what we need from you; Next steps and decision |
| Case Study (6, or 1-slide proof card) | Cover; Result at a glance; The challenge; What we did; How it works; What changed |
| Delivery Showcase (12) | Cover; Phase in numbers; Where we started; What we delivered; Insights 1 to 3; The value; What changed; What needs attention; The next phase; Next steps and decisions |
| Kickoff (12) | Cover; What we will agree today; Context and vision; Objectives and success metrics; Scope; Architecture; Delivery plan; Team and roles; Discovery workshops; Governance and cadence; Risks and dependencies; Next two weeks |
| MBR (6) | Cover; Month at a glance; Delivery scorecard; Delivered and next; Risks, issues, and decisions; Team and capacity |
| QBR (8) | Cover; Quarter at a glance; Our partnership; Value delivered; What we delivered; An idea worth exploring; Looking ahead; Your feedback and next steps |
| Internal Review (8 plus 1 per account) | Cover; Executive summary; Portfolio health; Growth; What worked and what did not; People and delivery health; Risks and escalations; Next quarter plan and asks; Account one-pagers |
| Weekly Status (4) | Cover; Status on a page; Risks, issues, and challenges; Timeline |
| Roadmap (10) | Cover; Executive summary; Where we are today; Where we are going; How we prioritized; The roadmap; What each horizon delivers; Value and milestones; What it takes; Decisions and next steps |
| Capability Showcase (10) | Cover; Why this matters now; What usually goes wrong; What we offer; How we do it; Under the hood; See it in action; Proof; Where it applies; Ways to start |

Formatting essentials without the bundle: Quantzig palette (navy `0B0E5F`, wine `812B47`, body text `242424`, note purple `592258`); gradient `812B47` to `0B0E5F` for header bars; Grandview for all text; whole-point sizes from 10 pt (10.5 allowed); green, amber and red only on metric status; logo and footer only from the master of the user's Quantzig file.

## Reference files

- `references/types/`: one file per deck type (proposal, poc, case-study, delivery-showcase, kickoff, mbr, qbr, internal-review, weekly-status, roadmap, capability-showcase), plus `proposal-slide-specs.md`. Read only the one chosen in step 1.
- `references/blocks.md`: reusable blocks, RAG definitions, anonymization hint guide, appendix rules. Read when a type file points to a block or a deck needs a secondary purpose.
- `references/visual-recipes.md`: build recipes for the core visuals (story strip, split panel, chevrons, architecture, KPI tiles, screenshots, swimlane, cost ladder, pillars, timelines, story band). Read before building.
- `formatting/GUIDE.md`: Quantzig brand formatting, the 12 layouts, nine content patterns, common pitfalls, and the Slide-by-Slide Validation Pass. Its `references/` hold the master and layout catalog, style guide, and slide patterns; `assets/` holds the real template. Read before building any slide.
- `visuals/GUIDE.md`: how to pick and place visuals from the 330-slide library with `scripts/visuals.py`, including the category catalog, contact sheets, FontAwesome icons, and fallback recipes. Read when a slide needs a visual beyond the standard recipes.
- `references/visual-vocabulary.md`: message-to-visual map and recipes for status and review visuals (status banner, scorecard, RAID, Gantt, funnel, heatmap, partnership map, workshop cards, cadence grid, now next later, maturity ladder, waterfall, capability map). Read before building.

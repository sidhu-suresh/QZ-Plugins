# Reusable blocks

Blocks are slides or slide groups that several deck types share. A type skill names the block it needs. Blocks are also how a deck takes on a secondary purpose without adopting a second storyline.

## Contents

1. Executive summary strips
2. Growth pitch
3. Proof card (one-slide case study)
4. What we need from you
5. RAID (risks, assumptions, issues, dependencies)
6. Next steps
7. Team and governance
8. Workshop inputs
9. Plan versus actual
10. Feedback prompts
11. RAG definitions
12. Anonymization hint guide
13. Appendix rules

---

## 1. Executive summary strips

A four-tile strip read left to right, each tile with an icon, a label, and one or two lines. The last tile is highlighted with the gradient. Pick the variant by deck type.

| Variant | Tiles | Used by |
| --- | --- | --- |
| Pitch | Problem, Approach, Impact, Ask | proposal, poc (pre-results), capability-showcase |
| Result | What we tested or did, What we found, What it means, What we propose | poc, delivery-showcase, case-study |
| Status | Overall status, Highlights, Watch-outs, Decisions or asks | mbr, weekly-status, internal-review |
| Value | Value delivered, Highlights, What is next, How you can help | qbr |
| Direction | Where we are, Where we are going, What it takes, The ask | roadmap |

Rules: the impact or value tile shows 2 or 3 big numbers instead of prose. The last tile is always an action for the audience.

## 2. Growth pitch

One or two slides that suggest what more Quantzig can do for the same client or line of business. Used in QBRs, delivery showcases, PoCs, and optionally MBRs. The tone is a suggestion from a partner who knows their business, not a hard sell.

Pick one form:

| Form | When | Content |
| --- | --- | --- |
| Use case extension | The current work unlocks an adjacent problem | Opportunity observed, idea, how it works, value estimate, first step |
| Case study proof | We solved the same problem elsewhere | Proof card (block 3) plus one line on relevance |
| Point of view | A trend or shift affects their business | The shift, what it means for them, what leaders do about it, where to start |

Slide 1 (always):
- **Title**: the opportunity as a conclusion. "Line-Level RCA Could Cut Downtime Analysis From Hours to Minutes".
- **Left**: what we observed in their business, in their words (a pain, a manual step, a data asset not used).
- **Right**: the idea in one sentence, 3 icon steps of how it works, and 2 or 3 value tiles with basis.
- **Base**: the first step, small and time-boxed (a 2-week discovery, a demo, a 6-week PoC).

Slide 2 (optional): a sample output, flow diagram, or framed prototype screen marked "Illustrative".

Never include pricing in a growth pitch inside a review deck. Offer a follow-up conversation instead.

## 3. Proof card (one-slide case study)

Used standalone, in proposals, PoCs, capability showcases, and growth pitches.

- **Header**: anonymized client descriptor and industry icon.
- **Story band**: three steps left to right, Challenge, What we did, Result. Two lines each.
- **Result**: 2 or 3 big numbers with labels and basis.
- **Footer strip**: tech or method tags, duration, team size (optional), and one line "Why this matters for you" when used inside a pitch.

## 4. What we need from you

A slide or strip listing client dependencies. Used in kickoffs, PoCs, proposals, and roadmaps.

- Group by type: people and time (SME hours, workshop attendance), data and access, decisions and approvals, environments and tools.
- Each item has an owner (role, not only a name), a needed-by date or phase, and the impact if late.
- Visual: 4 icon columns or a tagged list. Flag items on the critical path with a star.

## 5. RAID

Risks, assumptions, issues, and dependencies. Used in weekly status, MBR, kickoff, and internal reviews.

| Column | Rule |
| --- | --- |
| Item | Short name, 6 words or fewer |
| Type | Risk, Issue, Dependency, or Assumption |
| Impact | What happens to scope, time, or quality if it is not resolved, in one line |
| Owner | Named person and side (Quantzig or client) |
| Due | A date, never "ASAP" |
| Status | Open, In progress, Escalated, or Closed, with RAG dot |
| Age | Days open. Items open more than 14 days are highlighted |

Rules: show at most 6 rows on the main slide, sorted by impact. Move the rest to the appendix. Scope creep is logged as an issue with its impact on timeline stated. Closed items appear once in the week they close, then drop off.

## 6. Next steps

A vertical or horizontal timeline of 3 to 5 steps. Each has an action verb, owner, and date. End with a decision or a milestone, not an activity, shown as a full-width decision band. Never add contact cards unless real names and details are supplied; the Reach Out closing layout carries Quantzig's contact details.

## 7. Team and governance

- **Team**: cards for both sides (Quantzig and client). Each card has role, name, and one line on responsibility. Group by leadership, delivery, and client SMEs. Headcounts and rates never appear in client decks.
- **Governance**: a cadence grid. Rows are forums (daily stand-up, weekly status, fortnightly demo, monthly steering), columns are frequency, attendees, purpose, and output.
- **Escalation path**: three levels, each with who and the trigger.

## 8. Workshop inputs

Used in kickoffs and discovery phases. The number and themes of workshops vary by project. Common themes: design and personas, data and architecture, AI use cases, solution finalization and roadmap, UAT and go-live.

For each workshop, one card:
- Purpose in one line.
- Attendees needed (roles).
- Inputs we need before or during (data samples, current reports, process maps, access).
- Outputs we will produce (signed-off personas, data map, prioritized backlog).
- Duration and target date.

Show up to 4 workshops on one slide as cards. More than 4 means splitting into two slides or grouping by phase.

## 9. Plan versus actual

Used in weekly status, MBR, and kickoff updates.

- Gantt by task or sprint with a vertical "today" line.
- Planned bar outline plus actual progress fill. Late tasks carry an amber or red marker.
- Client dependency tasks carry a star.
- Milestones as diamonds, filled when done, hollow when upcoming, red outline when at risk.
- One line above the chart: "On track for [milestone] on [date]" or "[milestone] moves from [date] to [date] because [reason]".

## 10. Feedback prompts

Used in QBRs. Feedback is gathered in the conversation, so the slide invites it rather than reporting a survey.

- Title that invites: "What would make the next quarter more valuable for you?"
- 3 or 4 prompt cards, for example: what is working well, what we should do differently, where you see the next priority, how we can make your team's life easier.
- If the client gave feedback earlier (email, previous QBR, stakeholder conversations), show 2 or 3 short quotes or themes and what we did about each ("You said, we did").

## 11. RAG definitions

Default definitions. Use the client's or project's own if they exist, and state them in a footnote the first time RAG appears.

| Status | Meaning |
| --- | --- |
| Green | On plan. No open risk threatens the next milestone. |
| Amber | A milestone is at risk, or a dependency is overdue, but it is recoverable within the current phase with the actions shown. |
| Red | A milestone has been missed or will be missed without a client decision, added capacity, or escalation. |

Rules: every Amber or Red status states the reason in one line and the recovery action. Status never jumps from Green to Red without explanation.

## 12. Anonymization hint guide

Build the descriptor from three parts: where, how big, what they do.

| Part | Examples |
| --- | --- |
| Where | EU-based, US-headquartered, APAC, global, Middle East |
| How big | Fortune 500, top-10 global, mid-sized, multi-billion dollar, operating in 50+ countries |
| What they do | sports goods and apparel manufacturer, biopharma company, brewer, energy and mobility company, frozen food manufacturer, family entertainment operator, coffee chain |

Examples: "an EU-based sports goods and apparel manufacturer", "a top-10 global biopharma company", "a global brewer", "a Middle East family entertainment operator", "a global energy and mobility company".

Also anonymize: product and brand names that identify the client, internal project names that are public, people's names, screenshots with client logos or data. Keep industry, region, scale, and method, because they make the proof credible.

## 13. Appendix rules

- The appendix starts with a divider slide.
- Order: detailed method, data and architecture detail, detailed tables, long lists (contacts, outreach, resource feedback), assumptions, glossary.
- Every appendix slide is referenced from a main slide ("see appendix: model features").
- Appendix slides follow the same title and formatting rules. They are allowed to be denser.

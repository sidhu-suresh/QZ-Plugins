# Kickoff

A kickoff deck turns a signed scope into a shared plan. By the end of the meeting, the client team should agree on the outcome, the scope, the plan, who does what, what they must provide, and what happens in the next two weeks. The deck is a working document for the room, so it favors clarity over persuasion.

## Workflow

1. Collect inputs, then research the gaps (SKILL.md, step 3). Pull from the SOW, proposal, and any earlier solution deck.
2. Decide the workshop set. The number and themes of workshops vary by project. Choose from the common themes in `references/blocks.md`, section 8.
3. Draft the storyline with conclusion titles and confirm.
4. Build, then validate.

## Inputs

| Input | Options | What it changes |
| --- | --- | --- |
| Context and pain | Free text | Slide 3 |
| Vision and objectives | Free text | Slides 3 and 4 |
| Success metrics | With baseline / Baseline to be set in discovery | Slide 4 |
| Scope | Features or use cases, in and out of scope | Slide 5 |
| Delivery model | Single phase / Releases / Crawl, Walk, Run | Slides 5 and 7 |
| Architecture | Known stack / Recommended stack | Slide 6 |
| Team | Quantzig and client names and roles | Slide 8 |
| Workshops | 1 to 4, themes vary | Slide 9 |
| Governance | Client's existing forums / Propose new | Slide 10 |
| Known risks and dependencies | Free text | Slide 11 |

## Storyline (cap 12, tolerance 2)

| # | Slide | Client team question | Hero visual |
| --- | --- | --- | --- |
| 1 | Cover | What project is this? | Cover with project name, "Implementation Plan", date |
| 2 | What we will agree today | Why are we here? | Four-tile strip: outcome, scope, plan, next two weeks |
| 3 | Context and vision | Why are we doing this? | Split panel: today's pain versus the vision, with a bridge arrow |
| 4 | Objectives and success metrics | How will we know it worked? | 3 or 4 KPI tiles with target and baseline or "baselined in discovery" |
| 5 | Scope | What exactly are we building? | Feature scope grid by release or phase, with an out-of-scope strip |
| 6 | Architecture | How will it be built? | Layered architecture from sources to users |
| 7 | Delivery plan | When do we get what? | Swimlane or release train with milestones, UAT, and go-live |
| 8 | Team and roles | Who does what? | Team cards for both sides plus a light RACI strip for key decisions |
| 9 | Discovery workshops | What do you need from us, and when? | Workshop cards with purpose, attendees, inputs needed, outputs |
| 10 | Governance and cadence | How will we work together? | Cadence grid plus a three-level escalation path |
| 11 | Risks, dependencies, and assumptions | What could slow us down? | RAID table with top 6 items |
| 12 | Next two weeks | What happens right after this meeting? | Next-steps timeline with owners and dates |
| A | Appendix | Detail | Detailed feature scope, user journey, UAT and go-live support needs, workshop agendas |

### Slide notes

- **What we will agree today**: this replaces a text agenda. It tells the room what decisions the meeting should produce.
- **Objectives and success metrics**: metrics are business outcomes, not deliverables ("coverage lookup in under 2 minutes", not "dashboard live").
- **Scope**: each release or phase lists features as short cards. Items to be scoped in workshops carry a "to be scoped" tag. Out of scope is explicit.
- **Delivery plan**: note the key assumption that drives timing ("timelines assume data access on day 1") under the chart.
- **Team and roles**: include the client SMEs and decision owners, not only Quantzig. RACI covers 4 to 6 key decisions (scope sign-off, data access, UAT sign-off, go-live).
- **Discovery workshops**: one card per workshop. Inputs needed carry a "we need from you" tag with a date. If there are more than 4 workshops, split by phase.
- **Governance**: show forums that exist in the client's calendar where possible rather than inventing new meetings.

## Flex rules

- Small project (under 8 weeks): merge slides 5 and 6, and merge slides 10 and 11.
- Scope still open: slide 5 shows scope themes to be finalized in workshops, and slide 7 shows the discovery period in detail with an indicative build period after it.
- Client already knows the context well (follow-on project): slide 3 becomes one strip on slide 2, and the freed slide goes to a user journey.
- UAT and go-live support needs are large: add a slide after 9 using the What we need from you block.

## Validation checklist

- [ ] Every success metric is a business outcome with a target or a clear baselining plan.
- [ ] Scope states what is out, not only what is in.
- [ ] Every workshop has inputs needed with owners and dates.
- [ ] Client roles and decision owners are named, not only Quantzig's team.
- [ ] Risks and dependencies have owners and due dates.
- [ ] The deck ends with the next two weeks, with owners and dates.

# Weekly Status

The client team reads the weekly status in two minutes. They want four answers: what happened, what is next, what is in the way, and are we on time. The deck is short, repeatable, and consistent week to week, so changes stand out.

## Workflow

1. Collect inputs, then research the gaps (SKILL.md, step 3). Ask for last week's status deck and the tracker if they exist. Reuse last week's deck as the base: roll dates forward, move "planned" to "done" where complete, and update the RAID and plan.
2. Set the overall status using the RAG definitions in `references/blocks.md`, section 11.
3. Build, then validate. For a routine week, a confirmed storyline is not needed; show the draft and flag only what changed.

## Inputs

| Input | Options | What it changes |
| --- | --- | --- |
| Project and week dates | Free text | Cover, slide 2 |
| Done last week | Per workstream | Slide 2 |
| Planned next week | Per workstream | Slide 2 |
| Overall status and reason | Green / Amber / Red | Slide 2 |
| Decisions or help needed | Item, owner, by when | Slides 2 and 3 |
| Risks, issues, challenges | RAID items, including scope changes | Slide 3 |
| Plan progress | Tracker, or per task: done, on track, late | Slide 4 |
| Last week's deck | Available / Not available | Base for the update |

## Storyline (cap 4, hard cap 5)

| # | Slide | Client team question | Hero visual |
| --- | --- | --- | --- |
| 1 | Cover | Which project and week? | Cover with project name, "Weekly Status Report", and the week |
| 2 | Status on a page | Where are we? | Status banner, then the last week and next week split, then a decisions and help needed strip |
| 3 | Risks, issues, and challenges | What is in the way? | RAID table, top 6, with age and owners |
| 4 | Timeline | Are we on time? | Gantt with today line, milestones, client dependency stars, and a one-line timeline verdict |

### Slide notes

- **Status on a page**: the banner states the status and the reason in one line ("Amber: API links from the client team are 7 days late; UI work continues on a stub"). Items are outcomes ("Halo and cannibalization views ready for review"), grouped by workstream.
- **Risks, issues, and challenges**: scope requests outside the agreed scope are logged as issues with their timeline impact and the decision owner. Closed items show once as closed, then drop off.
- **Timeline**: the verdict line says whether the next milestone holds. If it moves, state the new date and the reason. Keep the plan identical to the baseline except for progress and marked changes.

## Flex rules

- One-slide format (when the client asks for it, or the week is quiet): banner on top, done and next in two columns, top 3 risks and the next milestone in a strip at the base.
- Status Red: add a recovery slide after slide 2 with actions, owners, dates, and the decision needed from the client.
- Several parallel workstreams: slide 2 groups by workstream with a small RAG dot per workstream next to its name.
- UAT or go-live week: add a checklist strip to slide 4 (UAT sign-off, data validation, access, training, hypercare).

## Validation checklist

- [ ] Overall status follows the RAG definitions and states the reason in one line.
- [ ] Last week's planned items are either in this week's done list or carried forward with a reason.
- [ ] Every risk and issue has an owner, a due date, and an age. Scope changes show timeline impact.
- [ ] The timeline shows today, milestones, and client dependencies, with a clear verdict line.
- [ ] Decisions needed from the client appear on slide 2 with owners and dates.
- [ ] Four slides unless a recovery or UAT slide is justified.

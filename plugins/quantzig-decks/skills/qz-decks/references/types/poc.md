# PoC

A PoC deck answers three questions: did it work, can we trust it, and what should we do next. The proof comes from something Quantzig already executed on a limited scope. The pitch is a pilot that scales the proof with clear success criteria. The deck earns the pilot by being honest about what was tested, what was not, and what must be true at scale.

## Two modes

| Mode | When | Difference |
| --- | --- | --- |
| Results | The PoC has been executed, results exist | Slides 7 and 8 show measured results and the real prototype |
| Pre-results | We are pitching the PoC itself, with an illustrative prototype | Slide 7 becomes "What you will see by week X", slide 8 shows illustrative screens marked "Illustrative", and success criteria become the promise |

Ask which mode applies if it is not clear.

## Workflow

1. Collect inputs, then research the gaps (SKILL.md, step 3). Pull from attachments: prototype screenshots, results, data landscape notes, scope documents.
2. Fix the success criteria first. Every result on slide 7 answers one criterion from slide 3. Tag them S1, S2, S3.
3. Draft the storyline with conclusion titles and confirm.
4. Build, then validate.

## Inputs

| Input | Options | What it changes |
| --- | --- | --- |
| Business objective | Free text | Slides 2 and 3 |
| Success criteria agreed | 2 to 4 measurable criteria | Slides 3 and 7 |
| Scope tested | Geography, brands, sites, data sources, users, duration | Slide 4 |
| Data used and gaps | Internal, external, proxies | Slide 4 |
| Approach and method | Free text or attachments | Slides 5 and 6 |
| Results | Per criterion: met, partly met, not met, with numbers | Slide 7 |
| Prototype | Live screenshots / Illustrative / Demo link | Slide 8 |
| Learnings and limits | Free text | Slide 9 |
| Pilot shape | Scope expansion, duration, team roles | Slides 10 and 11 |
| Commercials | Include range / Exclude, discuss later | Slide 10 |

## Storyline (cap 12, tolerance 2)

| # | Slide | Audience question | Hero visual |
| --- | --- | --- | --- |
| 1 | Cover | What is this about? | Cover with outcome title |
| 2 | Executive summary | Did it work, and what do you want? | Result strip: What we tested, What we found, What it means, What we propose |
| 3 | Objective and success criteria | What were we trying to prove? | Objective banner plus 2 to 4 criteria cards tagged S1 to S4 |
| 4 | Scope and data | What exactly was tested? | Split in scope versus out of scope, plus a data landscape strip (sources, coverage, proxies) |
| 5 | Our approach | How did you do it? | Chevron journey of 3 to 5 steps |
| 6 | How it works | Is it sound? | Layered architecture or a step-by-step worked example from raw data to insight |
| 7 | Results against success criteria | Did it meet the bar? | Scorecard: criterion, target, result, met or not, with big numbers |
| 8 | What it looks like | What will my team use? | Framed screenshots with callout pins naming the decision each supports |
| 9 | What we learned | What should we worry about? | Three columns: what worked, what we would change, what must be true at scale |
| 10 | Pilot proposal | What is next and how big? | Swimlane roadmap: pilot, scale-up, full scale, with the pilot's own success criteria at the gate |
| 11 | Team, governance, and what we need from you | Who and what does it take? | Team cards plus the What we need from you block |
| 12 | Next steps and decision | What happens Monday? | Next-steps timeline ending in a pilot go or no-go |
| A | Appendix | Show me the detail | Method, features, data dictionary, detailed results, dashboard pages, sample templates |

### Slide notes

- **Executive summary**: the "What we found" tile carries 2 or 3 big numbers. The last tile states pilot scope, duration, and the decision needed.
- **Objective and success criteria**: criteria are measurable and were ideally agreed with the client before the PoC ("capture 90% of valid reviews across UK locations"). If they were not agreed, say "proposed criteria".
- **Scope and data**: be explicit about proxies and limits. This slide protects credibility later.
- **Results**: every criterion from slide 3 appears once. Partly met results say why and what closes the gap. Never hide a missed criterion.
- **What we learned**: this is the slide that earns trust. Include data quality issues, model limits, and client dependencies found.
- **Pilot proposal**: the pilot scales one dimension at a time (more sources, more geographies, more users). State pilot success criteria and duration. Pricing only if the user chose to include it; otherwise "investment to be discussed".

## Flex rules

- Short PoC (under 4 weeks) or a single model: merge slides 5 and 6.
- No prototype UI (pure model or analysis): slide 8 shows sample outputs (ranked lists, segment profiles, charts) instead of screens.
- Multiple analytical options were tested: add one appendix slide comparing options, and state the chosen one on slide 6.
- Strong comparable past work: add a Proof card from `references/blocks.md` after slide 9, within the tolerance.
- Keep one version of each slide. Draft variants (different week counts, repeated architecture slides) are deleted, not moved to the appendix.

## Validation checklist

- [ ] Every success criterion on slide 3 has a result on slide 7, and every result on slide 7 traces to a criterion.
- [ ] Scope and data limits are stated before results are shown.
- [ ] Missed or partly met criteria are shown with a reason and a fix.
- [ ] Illustrative screens and pre-results content are tagged "Illustrative".
- [ ] The pilot has its own success criteria, duration, and a gate decision.
- [ ] No duplicate or draft variant slides anywhere in the deck.

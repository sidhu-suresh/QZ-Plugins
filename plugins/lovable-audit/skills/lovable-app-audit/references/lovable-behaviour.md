# How the builder takes a prompt

This file records what a Lovable style single page app build actually does with an instruction, so the prompts are written against observed behaviour rather than hope. It is deliberately generic: no app, no client, no project is named, and every line is either observed on a real round or marked as an inference.

Sources are our own prompt rounds, the QA passes that followed them, and a live re-verification on 2026-10-17 that drove a deployed app through twelve routes at two widths and measured the result. That re-verification is the reason the last section exists.

Re-verify before you rely. Three classes of defect that this file once recorded as chronic had already been fixed on the app we retested. The list below ages.

## What it does with a prompt

**It lands a multi-part prompt in part, and reports success anyway.** A single pass that asked for a layout change and a type and pill retune landed the layout and dropped the retune, and nothing in the result said so. This is the single most expensive behaviour in the file, because it looks like a normal successful run.

Consequence: one issue per prompt, always. And the QA pass checks each item, never each prompt, because a prompt is not a unit that succeeds or fails. Where a fix genuinely has several parts, split them so a partial landing is visible.

**It builds the shell of a control before the behaviour.** A filter that stores a value nothing reads, and a pair of pickers fed from two different lists so they can never agree, both look finished on screen. Observed live: changing a Channel filter from one value to another changed only the filter's own label, and the panel's text did not move at all, with the active scope line not mentioning the value either.

Consequence: a prompt that touches a control must state the observable effect, not the existence of the control. What changes on screen when it is used, and what the reader should see happen. A prompt that says "add a filter" gets a filter that does not filter.

**It reuses one component across many call sites.** A single detail panel opened from four different tiles, with real per tile content inside a shared shell. Observed live, and the same shape had been reported in an earlier round behind different triggers. The content differs, the shell repeats.

Consequence: name the contexts a panel must bind to, and say what belongs in it, or every tile will open the same panel. A generic panel behind many triggers is a finding, not a design.

**It falls back silently on a value it does not recognise.** Observed live and worse than expected: an unknown tab value rendered the default and rewrote the URL to match, while a near miss that shared a prefix rendered a different tab and left the URL unchanged, so the address bar and the screen disagreed with each other. No error appeared in either case.

Consequence: name the exact parameter, list the valid values, and say what should happen on anything else. The QA check is the URL against the rendered view, which is a comparison, not a glance.

**It leaks boilerplate by copy and paste.** Observed live: every dialog in one build rendered the label Close twice. Duplicate labels, duplicate controls and leftover strings are a reliable signature.

Consequence: the visual lens counts duplicates in a container rather than trusting that one thing looks right.

**It does land single concern asks, and it does make structural layout changes.** Facet cascading landed, stacking and page scroll landed, a shell rebuilt around a scrolling content column landed. So a narrow, specific prompt is not a weak prompt, and there is no reason to bundle for strength.

**It can drift from its own export.** A code export does not always match what is deployed. Point prompts at the deployed app, and treat an export that disagrees as a finding in itself.

## What it tends to leave behind

These are the habits worth checking on any build, rather than assumed defects on a particular one.

**Type and pill drift, independent of width.** Measured live: fourteen to eighteen distinct font size and weight combinations on a single route, and seven to eleven distinct pill heights. Identical counts at 1280 and at 1440, which means it is drift, not responsiveness. A scale retune asked for inside a larger prompt did not land. So run a retune as its own prompt, and verify it by counting the distinct values from the geometry file rather than looking at the page.

**Assets at natural size inside a small box.** Measured live: a logo at roughly seven and a half times its rendered width, and a mark rendered at zero by zero inside a live route. Cheap to check, easy to miss by eye.

**Truncation instead of reflow at mid widths.** Text clipped by line clamping showed up at 1280 more than at 1440. Check the mid widths, not only the narrow ones.

**Interpretation left unlabelled or over-labelled.** Italics used for interpretation lines alone is the good version of this. The bad version is a claim stated flatly that the data does not support.

**Collapsed sections against a stated default.** Observed live at two routes, collapsed to a fifty one pixel header.

**Route and navigation coverage is usually complete.** On the app we retested: every sidebar item resolved, unknown paths hit a real not found page, there were no console errors and no failed requests across the routes walked. So do not report a dead nav item or a missing route without checking, and do not read a clean console as a clean app.

## What we had wrong

This section matters as much as the ones above.

Three classes were recorded here from earlier rounds as chronic and did not reproduce on the live re-verification: a sticky bar sharing a z index with another and overlapping it while scrolling, panels stuck on a loading skeleton that never resolves, and charts cropped by a fixed height inside a flex fill container. The build we retested had a deliberately staggered sticky stack, no skeletons, and no clipped charts.

So the honest position is that the profile is a memory of a moment, not a description of the software. Every round re-captures and re-measures. A carried over issue gets re-checked before it is repeated.

The one thing to carry forward from that list is not the defect but the class of it: fixed heights inside flex fill containers, and two elements claiming the same layer at the same offset, are the shapes that produce those defects. Check the shape.

## Prompt shapes that land

From the rounds that worked, and the ones that did not:

- One issue, one prompt, one paste.
- Name the file and, where it matters, the component. An unambiguous target.
- Say what is wrong now in one line, then what it should be, then what must not change.
- State the observable effect for anything a reader can operate.
- Name parameters and their valid values.
- Keep a retune of a scale or a set of pills out of any prompt that also moves layout. Give it its own.
- Keep the acceptance check to one line and make it comparable, so the QA pass is a comparison rather than an impression.
- Order prompts by prerequisite and say which must run before which.
- Expect to check every part, because partial landing is normal.

## Budget and spill

Oversized prompts spill: the builder comes back with work outside what was asked. So 250 to 350 words typical, 450 as a hard ceiling, and an over budget prompt gets its scope cut rather than its wording compressed. Cut the reasons, the restatement, the examples and the hedging before cutting the target.

Latency, for planning a round rather than for the report: a twelve route, two width capture with about fifty tool calls took roughly eleven minutes of wall clock. Budget the round around the paste and the generation, and capture in parallel with the profile rather than after it.

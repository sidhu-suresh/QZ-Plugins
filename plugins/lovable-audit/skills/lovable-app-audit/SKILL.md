---
name: lovable-app-audit
description: Run a parallel team audit of a deployed Lovable app and return findings, single-issue paste-ready prompts and a QA pass. Use when the user shares screenshots, an export zip or a deployed URL for an app they are iterating on, or asks for an app to be reviewed, polished, fixed, reconciled against its brief or prepared for a client demo. The audit keeps a requirements profile per app, captures its own evidence from a browser, runs five lens specialists at once plus an optional security lens, and has sharded adversarial verifiers try to disprove every finding before the user sees it.
---

# Running an app audit team

This is the playbook. It exists so the team can be run two ways: by spawning `lovable-audit-lead`, or, if the lead cannot spawn its own specialists, by dispatching the team from the session you are already in. Use this file when you are the caller rather than the lead.

The audit carries no baked-in knowledge of any particular app. Everything app-specific comes from the app's profile file. Read `references/dashboard-quality.md` alongside `references/lovable-behaviour.md`. The dashboard reference separates configurable design choices from required quality checks. Judge options against the profile, never impose optional features by default.

## The team

| Agent | Lens | Reads |
| --- | --- | --- |
| `lovable-audit-capture` | Drives the browser: page text, accessibility tree, layout geometry, console and network failures, screenshots on main routes | The live app |
| `lovable-audit-visual` | Layout, scroll, layering, states, type, responsive, themes, keyboard, roles, performance smells | Capture, export |
| `lovable-audit-consistency` | Figures that disagree, records that contradict themselves, labels, units, export versus deployed | Capture, export |
| `lovable-audit-story` | The narrative arc, whether each screen leads with its answer, next steps, whether the journey completes | Capture, profile |
| `lovable-audit-scope` | The must have register, additions, silent removals, drift | Capture, profile, requirement sources |
| `lovable-audit-hygiene` | Credentials, real data in seed data, auth gates in the source, broken assets and links | Export only |
| `lovable-audit-security` | Optional. Gates that are only cosmetic, records reachable as the wrong role, trust in a value the visitor can edit, verbose failure | Live app, export |
| `lovable-audit-verifier` | Tries to disprove each finding, then re tests the fixes | Everything |

Only the lead, or you, writes to the user. The specialists return findings and nothing else, which keeps one voice on the prompts and stops several agents inventing incompatible fixes for the same screen.

## What runs at the same time

The lenses were never the slow part, because they already go together. Two things actually set the wall clock:

Start capture before you read the profile in any depth. Capture is mechanical and needs the route list, not the brief, so it can run while the profile is still being confirmed. Shard it across two or three instances by route group, each in its own browser tab, dispatched in one message.

Shard the verifier. One instance reading everything twice is the longest single step in a round. Split the merged findings across two or three instances, and split the fixes across one instance each in the QA pass.

Three things cannot be compressed: the human paste loop into Lovable, Lovable's own generation time, and the fact that two reviewers editing one file cannot safely run together. Say so rather than implying the round is instant.

Fan out on tokens, not on wishes. Each instance re reads its slice, and images are the expensive part, so capture text and geometry everywhere and images only where it counts.

## How to dispatch

Step 0 is the profile and Step 1 is capture, and they run together.

**Profile.** Find it in this order: the app repository at `audit/app-profile.md`, a connected working folder at `lovable-audit/<app-slug>/profile.md`, then the session outputs folder at the same relative path. If one exists, read it and treat it as the working memory for that app. If none exists, check with the user before creating one, because a profile in a folder you cannot see holds the must have register and the old versus new flags. Build a fresh one only once you are sure none exists. If only a URL was given and no brief, ask for the scope in one short block: what the app is for, who reads it, which pages must exist, what is deliberately out, what must not change, and where the requirement source lives. Mark the register pending until confirmed.

**Capture.** Send `lovable-audit-capture` out straight away with the live URL, the routes, the widths, a run id and an evidence folder, sharded by route group and dispatched in one message. Give it credentials only when the app has a login and the profile already holds them. Test persona or audience modes even without authentication. Never put a credential in a brief that leaves the machine or in a prompt.

Widths are 1440, 1280, 1024, 768 and 375. Capture writes its output under `audit/evidence/<run-id>/` as text, geometry, console and network files that survive the session, plus screenshots that land as session bound paths recorded in the manifest.

**Evidence pack.** Assemble what the team gets: the profile path plus the verbatim Dashboard configuration, Constraints, Scope and Known issues sections, since the specialists judge against those and cannot open a file you merely described. The app slug, the live URL, the route list, the requirement source paths, the export path if there is one, the capture folder and manifest with its stable labels, the widths and roles captured and those missed, which artifact is newest and when, and the list of things nobody could reach.

Two rules go in every brief. A fetched page shell is not evidence of what a screen shows, and never evidence that a screen is missing. And nobody asserts on a screen they did not reach, which includes a route the capture failed on.

**Dispatch the lenses at once.** Spawn them all in a single message, each with the evidence pack and its own lens. Do not dispatch a lens whose whole input is missing. With no export, hygiene has nothing to read. With no capture, hold the visual, story and consistency lenses rather than letting them guess. Dispatch `lovable-audit-security` only when the user opted in, or when the profile records that they want it for this app, and ask once in one line rather than assuming.

A specialist returns findings, or one line saying its lens is clean. Those differ. An empty return is a failure, so retry that one once and then record the lens as did not report, rather than letting silence read as a clean pass.

**Dedupe.** Give each surviving finding an identifier, because the verifier works by identifier and nobody else creates them. Merge on two keys: route plus element plus symptom, and separately the component or root cause, which collapses one cause showing up as six findings on six routes into one finding with six locations and one prompt. Take the lowest defensible severity, not the highest. Union the evidence rather than picking the sharpest line. Where two lenses disagree, and one calls a defect what the other says is recorded in the profile as deliberate, send it to the verifier unresolved rather than settling it by severity. Note where two lenses independently found the same thing, and keep one finding where hygiene and security both report one key.

**Verify, in shards.** Split the merged list across two or three verifier instances in a single message, each with the same pack, the identifiers it owns, and each finding's falsifier line. Sharding is safe here because the merge already collapsed the duplicates. Keep every blocker in every shard. A finding that cannot be reproduced from the evidence does not go in front of the user. Where the verifier asks for one more thing, note that you have no browser pass left now that capture has finished, so anything needing a live observation has to be asked for and may not arrive; if it does not, the finding goes to unverified rather than staying in the main list. Prompts may cite verified findings only.

**Then write the prompts.** The prompts come after the findings, never before.

**QA pass, fanned out.** Send the fix list and the new evidence back to the verifier, stamped with the run it belongs to, split so one instance owns one fix. Each re tests its own fix on the same screen as before, then hunts for what it broke on other routes, other widths, the other theme and the components that share the code that changed. Run a separate sweep instance over the shared components and the widths whose only job is regressions. Regressions go at the top of the report.

**Update the profile.** Iteration log entry, corrected lines, updated issue statuses.

## Dashboard quality coverage

For dashboard/analytics apps, check the applicable items in `references/dashboard-quality.md`. Capture and report the configured choices separately from defects. Required checks include user-facing punctuation and copy cleanup, untrimmed text, card density/clipping, functional sorting on every table, working/cascading filters, data reconciliation, chart behavior, state/error handling, responsive behavior and accessibility. Track each item as pass, fix required, not applicable or not verified. Do not call missing evidence a pass. Include only relevant checks in each prompt's QA checklist; retain full coverage in the round checklist.

## Severity

- **Blocker.** The journey cannot complete, or a client visible figure contradicts itself, or a credential or real data is exposed, or a record or route is reachable as the wrong role.
- **High.** A visible defect on a main route, a scope must have missing, or a broken primary interaction.
- **Medium.** Polish, consistency, crowding, a secondary route misbehaving.
- **Low.** Nits, and copy.

## Prompt discipline

Read `references/lovable-behaviour.md` first. It records what the builder does with a prompt, observed rather than assumed, and the rules below follow from it. The short version: a multi-part prompt lands in part and reports success anyway, so one issue per prompt and QA per item; a control is built as a shell before its behaviour, so name the observable effect; one component gets reused across call sites, so name the contexts a panel binds to; an unrecognised value falls back silently and can leave the address bar disagreeing with the screen, so name the parameter and the valid values; and a type or pill retune needs its own prompt and is verified by counting. Carried over issues decay, so re-verify before repeating one.

**A run is one paste.** A round normally produces several prompts and the user pastes them one at a time, in your order. At most five prompts in a round, with the rest queued and the reason stated.

**One issue per prompt.** Never combine two issues to save a round. A single fix with several parts Lovable would take in one go is one prompt. A fix that would not fit is split into sequential prompts.

**Budget the tokens.** 250 to 350 words typical, 450 hard ceiling. Over budget means cutting scope, not compressing the wording.

**Shape.** Name the file and, where it matters, the component. What is wrong now, in one line. What it should be, one to three lines. What must not change. A one line acceptance check. Stop.

**Cut.** Restating the app or the route. Why the change is wanted. Examples unless the behaviour is ambiguous without one. Politeness and hedging. Words like comprehensive and seamless. Any instruction starting with making sure, which invites Lovable to invent extra work.

**Preamble.** Short: the file, the routes touched, and the constraint that nothing outside the described change moves. From the app's own constraints, never from another project.

**Never bundle a redesign into a fix.** Name the files and routes the prompt touches and say the rest stays as it is.

**Respect the app's own architecture**, whatever the profile records about the data layer, the approval flow and the conventions, unless the user changes it.

**The QA checklist sits outside the fence.** It follows the prompt in your reply as a short tick list, it is not pasted into Lovable, and it does not count against the budget. One per prompt, and only the items that could actually fail.

Deliver each prompt in a fenced code block so it gets a copy button.

## House rules

No AI markers. No em dashes, no em dots, no arrows as punctuation. No "let us dive in", no "certainly", no "great question". Plain human prose.

Do not move a figure or a piece of demo data the profile lists as load bearing. If one has to move, flag it rather than changing it quietly.

Label an interpretation as an interpretation wherever the app does not already.

Report what nobody could verify in one line, rather than leaving it implied.

Never name another client's work in anything that leaves the firm, including a prompt, a findings file, a demo's sample data and an app's on screen copy.

Never let a credential into a brief, a prompt or a findings file. Record the role and where the credential lives, nothing else.

## Output format

One line verdict. Findings grouped by severity, each with route, element, symptom, evidence, its capture label, severity, and old or new against the profile. One short line per lens that came back clean. Then the disputed and unverified buckets, kept separate. Then the prompts in order in code blocks, with the prerequisite order and anything queued. Then the QA checklists. Then what could not be verified.

Do not pad, and do not summarise what you just wrote.

## When a round is finished

Four conditions, named at the end with the outstanding ones called out: every prompt in the round pasted; the QA pass showing each item landed or consciously deferred; the profile's known issues updated; and an iteration log entry for the round. Allow at most two QA cycles on a round. If items are still not landed after two, stop and ask the user whether to keep going rather than spending a third pass on the same fix.

## What the team cannot reach

Capture closes most of the gap, but not all of it. A live single page app can be walked, resized and screenshotted, so layout, text, order, geometry and reachability are all fair game. A physical keyboard and full screen-reader assessment are outside this capture. Where browser key events are available, capture keyboard navigation, focus visibility, dialog focus behavior and accessible names on main routes. A login screen or route behind credentials nobody supplied remains inaccessible. Ask for the credentials or a pass for those, and name what stayed out of reach rather than implying it was fine. Where the capture failed on a route, that route is unverified, not clean.

## The profile

One markdown file per app, written by the team and owned by the user. A skeleton ships at `templates/app-profile.md`.

**Identity.** App name, live URL, Lovable project id, audience, first seen, last audited.

**Requirement sources.** Each one, where it lives, which wins on conflict.

**The story.** The decision the app supports, the persona, the intended reading order, the one screen that has to land.

**Scope.** Must haves with status and what proves each. Good to haves. Explicitly out of scope and who ruled it out. A standing no-go list for this app.

**Design system.** Palette with hex values, accent and derived stops, fonts, radii and shadows, the token file, and whether the palette is locked to a client brand.

**Architecture.** Routes and purpose, the shared components that matter, where data comes from, the role and permission model, whether state persists.

**Access and roles.** Whether there is a login, the roles, where test credentials are kept, and what each role may do. The role and the location, never the value. Without login, skip credentialed sign-in only. Test persona-specific views and actions when personas or audience modes exist.

**Capture.** The routes captured, the widths, the evidence folder, and which artifact is newest.

**Constraints that must survive every change.** Per app, never assumed from another project: demo data that must not move, any approval or governance flow, load bearing figures, the rule on what opens by default, the rule on what belongs in a shared modal, the convention for labelling an interpretation, and any naming rule.

**Known issues carried over.** With status and the date last checked.

**Iteration log.** Dated, newest first.

**Open questions.** Including whether the security lens is wanted on this app, until that is answered.

## Boundaries

No redesign, no re theming, no re platforming. No invented data, metrics or figures. No guessing at a screen nobody reached. No exploitation, no mutation and no exfiltration in the security lens, whatever the finding. If the user asks for something that conflicts with the profile, say so in a line and follow the profile unless they overrule it, and if they overrule it, update the profile so the decision survives.

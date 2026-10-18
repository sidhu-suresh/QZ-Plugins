# lovable-audit

A team of nine agents that audits a deployed Lovable app and hands back one paste-ready prompt per issue.

Point the lead at an app URL and it runs everything else: it reads the app's requirements profile while browser capture is already running, splits the work across parallel lens specialists, adversarially verifies what they claim, and writes the fixes as prompts sized for Lovable.

## The team

| Agent | Job |
| --- | --- |
| `lovable-audit-lead` | Orchestrates the round and is the only writer. Holds the profile and the prompt budget. |
| `lovable-audit-capture` | Drives the browser: page text, layout geometry, console and network, screenshots on the main routes. Sharded by route group, one tab each. |
| `lovable-audit-visual` | Layout, spacing, hierarchy, assets, truncation, responsive behaviour. |
| `lovable-audit-consistency` | One term, one meaning. Numbers that agree, controls that do what they say, parameters that mean what they claim. |
| `lovable-audit-story` | Does each route tell the story it is meant to tell, in the right order. |
| `lovable-audit-scope` | What was promised against what is actually there. |
| `lovable-audit-hygiene` | Source-level craft: dead code, naming, duplicated markup, leaked boilerplate. |
| `lovable-audit-security` | Optional, opt in per round, read only. Gates, roles, trust in visitor-controlled values, verbose failure. |
| `lovable-audit-verifier` | Adversarial. Tries to kill each finding. Runs in shards after the merge, and fanned out one per fix during QA. |

Specialists have no write access and no ability to spawn agents, so nothing can be edited mid round. Only the lead writes.

## Where the time goes

Capture runs at the same time as the profile read instead of after it, and the merged findings split across two or three verifiers, which is safe because the merge has already collapsed duplicates. The QA pass runs one verifier per fix plus a sweep instance over shared components and widths. Three things cannot be compressed: the paste loop into Lovable, Lovable's own generation time, and two reviewers editing one file at once.

## Written against the builder's real behaviour

`skills/lovable-app-audit/references/lovable-behaviour.md` records what this kind of build actually does with a prompt, observed and measured rather than assumed: multi-part prompts land in part and report success anyway, controls arrive as shells before their behaviour, one component gets reused across many call sites, unrecognised parameter values fall back silently, and type and pill drift is chronic and width independent. The lenses and the verifier judge against it, and prompt discipline follows from it.

## What it cannot reach

A motion captured midway, a real keyboard, a screen reader, and anything behind a login nobody supplied credentials for. A route the capture failed on is unverified, not clean.

## Install

Build `lovable-audit.plugin` from this folder and upload it in Cowork. Start a new session afterwards before expecting the agents to be callable.

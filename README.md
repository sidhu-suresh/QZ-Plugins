# Quantzig plugins

Private repository for Quantzig's Claude plugins. Contains client-derived material: keep this repository private.

## quantzig-decks (v0.4.0)

One skill, `qz-decks`, for every Quantzig deck: storyline by deck type, clarifying questions, research for thin slides, the real Quantzig master in Grandview and brand colours, a 330-slide visual library placed as native shapes, and automated checks (`formatting/scripts/deck_check.py`).

Source: `plugins/quantzig-decks/`

## lovable-audit (v0.2.0)

Nine agents that audit a deployed Lovable app. A capture agent drives the browser for page text, layout geometry and screenshots while the app's requirements profile is still being read, five lens specialists then run at once (visual, consistency, story, scope, source hygiene) with an optional read-only security lens, findings are merged and identified, and verification is split across shards. The round ends as one paste-ready prompt per issue, with the QA pass fanned out one verifier per fix. It also carries what this kind of build actually does with a prompt, observed and measured, in `skills/lovable-app-audit/references/lovable-behaviour.md`.

Source: `plugins/lovable-audit/`

## Building the upload files

From the repository root:

    cd plugins/quantzig-decks && zip -r ../../quantzig-decks.plugin . -x "*.DS_Store" && cd ../..
    cd plugins/quantzig-decks/skills && zip -r ../../../qz-decks.skill qz-decks -x "*.DS_Store" && cd ../..
    cd plugins/lovable-audit && zip -r ../../lovable-audit.plugin . -x "*.DS_Store" && cd ../..
    cd plugins/lovable-audit/skills && zip -r ../../../lovable-app-audit.skill lovable-app-audit -x "*.DS_Store" && cd ../../..

Upload `quantzig-decks.plugin` and `lovable-audit.plugin` in Cowork, and `qz-decks.skill` and `lovable-app-audit.skill` in the Chat tab. Start a new session after installing before expecting the agents to be callable.

## Changing a plugin

Edit files under `plugins/<plugin>/skills/<skill>/`, bump `version` in `plugins/<plugin>/.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`, commit with a message that says what changed, then rebuild and re-upload.

For `lovable-audit`, the agents live under `plugins/lovable-audit/agents/` and the behaviour notes under `plugins/lovable-audit/skills/lovable-app-audit/references/`. Bump both version files for either one.

## Version history

### quantzig-decks

- 0.4.0: mandatory clarifying questions with options; mandatory research for thin slides.
- 0.3.0: storyboard first, unique layout per slide, self-explanatory density, Grandview only, whole-point sizes from 10pt (10.5 allowed), status colours only on metrics, deck_check.py, final slide-by-slide review.
- 0.2.0: Grandview only, brand palette, template clean-up.
- 0.1.0: first plugin bundle.

### lovable-audit

- 0.2.0: Adds per-app dashboard configuration, a required post-build quality checklist and Knowledge template; expands table/filter/copy/data/responsive/accessibility checks; improves keyboard evidence and persona checks without login.
- 0.1.0: first release. Nine agents, browser capture sharded and running concurrently with the profile read, five lenses plus an optional read-only security lens, merged and identified findings, sharded adversarial verification, one paste-ready prompt per issue, and a fanned-out QA pass. Includes the observed builder behaviour reference.

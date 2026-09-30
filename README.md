# Quantzig plugins

Private repository for Quantzig's Claude plugins. Contains client-derived material: keep this repository private.

## quantzig-decks (v0.4.0)

One skill, `qz-decks`, for every Quantzig deck: storyline by deck type, clarifying questions, research for thin slides, the real Quantzig master in Grandview and brand colours, a 330-slide visual library placed as native shapes, and automated checks (`formatting/scripts/deck_check.py`).

Source: `plugins/quantzig-decks/`

## Building the upload files

From the repository root:

    cd plugins/quantzig-decks && zip -r ../../quantzig-decks.plugin . -x "*.DS_Store" && cd ../..
    cd plugins/quantzig-decks/skills && zip -r ../../../qz-decks.skill qz-decks -x "*.DS_Store" && cd ../../..

Upload `quantzig-decks.plugin` in Cowork and `qz-decks.skill` in the Chat tab.

## Changing the skill

Edit files under `plugins/quantzig-decks/skills/qz-decks/`, bump `version` in `plugins/quantzig-decks/.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`, commit with a message that says what changed, then rebuild and re-upload.

## Version history

- 0.4.0: mandatory clarifying questions with options; mandatory research for thin slides.
- 0.3.0: storyboard first, unique layout per slide, self-explanatory density, Grandview only, whole-point sizes from 10pt (10.5 allowed), status colours only on metrics, deck_check.py, final slide-by-slide review.
- 0.2.0: Grandview only, brand palette, template clean-up.
- 0.1.0: first plugin bundle.

# Project: One-File Web Games

A collection of mini games in the style of mobile playable ads. Every game follows
`docs/regulation.md`: its MUST rules are mandatory, and its SHOULD principles may be
deviated from intentionally (noted in a top-of-file comment). Each game's help panel
follows `docs/help.md`. The catalog page `src/index.html` lists every game and follows
`docs/catalog.md`.

## Development Flow (implementation-first)

1. **Implement**: Build `src/<name>/index.html` directly from the user's idea,
   following `docs/regulation.md`. Iterate on feel and balance with the user. Add or
   update the game's card in `src/index.html` per `docs/catalog.md` in the same change.
2. **Verify**: Walk through the MUST Compliance Checklist in `docs/regulation.md` and
   actually play the game in a browser with a mobile viewport, judging it against the
   SHOULD principles. Also view the catalog page in the same viewport to check the card.

The implementation is the only source of truth; do not write per-game spec documents.

## Project-Specific Rules

- **Testing policy**: No test framework for the single-file games. Verification is the
  Compliance Checklist plus real play in a browser — do not ask about introducing a
  test setup for game implementations. The scriptable MUST checks run through the
  `tester` agent as shell commands; feel, balance, and layout are judged by playing the
  game with the user, and no script replaces that.

## Subagents

The main conversation writes all code at every tier; there is no implementer agent.
`reviewer` and `tester` (in `.claude/agents/`) are read-only or check-only, so they run
without asking. Use the built-in `Explore` for codebase lookups.

- **Trivial** (typo, one-line fix, config tweak): implement directly, no agents.
- **Non-trivial** (a new game, a gameplay change, a doc change): implement directly,
  then run `reviewer` and `tester` in parallel.
- **Large** (changes across several games or to `docs/regulation.md` as a whole):
  propose that the user drive it with `/goal`, with a completion condition that requires
  `reviewer` to report no findings and `tester`'s checks to pass. That covers only the
  objective part; feel and balance are still tuned by playing with the user.

Visual checks have no agent: the main conversation plays the game in a browser with a
mobile viewport, as in the Verify step.

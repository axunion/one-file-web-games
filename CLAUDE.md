# Project: One-File Web Games

A collection of mini games in the style of mobile playable ads. Every game follows
`docs/regulation.md`: its MUST rules are mandatory, and its SHOULD principles may be
deviated from intentionally (noted in a top-of-file comment).

## Development Flow (implementation-first)

1. **Implement**: Build `games/<name>.html` directly from the user's idea,
   following `docs/regulation.md`. Iterate on feel and balance with the user.
2. **Verify**: Walk through the MUST Compliance Checklist in `docs/regulation.md` and
   actually play the game in a browser with a mobile viewport, judging it against the
   SHOULD principles.

The implementation is the only source of truth; do not write per-game spec documents.

## Project-Specific Rules

- **Testing policy**: No test framework for the single-file games. Verification is the
  Compliance Checklist plus real play in a browser — do not ask about introducing a
  test setup for game implementations.

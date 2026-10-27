# Project: One-File Web Games

A collection of mini games in the style of mobile playable ads. Every game MUST comply
with `docs/regulation.md` — it is the absolute requirement for all games.

## Development Flow (implementation-first)

1. **Implement**: Build `games/<name>.html` directly from the user's idea,
   following `docs/regulation.md`. Iterate on feel and balance with the user.
2. **Verify**: Walk through the Compliance Checklist in `docs/regulation.md` and
   actually play the game in a browser with a mobile viewport.

The implementation is the only source of truth; do not write per-game spec documents.

## Project-Specific Rules

- **Testing policy**: No test framework for the single-file games. Verification is the
  Compliance Checklist plus real play in a browser — do not ask about introducing a
  test setup for game implementations.

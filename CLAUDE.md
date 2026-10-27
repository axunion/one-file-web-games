# Project: One-File Web Games

A collection of mini games in the style of mobile playable ads. Every game MUST comply
with `docs/regulation.md` — it is the absolute requirement for all games.

## Development Flow (spec-first)

1. **Idea → Spec**: Copy `docs/spec-template.md` to `games/<name>/spec.md` and fill it
   in (Japanese). Confirm at this stage that nothing conflicts with the regulation.
2. **Spec Review**: Get the user's approval of `spec.md` before writing any
   implementation code.
3. **Implement**: Build `games/<name>/index.html` following `spec.md` and
   `docs/regulation.md`.
4. **Verify**: Walk through the Compliance Checklist in `docs/regulation.md` and the
   acceptance checklist in `spec.md`, and actually play the game in a browser with a
   mobile viewport.
5. **Sync**: If the design changed during implementation, update `spec.md` — the spec
   is always the source of truth.

## Project-Specific Rules

- **Language exception**: Each game's `spec.md` is written in Japanese. Everything else
  (regulation, code comments, commit messages, etc.) follows the global English rule.
- **Testing policy**: No test framework for the single-file games. Verification is the
  two checklists plus real play in a browser — do not ask about introducing a test
  setup for game implementations.

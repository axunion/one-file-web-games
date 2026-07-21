# Global Claude Rules

> `CLAUDE.md` and `AGENTS.md` are identical mirrors. Whenever either file is changed,
> apply the exact same change to the other.

Behavioral defaults plus house conventions. Bias toward caution over speed; on trivial
tasks, use judgment.

## Approach

- **Think before coding.** State assumptions; if uncertain, ask. When multiple
  interpretations exist, surface them rather than silently picking one. If a simpler path
  exists, say so and push back when warranted.
- **Simplest thing that works.** Write the minimum code that solves the stated problem —
  nothing speculative. No unasked-for abstractions, flexibility, or error handling for
  impossible cases. If 200 lines could be 50, rewrite it.
- **Surgical changes.** Every changed line should trace to the request. Don't refactor,
  reformat, or "improve" adjacent code that isn't broken; match the surrounding style.
  Remove only the imports and symbols your change orphaned; leave unrelated dead code alone
  and mention it.
- **Goal-driven.** Turn each task into a verifiable outcome ("fix the bug" → "write a
  failing test that reproduces it, then make it pass"). For multi-step work, state a brief
  plan with a verification check per step, then loop until each check passes.

## Language

Write everything in **English** — in-code comments, console output, error and log
messages, AI-readable instruction files, and docs meant for readers (README and the
like). Sole exception: development-time planning notes follow the language the user is
working in.

## Code Structure

- Name variables, functions, and files to communicate intent.
- One concern per file; split new code when a file exceeds ~300 lines. Don't split
  existing files unless asked.
- Extract a helper only when used in 3+ places; otherwise inline it.
- Delete dead code you create; never comment it out.

## Testing

- Write tests before or alongside implementation — they are your success criteria.
- If the project has no test setup, ask briefly: introduce one, or verify another way?
- Test observable outcomes and edge cases, not implementation details.
- Each test is fully self-contained; no shared mutable state between tests.

## Commits

Format:

```
<one-line summary>

<one sentence explaining the motivation>

- <change 1>
- <change 2>
```

The angle brackets are placeholders — replace them entirely with your own prose. No line
carries a prefix or label of any kind (`feat:`, `fix:`, and the like).

- Summary: imperative mood, ≤70 chars, no trailing period.
- Motivation sentence: include only when not evident from the diff alone.
- Bullets: include only for 2+ distinct changes.
- Never commit secrets (`*.key`, `*.pem`, `credentials*`).
- Never use `--no-verify`. Never use `--amend` unless explicitly asked; default to a new
  commit.

# Project: One-File Web Games

A collection of mini games in the style of mobile playable ads. Every game MUST comply
with `docs/regulation.md` — it is the absolute requirement for all games.

## Structure

```
docs/
  regulation.md      Cross-game regulation (English) — single source of truth
  spec-template.md   Spec template (Japanese) — copy to start a new game
games/
  <kebab-case-name>/
    spec.md          Game specification (Japanese)
    index.html       Complete game in a single self-contained file
```

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
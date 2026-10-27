# One-File Web Games

A collection of mini games in the style of mobile playable ads. Each game is a single
self-contained HTML file.

## Layout

```
docs/
  regulation.md      Cross-game regulation (English) — single source of truth
  spec-template.md   Spec template (Japanese) — copy to start a new game
games/
  <kebab-case-name>/
    spec.md          Game specification (Japanese)
    index.html       Complete game in a single self-contained file
```

## Playing

Open `games/<name>/index.html` in a browser. Games are designed for a mobile viewport.

## Adding a game

Every game must comply with [`docs/regulation.md`](docs/regulation.md). Development is
spec-first: copy `docs/spec-template.md` to `games/<name>/spec.md`, get the spec
approved, then implement `index.html`.

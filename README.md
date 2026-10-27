# One-File Web Games

A collection of mini games in the style of mobile playable ads. Each game is a single
self-contained HTML file.

## Layout

```
docs/
  regulation.md              Cross-game regulation — single source of truth
games/
  <kebab-case-name>.html     Complete game in a single self-contained file
```

## Playing

Open `games/<name>.html` in a browser. Games are designed for a mobile viewport.

## Adding a game

Every game must comply with [`docs/regulation.md`](docs/regulation.md). Development is
implementation-first: build `games/<name>.html` and verify it against the
Compliance Checklist.

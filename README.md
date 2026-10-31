# One-File Web Games

A collection of mini games in the style of mobile playable ads. Each game is a single
self-contained `index.html` in its own directory under `src/`. `src/` is the site root,
so a game is served at `/<name>/`.

## Layout

```
docs/
  regulation.md              Cross-game regulation — single source of truth
  catalog.md                 Rules for the catalog page `src/index.html`
  help.md                    Rules for each game's bilingual how-to-play panel
src/                         Site root
  index.html                 Table of contents linking to every game
  <kebab-case-name>/
    index.html               Complete game in a single self-contained file
```

## Playing

Serve `src/` with any static server and open `/<name>/`; the root `/` lists
all games. Games are designed for a mobile viewport.

## Adding a game

Every game follows [`docs/regulation.md`](docs/regulation.md) (MUST rules are mandatory,
SHOULD principles are guidelines). Development is implementation-first: build
`src/<name>/index.html` with a help panel following [`docs/help.md`](docs/help.md), add its
card to `src/index.html` following [`docs/catalog.md`](docs/catalog.md), and verify it
against the Compliance Checklist.

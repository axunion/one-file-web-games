# Catalog Page

Rules for `src/index.html`, the page that lists every game. Add or change a game's
card by copying an existing `<li>` and following these rules.

## Card

One `<li><a href="<game-name>/">` per game, appended at the end of the `<ul>`. A card
has three parts, in this order:

1. **Thumbnail**: an inline `<svg viewBox="0 0 120 90" aria-hidden="true">`.
2. **Title**: the game's title in a `<strong>`. It stays on one line; overflow is
   cut with an ellipsis, so keep titles short.
3. **Category**: one `<i class="tag <category>">`.

There is no description. The grid is `auto-fill` with a 160px minimum column, so adding
a card needs no CSS change.

## Thumbnail

- Draw it with SVG shapes only (no image files, no network) and keep it to the
  game's core object, e.g. the tiles, the skewer, the yarn.
- Use the game's own palette, starting with its background color as the full-bleed
  `<rect>`, so the card previews the game's world.
- Keep the subject centered with margin to the edges; the card clips with rounded
  corners.

## Category

- Exactly one per game, and abstract: a genre-level bucket, not a mechanic or
  feature (no "Snake", "Sound", "Match-3").
- Reuse an existing category when one fits. Current categories: Puzzle, Arcade.
- A new category needs one CSS line next to the others, `.tag.<name>`, with a
  tinted background and a darker text of the same hue. Pick a hue distinct from the
  existing ones.

## Page style

The soft gradient background and the serif heading are deliberate; the game pages
keep their own styles. Leave both alone when adding games.

## Keeping it in sync

When a game's title, palette, or core object changes, update its card in the same
change. Check the page in a mobile viewport afterwards.

# Help Panel

Rules for the how-to-play panel every game carries. The reference implementation is
`src/classic-2048/index.html`: copy its help parts into a new game, then restyle them to
the game's world. The code there is the source of truth; this page records what to keep
and what to adapt.

## What stays the same in every game

The structure and behavior are shared so that players learn it once.

- **Opening and closing**: a round `?` button sits at the top right. Opening the panel
  covers the whole screen, and a round `×` button takes the exact place of the `?`.
  `Esc` also closes it. Nothing opens automatically; the first interaction still teaches
  the game (see Self-explanatory in `docs/regulation.md`).
- **Both icons are inline SVG strokes**, never text glyphs. The ring is the button's own
  border; the SVG draws only the mark.
- **Input is blocked while open**: pointer and key handling for the game ignore events
  until the panel closes, and the controls behind it are `inert` so Tab and Enter cannot
  reach them. The `?` stays above the game-over screen, so help is reachable there.
- **Languages**: English and Japanese. The initial language comes from
  `navigator.language` (`ja` prefix gives Japanese, anything else English). It is not
  saved, because the Persistence MUST allows only the best record in `localStorage`.
- **Language switch**: two equal-width buttons at the top left, aligned with the `×`.
  The labels are written in the current language: `EN` / `JA` in English, `英語` /
  `日本語` in Japanese. The active one is filled.
- **`lang` attribute**: set on the panel and the `?` button, the elements that carry
  translated text. Setting it on `<html>` would change font fallback for the whole game.
- **Layout**: the switch and `×` are pinned to the top. The title and text sit in a
  fixed-height box that is centered vertically, with text starting at the top of the
  box, so the controls, the box, and where the text starts stay put when the language
  changes.
- **Accessibility**: the `?` and `×` buttons get `aria-label`s in the current language.

## Text

- A title (`How to play` / `遊び方`) and **four short items**, in this order: the goal,
  the controls, the core rule, the end condition. Drop an item the game does not need,
  and add one only when a rule cannot be learned by playing.
- Write explanations, not commands: "Swipe ... and every tile slides that way", not
  "Swipe to slide tiles". One short sentence per item, about two lines at the panel
  width. Japanese ends in です／ます and uses full-width punctuation.
- Write both languages from the same four points, not word for word, using the game's
  own terms for its objects.

## Adapting to the game

Colors, font family, sizes, spacing, button details, and the panel background are free
to change so the panel belongs to the game's world. Keep the `?`/`×` pair at the same
position and the language switch at the same height as the `×`. Derive the styling from
this game's palette; do not copy another game's.

The fixed-height, centered layout assumes about four short items. A game whose
explanation needs more, such as many rules, diagrams, or text that would scroll, picks
its own layout and keeps everything else above. No deviation comment is needed.

## Keeping it in sync

When the help text or panel changes in a way other games should share, update
`src/classic-2048/index.html` and this page together. Check the panel in a mobile
viewport in both languages, including that switching language moves nothing.

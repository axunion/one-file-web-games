# Game Regulation

Cross-game constraints for every game in this repository. Per-game behavior is defined
by the implementation itself.

## Purpose & Scope

This repository is a collection of mini games in the style of mobile playable ads:
instantly understandable, instantly playable, bite-sized. The rules are modeled on common
playable-ad constraints (self-contained single file, no network, instant play) but the
games are for browser play, not actual ad-network submission. Any genre fits, including
action and puzzle games, as long as it keeps that spirit.

Rules come in two strengths:

- **MUST**: technical and UX constraints that are objectively verifiable and independent
  of genre. Every game satisfies all of them.
- **SHOULD**: experience principles that keep the playable-ad feel. Numbers are
  guidelines, not limits. A game that deviates keeps working as long as the deviation
  is intentional: state it in one line in an HTML comment right after `<!DOCTYPE html>`,
  e.g. `<!-- SHOULD deviation: short rounds - a full puzzle takes about 5 minutes -->`.

## MUST

### File Constraints

- One game = one directory `src/<game-name>/` holding a single `index.html`, where
  `<game-name>` is kebab-case. With `src/` as the site root, the game is served at
  `/<game-name>/`.
- All HTML, CSS, and JavaScript live inline in that `index.html`. No separate
  `.css`/`.js` files, no build step. The file runs when opened directly in a browser
  (`file://` and any static server).
- Maximum file size: **512 KB**.
- Encoding is UTF-8 with `<meta charset="utf-8">`, and the file starts with
  `<!DOCTYPE html>`.

### No External Dependencies

- **Zero network requests.** No CDNs, web fonts, external images, analytics, `fetch`,
  `XMLHttpRequest`, or WebSockets.
- **No frameworks or libraries.** Vanilla JavaScript, CSS, and HTML only.
- All assets are generated in code: Canvas drawing, inline SVG, data URIs, CSS shapes,
  and Web Audio API synthesis. System fonts only.
- Every page declares the shared favicon below as an inline data URI right after
  `<title>`. Without a `<link rel="icon">`, browsers request `/favicon.ico`
  automatically, which is a network request; the data URI avoids it. Copy the tag
  verbatim so all games share one icon (the table-of-contents page `src/index.html`
  carries it too):

  ```html
  <link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Cpath d='M9 5H23C27.5 5 30 7.5 31 12L31.5 21C31.8 25 30 27.5 27 27.5C24.5 27.5 23.5 26 22.5 24L21.5 22H10.5L9.5 24C8.5 26 7.5 27.5 5 27.5C2 27.5 0.2 25 0.5 21L1 12C2 7.5 4.5 5 9 5Z' fill='%23ff6b4a'/%3E%3Cpath d='M9 10.5v7M5.5 14h7' stroke='%23fff' stroke-width='2.4' stroke-linecap='round'/%3E%3Ccircle cx='21.5' cy='15.5' r='2.2' fill='%23fff'/%3E%3Ccircle cx='26' cy='12' r='2.2' fill='%23fff'/%3E%3C/svg%3E">
  ```

### Mobile-First UX

- Designed for portrait orientation on a phone; fills the full viewport and scales
  responsively to any screen size, including desktop.
- Touch is the primary input. Every action also works with mouse click/drag.
- Page scrolling, pinch zoom, double-tap zoom, text selection, and touch callouts are
  suppressed during play. Safe-area insets are respected on notched devices.

### Performance

- Targets 60 fps on a mid-range phone, with animation driven by `requestAnimationFrame`.

### Audio

- Audio is optional. If present, it is synthesized with the Web Audio API, starts only
  after a user gesture (autoplay policy), and is mutable via an in-game toggle.

### Persistence

- `localStorage` may store only the best record (high score, or an equivalent such as
  fewest moves), under the key `ofwg:<game-name>` (e.g. `ofwg:neko-jump`). No other
  client-side storage and no mid-game save state.
- The game works normally when storage is unavailable.

## SHOULD

Each principle lists its intent, so a deviation can be judged against it.

- **Instant play**: playable within about 3 seconds of load, with no loading screens,
  menus, or settings first, and one tap to start. *Intent: zero friction before the
  first interaction.*
- **Self-explanatory**: instructions fit in one short line (e.g. "Tap to jump") or the
  first interaction teaches the game. *Intent: no tutorial to read.*
- **Short rounds**: a round lasts from tens of seconds to a few minutes. *Intent: easy to
  play in a spare moment and to replay.*
- **Simple input**: one or two verbs (tap, swipe, hold, drag). *Intent: the whole control
  scheme is understood at a glance.*
- **Clear end condition**: the game ends by an obvious fail or clear condition. *Intent:
  the player always knows what they are working toward.*
- **Visible progress**: a score or equally clear progress indicator is shown during
  play. *Intent: feedback on how the player is doing.*
- **Instant retry**: one tap restarts after the game ends. *Intent: "one more try"
  without friction.*
- **Lean frames**: minimal per-frame allocations and DOM/layout work; prefer Canvas for
  motion-heavy games. *Intent: keep the 60 fps MUST cheap to meet.*

## Compliance Checklist

Copy this checklist when verifying a finished game and confirm every item. SHOULD
principles have no checklist: judge them by playing the game, and note any intentional
deviation in a comment right after `<!DOCTYPE html>`.

- [ ] Single `src/<game-name>/index.html` with all CSS/JS inline; opens directly in a browser
- [ ] `index.html` is 512 KB or less
- [ ] `<!DOCTYPE html>` and UTF-8 charset declared
- [ ] Zero network requests (verified in DevTools Network tab)
- [ ] No frameworks or libraries; all assets generated in code
- [ ] Shared favicon tag present verbatim right after `<title>`
- [ ] Portrait mobile layout fills the viewport and scales to desktop
- [ ] Fully playable with both touch and mouse
- [ ] Scroll/zoom/text-selection suppressed during play
- [ ] Smooth (~60 fps) animation via `requestAnimationFrame`
- [ ] Audio (if any) starts only after a user gesture and can be muted
- [ ] `localStorage` limited to a best record under `ofwg:<game-name>`; game works
      without it

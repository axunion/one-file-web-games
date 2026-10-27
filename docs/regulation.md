# Game Regulation

Every game in this repository MUST comply with all rules below. This document is the
single source of truth for cross-game constraints; per-game behavior is defined by the
implementation itself.

## Purpose & Scope

This repository is a collection of mini games in the style of mobile playable ads:
instantly understandable, instantly playable, short-session games. The rules are modeled
on common playable-ad constraints (self-contained single file, no network, instant play)
but the games are for browser play, not actual ad-network submission.

## File Constraints

- One game = one file `games/<game-name>.html`, where `<game-name>` is kebab-case.
- All HTML, CSS, and JavaScript live inline in that file. No separate `.css`/`.js`
  files, no build step. The file must run when opened directly in a browser
  (`file://` and any static server).
- Maximum file size: **512 KB**.
- Encoding is UTF-8 with `<meta charset="utf-8">`, and the file starts with
  `<!DOCTYPE html>`.

## No External Dependencies

- **Zero network requests.** No CDNs, web fonts, external images, analytics, `fetch`,
  `XMLHttpRequest`, or WebSockets.
- **No frameworks or libraries.** Vanilla JavaScript, CSS, and HTML only.
- All assets are generated in code: Canvas drawing, inline SVG, data URIs, CSS shapes,
  and Web Audio API synthesis. System fonts only.

## Mobile-First UX

- Design for portrait orientation on a phone; fill the full viewport and scale
  responsively to any screen size, including desktop.
- Touch is the primary input. Every action must also work with mouse click/drag so the
  game is fully playable on desktop.
- Prevent page scrolling, pinch zoom, double-tap zoom, text selection, and touch
  callouts during play. Respect safe-area insets on notched devices.

## Instant Play

- Playable within 3 seconds of load. No loading screens, menus, or settings before play.
- Instructions fit in one short line (e.g. "Tap to jump") or are unnecessary because the
  first interaction teaches the game.
- One tap starts the game. After a game over, one tap restarts it immediately.

## Game Design

- Hyper-casual core loop: one simple verb (tap, swipe, hold, drag), an obvious goal, and
  a clear fail condition.
- A session lasts roughly 30 seconds to 2 minutes.
- Show a score or equally clear progress indicator at all times during play.

## Performance

- Target 60 fps on a mid-range phone. Drive animation with `requestAnimationFrame`.
- Keep per-frame allocations and DOM/layout work minimal; prefer Canvas for
  motion-heavy games.

## Audio

- Audio is optional. If present, it must be synthesized with the Web Audio API, start
  only after a user gesture (autoplay policy), and be mutable via an in-game toggle.

## Persistence

- `localStorage` may be used only to store the high score, under the key
  `ofwg:<game-name>` (e.g. `ofwg:neko-jump`). No other client-side storage.
- The game must work normally when storage is unavailable.

## Compliance Checklist

Copy this checklist when verifying a finished game and confirm every item:

- [ ] Single `games/<game-name>.html` with all CSS/JS inline; opens directly in a browser
- [ ] The file is 512 KB or less
- [ ] `<!DOCTYPE html>` and UTF-8 charset declared
- [ ] Zero network requests (verified in DevTools Network tab)
- [ ] No frameworks or libraries; all assets generated in code
- [ ] Portrait mobile layout fills the viewport and scales to desktop
- [ ] Fully playable with both touch and mouse
- [ ] Scroll/zoom/text-selection suppressed during play
- [ ] Playable within 3 seconds; instructions ≤ 1 line; tap to start
- [ ] One tap restarts after game over
- [ ] Score or clear progress visible during play
- [ ] Smooth (~60 fps) animation via `requestAnimationFrame`
- [ ] Audio (if any) starts only after a user gesture and can be muted
- [ ] `localStorage` limited to `ofwg:<game-name>` high score; game works without it

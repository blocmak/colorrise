# AGENTS.md

## Cursor Cloud specific instructions

This repo is **ColorRise**, a single static client-side PWA game (human vs. computer flood-capture). The entire app lives inline in `index.html` (UI + CSS + game logic), with `sw.js` (service worker for offline caching), `manifest.webmanifest`, and `icon.svg`.

### Services / how to run
- There is **one** thing to run: a static HTTP server at the repo root. The service worker (`sw.js`) and PWA features only work over `http(s)://`, not `file://`, so you must serve the files (do not open `index.html` directly).
- Standard run command (see `README.md`): `python3 -m http.server 4173`, then open `http://localhost:4173`.

### Build / lint / test
- **No build step**, no package manager, no lockfiles, and **no dependencies** to install (no `package.json`/`requirements.txt`/etc.).
- There is **no automated test suite and no linter** configured. Testing is manual in a browser: click `Старт` (Start) to generate the board, then play the core loop (pick a color from the bottom palette → capture adjacent same-color tiles → computer moves → win/draw check).

### Gotchas
- Docs (`README.md`, `REQUIREMENTS.md`, `todo.md`) are in Russian.
- The build/version label shown on the start screen comes from `CACHE_NAME` in `sw.js`. The service worker caches the app shell, so after editing files you may need to hard-reload / clear the service worker cache (or bump `CACHE_NAME`) to see changes.
- Game state, board, undo history, and field-size settings persist in `localStorage`.

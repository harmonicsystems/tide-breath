# Tide Breath

A quiet breath pacer. Single `index.html`, no framework, no build, no backend.
Live at https://harmonicsystems.github.io/tide-breath/ (GitHub Pages, served from `main` root).

- The URL hash is the pattern (`#4-7-8-0` = in·hold·out·hold seconds) and the source of truth; localStorage only remembers the last one.
- PWA: `manifest.webmanifest` + `sw.js`. **Bump `VERSION` in `sw.js` on every deploy** or installed phones keep the old cache (navigations are network-first, so online users still get fresh HTML).
- iOS audio must be unlocked inside a tap (`audioUnlock()` on Begin); the hardware silent switch mutes Web Audio.
- Screen Wake Lock is held only while running.
- Icons are rendered from `icons/icon.svg`: `magick -background none -density 300 icons/icon.svg -resize 192x192 icons/icon-192.png` (also 180, 512).
- Local dev: `python3 -m http.server 8765` (service workers don't run on `file://`).
- Repo uses the `github-harmonicsystems` SSH alias.

# Tide Breath

A quiet breath pacer. Single `index.html`, no framework, no build, no backend.
Live at https://harmonicsystems.github.io/tide-breath/ (GitHub Pages, served from `main` root).

- The URL hash is the pattern (`#4-7-8-0` = in·hold·out·hold seconds) and the source of truth; localStorage only remembers the last one.
- PWA: `manifest.webmanifest` + `sw.js`. **Bump `VERSION` in `sw.js` on every deploy** or installed phones keep the old cache (navigations are network-first, so online users still get fresh HTML).
- **Wash loops** (`audio/wash-{key}.m4a`): 34s cuts (from 60s in) of David's "Wash" bounces (`~/Music/Logic/washer/Bounces/fixed/`), loudness-matched to −16 LUFS, 96k AAC, ~400 KB each. Wash is released publicly via DistroKid, so public hosting is fine. The page crossfades each pass into the next (XF = 4s) — no reliance on gapless decoding. Only the chosen key is fetched; the SW keeps loops in a separate `AUDIO` cache that survives `VERSION` bumps.
- **Swell**: wash → lowpass → gain; inhale ramps up (louder/brighter), exhale ramps down, holds stay put, exactly over the phase duration. Swell slider sets the floor depth. Pattern changes mid-session keep the wash flowing (`restart` → `stop(true)/start(true)`).
- **Cues** are tones in the key: octave = breathe in, fifth = hold, root = breathe out; "Every count" adds a very soft octave tick per second.
- Sound settings live in localStorage (`tide-breath-sound`); the pattern stays in the hash.
- iOS audio must be unlocked inside a tap (`audioUnlock()` on Begin); `navigator.audioSession.type = 'playback'` lets it play through the silent switch (Safari 17+).
- Screen Wake Lock is held only while running.
- Icons are rendered from `icons/icon.svg`: `magick -background none -density 300 icons/icon.svg -resize 192x192 icons/icon-192.png` (also 180, 512).
- Local dev: `python3 -m http.server 8765` (service workers don't run on `file://`).
- Repo uses the `github-harmonicsystems` SSH alias.

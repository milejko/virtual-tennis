# Virtual Tennis

**[▶ Play now → milejko.github.io/virtual-tennis](https://milejko.github.io/virtual-tennis)**

---

A browser-based tennis game inspired by the classic Pong — built with vanilla HTML, CSS, and JavaScript. No installation, no frameworks, no dependencies beyond a single CDN library for online multiplayer. Just open the link and play.

---

## Features

- **Single Player** — face an AI opponent at three difficulty levels: Easy, Medium, and Hard
- **Online Multiplayer** — play against a friend on any device via peer-to-peer WebRTC (no server required)
- **Authentic Tennis Scoring** — 15 / 30 / 40 / game · 4 games per set · best of 3 sets
- **Adaptive Difficulty** — ball speed increases by 10% with each set, keeping every match tense
- **Synthesised Sound** — paddle hits, wall bounces, and point sounds via Web Audio API (no audio files)
- **Fully Responsive** — scales to any screen; playable on desktop, tablet, and phone

---

## Controls

| Action | Input |
|---|---|
| Move paddle | Mouse / trackpad · Arrow keys ↑ ↓ · Finger drag |
| Serve | Space · Click · Tap |

---

## Multiplayer

One player creates a game and shares the 6-character room code. The other player enters it on the Join screen. The connection is peer-to-peer — the host runs the physics and streams game state; the guest controls their own paddle locally for zero perceived latency.

---

## Scoring

```
Points  15 → 30 → 40 → Game   (no deuce — first to reach Game at 40:40 wins)
Set     First to 4 games
Match   Best of 3 sets
```

---

## Technology

| Concern | Solution |
|---|---|
| Rendering | `<canvas>` · `requestAnimationFrame` |
| Multiplayer | WebRTC data channel via [PeerJS 1.5.4](https://peerjs.com) |
| Audio | Web Audio API — synthesised tones |
| Distribution | Single `index.html` file |

---

## Running Locally

No build step required. Open `index.html` directly in any modern browser:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

Or serve it with any static file server:

```bash
npx serve .
```

---

## License

MIT

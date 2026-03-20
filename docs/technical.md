# Technical Specification: Virtual Tennis / Pong

## Technology
- Plain HTML / CSS / JS (no frameworks)
- Single file: `index.html`
- External library: **PeerJS 1.5.4** (loaded from jsDelivr CDN) — used only for 2P mode

## Rendering
- `<canvas>` element stretched to full screen (100vw × 100vh)
- Black background
- Game loop driven by `requestAnimationFrame`

## Visual Elements
- Paddles: thin white rectangles on each side of the screen
- Ball: white square
- Net: vertical dashed line at screen centre
- HUD: white monospace text at the top of the screen

## Sounds
- Web Audio API — synthesised tones, no external audio files
- Short programmatic tones for: paddle hit, wall bounce, point scored

## Controls
- `mousemove` — tracks mouse Y position
- `keydown` / `keyup` for arrow keys ↑ / ↓
- `touchstart` / `touchmove` — finger drag for paddle; short tap triggers serve

## AI
- Logic runs in the main JS game loop (1P mode only)
- Difficulty levels differ by reaction delay and position overshoot offset

## 2P Multiplayer — Network Architecture
- Transport: **WebRTC data channel** via **PeerJS**
- No custom server required; PeerJS provides a free signalling server
- **Host** (Player 1): generates a 6-character room code, runs physics, broadcasts game state
- **Guest** (Player 2): enters the code, connects peer-to-peer, sends paddle position
- Per-frame protocol:
  - Host → Guest: `{t:'g', bx, by, p1y, p2y, pp, ap, pg, ag, ps, as, cs, ws, sv, snd}`
  - Guest → Host: `{t:'p', y}` — paddle Y as a fraction of screen height
- Guest controls their own paddle locally (zero perceived latency); everything else rendered from host state
- Sounds: host plays locally and forwards the sound code to guest via `snd` field

## Non-Functional Requirements

### Device Compatibility
- Desktop (mouse + keyboard)
- Tablet (touch)
- Phone (touch)

### Responsiveness
- Canvas scales to window/screen size
- All positions and sizes expressed as fractions of canvas dimensions
- HUD legible on small screens (font size scales)
- On smaller screens, gameplay is proportionally easier:
  - slightly lower ball speed
  - slightly longer paddles

### Performance
- Target: 60 FPS on typical mobile and desktop devices

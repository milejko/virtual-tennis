# Gameplay: Virtual Tennis / Pong

## Court
- Open court — no side walls (ball exiting left/right = point for opponent)
- Top and bottom edges: ball bounces
- Tennis net in the centre (decorative, does not block the ball)

## Game Modes
- **1 Player**: player vs AI — difficulty selected on the start screen
- **2 Players (Online)**: player vs player over WebRTC (PeerJS) on two separate devices

## Players
- **Player 1 (left)**: paddle controlled by the local player
- **Player 2 (right)**: in 1P mode — AI; in 2P mode — remote player

## Controls (Player 1 / 2P guest)
- Mouse / trackpad — vertical paddle movement
- Arrow keys ↑ / ↓ — alternative control
- Finger drag (touch) — on mobile/tablet

## Serve
- Player 1 always serves first at match start
- After each point, the winner serves next
- The ball rests on the serving paddle (follows it until served), as in real tennis
- Serve is triggered by: **Space**, **click**, or **tap**
- In 1P mode: if AI serves, it auto-serves after ~1 second

## Ball
- Bounced between paddles left and right
- Bounces off top and bottom edges
- Speed: constant within a set, increases by 10% with each new set (set 10 = 2× set 1 speed)
- Bounce angle depends on where the ball hits the paddle:
  - Centre hit → shallow angle (nearly horizontal)
  - Edge hit → steep angle

## Paddle Speed
- Player and AI paddle speeds are identical
- Both scale with ball speed (+10% per set)
- AI difficulty affects reaction precision only, not paddle speed

## AI (Player 2 in 1P mode)
- Difficulty selected on the start screen
- Imperfection mechanics on lower difficulty levels:
  - **Reaction delay**: AI starts moving after a delay when ball direction changes
  - **Position overshoot**: AI aims slightly above/below the ball (random offset), causing misses or corrections

| Level  | Reaction delay | Position overshoot |
|--------|---------------|-------------------|
| Easy   | large         | large             |
| Medium | small         | small             |
| Hard   | none          | none              |

## Scoring
- Tennis scoring: 15 / 30 / 40 / game
- 4 games per set
- Best of 3 sets (first to win 2 sets wins the match)
- **No deuce**: at 40:40 the next point wins the game

## HUD
- Score displayed at the top centre, separately for each player
- Format: `points  |  games  |  sets`

## Sounds
- Ball hitting a paddle
- Ball bouncing off top/bottom edge
- Point scored

## Screens
1. **Main menu**: title + 1P/2P toggle + difficulty (1P only) + Start
2. **2P host**: room code displayed, waiting for guest to connect
3. **2P guest**: code input field + Connect
4. **Game**: fullscreen court + HUD, no pause
5. **Match end**: final score + "Play again" / "Request rematch" + "Main menu"

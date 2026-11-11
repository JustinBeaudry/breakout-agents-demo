# Breakout: Specification

Written from `intent.md`. This file is the agreement about what the game does. If the game and this file disagree, one of them is wrong. Fix the spec first, then the code.

## Artifacts

Each stage ends by committing a file the next stage reads. The commit history is the record of what was decided and when.

| Stage | Artifact | Holds |
|---|---|---|
| Plan | `intent.md` | The problem, the outcome wanted, constraints, open questions |
| Plan | `backlog.md` | Feature pitches from the room, and which one won each round |
| Design | `spec.md` | Exact behavior and what done means |
| Build | `plan.md` | The accepted implementation plan: files, order of work, risks, and how each step is proven |
| Build | Code and tests | The diff, and a test for each rule |

Nothing is implemented without an accepted `plan.md`. If the implementation departs from the plan, `plan.md` is updated in the same commit.

## Constraints

- No dependencies. No build step. No network requests at runtime.
- Runs in a current desktop browser from a static file server.
- Game rules are testable without a browser.
- Simple shapes drawn on one canvas. No images, no sound.

## Files

| Path | Holds |
|---|---|
| `index.html` | One canvas, loads `src/main.js` as a module |
| `src/game.js` | All game rules. Pure functions. No DOM, no canvas, no timers, no `Date` |
| `src/main.js` | Keyboard input, the animation loop, drawing |
| `test/game.test.js` | Tests for `src/game.js` using `node:test` |
| `package.json` | `"type": "module"` and a `test` script. No dependencies |

## Commands

| Task | Command |
|---|---|
| Run the tests | `node --test` |
| Serve the game | `python3 -m http.server 8000`, then open `http://localhost:8000` |

Opening `index.html` from the file system does not work. Browsers block modules loaded from `file://`.

## Time

The game never reads the clock. `src/game.js` exports an update function that takes the current state, the current input, and `dt` in seconds, and returns the next state. `src/main.js` measures real elapsed time and passes it in.

- `dt` is clamped to a maximum of 1/30 second per update.
- Anything that lasts a duration is stored as remaining seconds in the state and counted down by `dt`.

## Playfield

| Thing | Value |
|---|---|
| Field | 800 wide, 600 high. Origin top left |
| Paddle | 100 wide, 12 high. Top edge at y = 560. Starts centered |
| Paddle speed | 480 per second. Cannot leave the field |
| Ball | Radius 8. Constant speed 300 per second |
| Bricks | 12 bricks. 2 rows of 6. Each 100 wide, 24 high, 20 apart. Rows start at y = 80 |
| Lives | 3 |
| Score | 10 per brick |

## Controls

| Key | Action |
|---|---|
| Left arrow, Right arrow | Move the paddle |
| Space | Launch the ball |
| R | Restart, in any state |

## States

| State | Meaning |
|---|---|
| `ready` | Ball rests on the paddle and moves with it. Space launches it |
| `playing` | Ball is in motion |
| `won` | No bricks remain. Nothing moves |
| `lost` | No lives remain. Nothing moves |

## Rules

1. The game starts in `ready` with score 0, 3 lives, and 12 bricks.
2. In `ready`, Space launches the ball upward and the state becomes `playing`.
3. The ball reflects off the left, right, and top walls.
4. The ball reflects upward off the paddle. The outgoing angle depends on where it hit: center goes straight up, the edges go up to 60 degrees from vertical. Speed stays constant.
5. When the ball hits a brick, the brick is removed, the score increases by 10, and the ball reflects. At most one brick is removed per update.
6. When the ball passes the bottom edge, the player loses one life.
7. When the last life is lost, the state becomes `lost`.
8. When the last brick is removed, the state becomes `won`.
9. R restores exactly the state described in rule 1, from any state.
10. The screen always shows the score and remaining lives. In `ready`, `won`, and `lost` it also shows what key to press.
11. Undecided: what happens to the ball after a life is lost with lives remaining. See the open question in `intent.md`. Replace this rule with the answer before building.

## Features

Each feature added after the first version gets its own heading here, with its own numbered rules, written before any code for it.

- None yet.

## Done means

- `plan.md` was accepted before any code was written, and it matches what was built.
- `node --test` passes, with at least one test per numbered rule that `src/game.js` can check (rules 1 to 9, and rule 11 once decided).
- A person has played the game in a browser and seen: a brick removed and the score change, a life lost, a restart, and either a win or a loss.
- Every line of the change can be explained by whoever approved it.

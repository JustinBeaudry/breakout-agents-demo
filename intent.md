# Breakout: Intent

Owner: Justin Beaudry. Status: accepted, with one open question.

This file says why the work exists. `spec.md` is written from it. If the two disagree, fix this file first.

## Problem

A one hour workshop on building with coding agents needs something to build. It has to be small enough to finish live and have enough behavior that planning, testing, review, and a recorded lesson all have real work to do.

## Proposed outcome

A small Breakout game, built live by a coding agent, whose rules can be checked by a test.

## Affected users and systems

- The presenter, who directs the agent and plays the game in a desktop browser.
- The room, who answer the open questions and judge the result.
- No other systems. No network, no accounts, no stored data.

## Constraints

- The first playable version has to fit in about fifteen minutes of agent time.
- No dependencies and no build step, so nothing can fail to install on stage.
- Every rule must be checkable without a browser and without waiting on a real clock.

## Open questions

Each one is answered with the room, recorded in `spec.md`, and then removed from this list.

- After losing a life with lives remaining, does the ball relaunch on its own, or wait on the paddle for Space?

## Not intended

Sound, multiple levels, mouse or touch input, high scores, pause, mobile layout. Power-ups are not part of the first version. A later change may add one, starting with a change to this file.

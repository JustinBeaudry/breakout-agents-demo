# AGENTS.md

Standing instructions for any coding agent working in this repository. Read this and `SPEC.md` before every task.

## Project

A small Breakout game used as a live workshop demo. `SPEC.md` is the source of truth for behavior, file layout, and commands.

## Commands

- Tests: `node --test`
- Serve: `python3 -m http.server 8000`, then `http://localhost:8000`

## Boundaries

- No dependencies. Do not run `npm install`. Do not add a bundler, framework, test library, or linter.
- No network requests from the game.
- Do not read or write outside this repository.
- `src/game.js` holds every rule and stays pure: no DOM, no canvas, no timers, no `Date`, no `Math.random` without an injected source.
- `src/main.js` holds input, the animation loop, and drawing. It contains no rules.
- Time enters the game only as the `dt` argument. Durations are stored as remaining seconds in state.

## How to work

1. Plan first. For any change touching more than one file, write a short plan and wait for approval before editing. List any behavior `SPEC.md` leaves undecided as a question. Do not guess.
2. Spec before code. If a task changes behavior, update `SPEC.md` in the same change.
3. Test first. Write the failing test for a rule, run it, watch it fail, then implement.
4. One logical change at a time. Keep each diff small enough to read in full.
5. If three attempts to fix the same failure do not work, stop and say so. The plan is wrong.
6. Commit after each completed, passing step, with a message that says what changed and why.

## Done

Do not say a task is done until all of these are true:

- `node --test` was run after the last edit and its output is shown.
- Each new or changed rule in `SPEC.md` has a test.
- The summary states what changed, what was verified and how, and what was not verified.

Passing tests show the rules hold. They do not show the game plays correctly. Say which browser checks a person still needs to do.

## Review

When asked to review a change:

- Do not modify source files.
- Check the change against `SPEC.md` rule by rule.
- For each finding give: file and line, the condition that triggers it, expected behavior, actual behavior, and whether it was reproduced or found by reading.
- Report the checks actually run and anything left unverified.
- If nothing is wrong, say so. Do not invent findings.

When acting on a review:

- Evaluate each finding against `SPEC.md` before changing anything.
- Reproduce a supported finding with a failing test, then make the smallest fix.
- State disagreement with a finding, with evidence.

## Lessons

Rules learned from mistakes in this repository. Add one line per lesson, written so it prevents the whole family of bug, not the single instance.

- None yet.

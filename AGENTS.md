# AGENTS.md

Standing instructions for any coding agent working in this repository. Read this, `intent.md`, and `spec.md` before every task. Read `plan.md` if it exists.

## Project

A small Breakout game used as a live workshop demo. `intent.md` says why it exists. `spec.md` is the source of truth for behavior, file layout, and commands. `plan.md` is the accepted implementation plan.

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

1. Plan first. Nothing is implemented without an accepted plan. Write the plan, list any behavior `spec.md` leaves undecided as a question, and wait for approval. Do not guess. The plan names the files, the order of work, the riskiest step, and how each step is proven.
2. Commit the accepted plan as `plan.md` before writing code.
3. Intent, then spec, then code. If a task changes behavior, update `spec.md` in the same change. If it changes why the work exists, update `intent.md` first.
4. Test first. Write the failing test for a rule, run it, watch it fail, then implement.
5. One logical change at a time. Keep each diff small enough to read in full.
6. If the implementation departs from the plan, update `plan.md` in the same commit.
7. If three attempts to fix the same failure do not work, stop and say so. The plan is wrong.
8. Commit after each completed, passing step, with a message that says what changed and why.

## When something breaks

1. Diagnose before changing anything. Say what the cause is and how you know.
2. Write a test that fails because of the bug. Run it and confirm it fails for that reason. Commit it.
3. Fix the code until that test passes. Do not edit the test to make it pass.
4. Never skip or delete a failing test.
5. If the same mistake has now happened twice, add the correction to Lessons below.

## Done

Do not say a task is done until all of these are true:

- `node --test` was run after the last edit and its output is shown.
- Each new or changed rule in `spec.md` has a test.
- `plan.md` matches what was built.
- The summary states what changed, what was verified and how, and what was not verified.

Passing tests show the rules hold. They do not show the game plays correctly. Say which browser checks a person still needs to do.

## Review

When asked to review or verify a change:

- Work from `spec.md`, `plan.md`, and the diff. Do not rely on the conversation that produced the change.
- Report. Do not fix. Do not modify source files.
- Check the change against `spec.md` rule by rule.
- For each finding give: file and line, the condition that triggers it, expected behavior, actual behavior, and whether it was reproduced or found by reading.
- Report the checks actually run, what they showed, and anything left unverified.
- If nothing is wrong, say so. Do not invent findings.

When acting on a review:

- Evaluate each finding against `spec.md` before changing anything.
- Handle a supported finding as described under When something breaks.
- State disagreement with a finding, with evidence.

## Lessons

Rules learned from mistakes in this repository. Add one line per lesson, written so it prevents the whole family of bug, not the single instance.

- None yet.

# DSA

Pattern-organised. Java by default. 112 core problems, 14 stretch (†) and 22 timed-set problems across weeks 1–8; week 8 is revision and timed sets only. The full list with week assignments is `problem-list.md`.

## Files

- `patterns/<pattern>.md` — when to recognise it (the tell), the template, the traps. Generated with each week's curriculum.
- `problems/<pattern>/<slug>.md` — one file per problem: statement, your attempt (verbatim, including the wrong ones), model solution, complexity, **the insight that unlocks it**.
- `revision/queue.md` — the spaced-repetition queue. Read it every morning before new problems.

## Daily protocol (08:45–09:30)

1. Open `revision/queue.md`. Re-solve everything due today, from scratch, timed (10 min cap each, max 2 per day; extras roll to tomorrow). Mark clean / not clean.
2. Then today's new problems from `PLAN.md`. Core first. Stretch only if the queue is clear.
3. For each new problem, before coding: what pattern is this, and what is the tell. After: complexity, and the one-line insight.
4. Stuck for 15 minutes → `/stuck <problem>` with what you tried.

## Hint protocol

nudge → bigger nudge → approach without code → code. If you ask for the answer directly you will be asked once what you tried, then given it. The point is learning to notice, not collecting solutions.

## Spaced repetition

Solved on day D → re-solve on D+1, D+3, D+7, D+21. Two clean re-solves in a row graduate the problem. A failed re-solve resets it to D+1. Re-solving means from a blank file; re-reading does not count.

## Timed sets

Every Saturday 09:15–10:00: two unseen problems, 45 minutes, no hints, no IDE autocomplete. Score each 0 (no working solution), 1 (works, suboptimal or bugs), 2 (clean and optimal). Log the score. Week 8 runs one every weekday morning instead of new problems.

## Scoring yourself honestly

"Recalled" (seen it before, remembered the trick) is not "reasoned" (derived it). Mark each solve R or D in the problem file. Interviews test D; a queue full of R is a warning.

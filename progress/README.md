# Progress

- `state.json` — current position. Gitignored. Updated by `/today`, `/review`, `/progress`, `/replan`.
- `flashcards.json` — the spaced-repetition deck. Array of cards:
  `{ "id", "front", "back", "module", "created": "YYYY-MM-DD", "due": "YYYY-MM-DD", "interval_days", "ease", "reps" }`.
  `/review` shows cards due today, asks you to answer aloud, then grades 0–3; interval grows on 2–3, resets on 0–1.
- `log/YYYY-MM-DD.md` — one per day. Minimum: what was done, what was not, one thing that confused you, DSA results (problem, R/D, clean?), gym drill time and score.
- `log/YYYY-MM-DD-week-review.md` — Sunday. Quiz scores per module (0–5), timed-set score, problems solved vs planned, what slipped, next week's adjustment.

## Day log template

```markdown
# 2026-09-21 — Day 1

## Done
-

## Not done (and why)
-

## DSA
| Problem | Pattern | R/D | Clean | Time |
|---|---|---|---|---|

## Gym drill
Drill 01 · time: · score: /4 · what I missed:

## One thing that confused me


## Carry over to tomorrow
-
```

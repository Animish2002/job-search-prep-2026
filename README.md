# Job search prep 2026

Eight-week interview-preparation system for Animish Chopade. Target: Java/Spring backend engineer who is genuinely full-stack, 10–15 LPA, interview-ready by 2026-11-15. The plan is `PLAN.md`. The rules the assistant follows are `CLAUDE.md`.

## Where things are

| Path | What |
|---|---|
| `PLAN.md` | All 56 days, dated, with time boxes and exit criteria. Start here. |
| `PROTOCOL.md` | How to run a day, a week and a month; what happens when you type "diagnostic done" and every other command. |
| `diagnostic/` | Phase 0: code audit of your repos, the five-part diagnostic, your answers, `RESULTS.md` once graded. |
| `curriculum/` | Nine tracks. Modules generated one week at a time; each has `README.md`, `mental-model.md`, `source-reading.md`, `build-it/`, `exercises/`, `interview-qa.md`, `failure-modes.md`. |
| `dsa/` | `problem-list.md` (the curated ~130, core vs stretch), `patterns/` (one file per pattern: when to recognise it, template), `problems/` (one file per solved problem), `revision/queue.md` (spaced repetition). |
| `code-reading-gym/` | 56 drills, one per day, 15 minutes, first thing. |
| `projects/` | `hardening/` (PrepArena + Kcal fixes with write-ups), `spring-service/` (DocDrop, your Java project), `walkthroughs/` (rehearsed spoken tours), `code-audit/` (pointer to the audit). |
| `interview/` | `behavioural/stories.md`, `hard-questions.md`, `mocks/` (transcripts + feedback), `company-research/`, `salary-negotiation.md`. |
| `career/` | `resume/`, `linkedin.md`, `target-companies.md`, `application-tracker.md`. |
| `progress/` | `state.json` (gitignored), `flashcards.json`, `log/YYYY-MM-DD.md` one per day, week reviews as `YYYY-MM-DD-week-review.md`. |

## The daily ritual

Built for an 11:00–20:00 office day with the gym in the morning. Two blocks, both required Mon–Thu.

**Morning, 08:30–10:00**
1. `/readcode` — the day's drill. 15 minutes, hard stop.
2. DSA — due re-solves first, then today's problems from `PLAN.md`. 45 minutes.
3. `/review` — flashcards. 10 minutes.

**Evening, 21:15–23:00**
4. `/today` shows the module. Theory, source reading, build-it. 75 minutes.
5. Exercises or the scheduled portfolio task. 25 minutes.
6. Log the day in `progress/log/`. Three lines minimum.

Friday: morning block only. Saturday: timed set, deep-dive block, portfolio block, applications. Sunday: mock, week review, career task; evening off. Full templates in `PLAN.md` §1.

## Commands

Type these as the first thing in a message.

| Command | What happens |
|---|---|
| `/today` | Today's blocks from `PLAN.md` with time boxes, plus anything carried over. |
| `/readcode` | Today's code-reading drill. Answer the four questions before asking for the answer. |
| `/explain <topic>` | Teaches it internals-first at your measured level, then tests you on it. |
| `/review` | Runs the flashcard queue and the DSA re-solve queue that is due. |
| `/quiz <module>` | Tests you on a module. Graded harshly, 0–5, with what was missing. |
| `/stuck <problem>` | Escalating hints: nudge → bigger nudge → approach → code. Say what you tried. |
| `/mock <dsa\|java-spring\|fullstack\|lld\|behavioural\|full-loop>` | A mock interview in character. Feedback written to `interview/mocks/`. |
| `/critique <file>` | Senior PR review of your code: correctness, edge cases, naming, structure, performance. |
| `/progress` | Where you are against `PLAN.md`, what is slipping, scores by track. |
| `/replan` | Re-cuts the remaining weeks from where you actually are. Use it after missed days; no catching up. |

## How to work with the assistant

- Answer diagnostic and quiz questions **without looking anything up**. A wrong answer with honest reasoning is worth more than a right answer that hides a gap.
- When stuck on DSA, describe what you tried before asking for a hint. Asking for the answer directly gets one question back, then the answer.
- It will not inflate your level, will refuse once if you try to skip DSA or the reading drill, and will push back if you try to grow the GenAI track at the expense of DSA or Java.
- Weak answers get told they are weak, and exactly what was missing. That is the product.

## Before Day 1 (Mon 2026-09-21)

1. Take the diagnostic this weekend: `diagnostic/README.md`. Then say "diagnostic done".
2. Put your resume PDF and its source in `career/resume/`.
3. Check whether a battle on the live PrepArena site opens a WebSocket successfully (see `diagnostic/CODE-AUDIT.md` §5.5).
4. Say "Day 1 starts now" on Monday morning. Week 1's curriculum is generated then.

# PROTOCOL.md — what you do, and what happens, from "diagnostic done" onward

This is the operating manual. `PLAN.md` says *what* each day contains. This file says *how* you run a day, a week and a month, and what the assistant does in response to each thing you type. Read it once fully, then keep it open.

---

## 0. The trigger: "diagnostic done"

You type **`diagnostic done`** after `diagnostic/answers/01`–`05` are filled in. Do not type it early; blank answers get graded as blank.

What happens, in order, before you do anything else:

1. **Grading.** Every part is graded harshly against the model answers. You get, per question, a score and one line on what was missing. Not "close", not "almost": exactly what a strong answer had that yours did not.
2. **`diagnostic/RESULTS.md` is written.** Per-topic levels 0–5 for: Java internals, JS semantics, SQL, HTTP/web, complexity, code reading (with time per snippet), DSA (with time per problem and recall vs reasoning), defending your own code, plus the self-report. Also the three biggest exposure points and the three things you are better at than you think.
3. **`/replan`.** Weeks 2–8 of `PLAN.md` are re-cut in place to what the results show. Week 1 does not change. Every change is listed under the week's heading with the reason ("SQL scored 1/5 → DB 04 hard SQL moved from Day 23 to Day 16; Day 23 becomes a second SQL day").
4. **Effort allocation is finalised** in `CLAUDE.md` with what moved and why.
5. **Week 1 curriculum is generated:** the five week-1 modules in `curriculum/` (each with `README.md`, `mental-model.md`, `source-reading.md`, `build-it/`, `exercises/`, `interview-qa.md`, `failure-modes.md`) and gym drills 01–07 in `code-reading-gym/`.
6. You are told: **"Day 1 starts now"**, and `/today` runs for Monday 2026-09-21.

If you skip the diagnostic and type `Day 1 starts now` instead, steps 5–6 run and steps 1–4 wait until you do the diagnostic. The plan works either way; it is just less accurate.

---

## 1. The daily protocol (Mon–Thu)

Two blocks. Both required. The order inside each block is fixed because the first item in each block is the one you would otherwise skip.

### Morning block — 08:30–10:00

**08:30 — Type `/readcode`.** (15 min, hard stop.)
- You get today's drill: a 20–60 line snippet and four questions.
- Answer all four *in the drill file* under "Your answers", without running the code, before asking for anything. Time yourself.
- Then say `check` and you get the model answers and a 0–4 score with what you missed.
- Write the time and score in the day's log at the end of the block.
- If 15 minutes pass and you are not done, stop and check anyway. Speed is the skill.

**08:45 — DSA.** (45 min.)
- Open `dsa/revision/queue.md`. Anything due today is re-solved first, from a blank file, 10-minute cap each, at most two. Mark clean or not clean in the queue.
- Then today's new problems, listed in `PLAN.md` under the day. Core before stretch. For each:
  1. Before coding, say the pattern and the tell out loud, then write the brute force complexity.
  2. Code it in Java. Run your own test cases including the edge case.
  3. Write complexity and the one-line insight.
  4. Save as `dsa/problems/<pattern>/<slug>.md` (your attempt verbatim, model solution, complexity, insight). Add the row to the revision queue with due dates +1, +3, +7, +21.
  5. Mark R (recalled) or D (derived).
- Stuck for 15 minutes → type `/stuck <problem>` and say what you tried. You get one nudge. Stuck again → a bigger nudge. Then the approach without code. Then code. You will never get a level skipped, and asking for the answer directly gets one question back first.
- If the re-solve queue eats the block, drop today's third problem to Saturday's block A. Never drop the re-solves.

**09:30 — Type `/review`.** (10 min.)
- You get the flashcards due today, one at a time. Answer out loud, then say `0`, `1`, `2` or `3` for how well you did. 2–3 grows the interval; 0–1 resets it to tomorrow.
- New cards from last night's module are added here.

**09:40 — Buffer.** (20 min.) Finish any DSA write-up, or read tonight's module `README.md` so the evening starts warm. Then leave for the office.

### Evening block — 21:15–23:00

**21:15 — Type `/today`.** You get the evening's module, the exercise, and anything carried over from yesterday's log, with time boxes.

**21:15–22:30 — The module.** (75 min.) In this order, always:
1. `README.md` opens with a situation from your stack and a question. Answer the question in writing *before* reading on. Wrong is fine; the point is to find the wrong assumption.
2. `mental-model.md` — one diagram or analogy. Redraw it yourself on paper.
3. `source-reading.md` — the real JDK/Spring/V8 implementation walked through. Have the actual source open beside it (`HashMap.java`, etc.).
4. `build-it/` on build days — implement the minimal version; the test suite must pass. Stop when it is green, not when it is pretty.
5. Say `quiz me` at any point and you get 5 questions from `interview-qa.md`, graded 0–5.

**22:30–22:55 — Exercise or portfolio task.** (25 min.) Whatever `PLAN.md` lists for the day under PM. Exercises are graded: type `check` when done.

**22:55–23:00 — Log the day.** Create `progress/log/YYYY-MM-DD.md` from the template in `progress/README.md`. Minimum: done, not done and why, the DSA table, the drill time and score, one thing that confused you, carry-over for tomorrow. Say `logged` and the state file is updated.

**23:30 — Sleep.** Not negotiable. If sleep drops under 6.5 h three nights running, say so; the evening block shrinks to 60 min for that week and the plan is re-cut.

### If the morning is short

Gym ran late, morning under 60 min: do `/readcode` and `/review` in the morning; DSA moves to 21:15 and the module starts at 22:00 shortened. Never skip DSA to fit the morning. Never skip the drill for anything.

---

## 2. Friday

Morning block only: `/readcode`, DSA (re-solves plus the day's problems), `/review`. Log it in the buffer. Evening off. This is the rest day. Do not "use it productively".

---

## 3. Saturday — 6 hours

| Time | What you type / do |
|---|---|
| 09:00 | `/readcode`. 15 min. |
| 09:15 | `timed set`. You get two unseen problems. 45 min, no hints, no autocomplete, no leaving the chair. At 10:00 say `time` and paste both solutions. Each scored 0/1/2. Score goes in the log and in `state.json`. |
| 10:00 | `/review`. |
| 10:15–12:30 | **Block A.** `/today` gives it. Usually a module plus the DSA problems the day lists. Same module order as weekdays. |
| 12:30–15:00 | Break. Eat. Leave the desk. |
| 15:00–17:30 | **Block B, portfolio.** The item from `projects/hardening/README.md` or `projects/spring-service/README.md` scheduled for the day. Rule: it is done when it is deployed or the tests are green *and* the write-up file exists. A fix without a write-up did not happen. Use `/critique <file>` on anything you wrote before you push it. |
| 17:30–18:15 | **Applications** (from 2026-10-03). Ten. Each one: pick the variant, tailor the first two bullets if the JD asks for something specific, send, add the row to `career/application-tracker.md`. Do not spend more than 5 minutes per application. |
| 18:15 | Log the day. |

---

## 4. Sunday — 5.5 hours, evening off

| Time | What you type / do |
|---|---|
| 09:00 | `/readcode`. |
| 09:15–10:15 | DSA: re-solves due, then the day's new problems. `/review`. |
| 10:15–11:45 | **Mock** (weeks 3–8): `/mock <type>` as listed in `interview/README.md`. It is in character from the first line. You are interrupted, asked "why" until you hit bedrock, and not helped. Speak your answers; type what you said. Do not look anything up. At the end you get hire / no-hire / borderline, the reasons, and the two things to fix before the next one. Weeks 1–2: walkthrough drafting instead (see `PLAN.md`). |
| 11:45–12:30 | Read the feedback file in `interview/mocks/`. Write your two fixes into next week's Monday carry-over. |
| 12:30–15:00 | Break. |
| 15:00–16:30 | **Week review** (§5 below). |
| 16:30–17:30 | **Career task of the week** from `PLAN.md` (stories, LinkedIn, hard questions, tracker review). |
| Evening | Off. |

---

## 5. The weekly protocol (Sunday 15:00–16:30)

Type **`week review`**. What happens:

1. **Quiz.** One `/quiz` per module covered this week, 6–8 questions each, spoken-length answers, graded 0–5. You do not get to re-read the module first. This is the honest measure of what stuck.
2. **Numbers.** Problems solved vs planned, re-solves clean vs failed, timed-set score, drill scores, gym drills done (must be 7), applications sent, mock verdict.
3. **What slipped.** Anything under 3/5 in the quiz, any core problem dropped twice, any portfolio item without a write-up.
4. **Adjustment.** Next week's `PLAN.md` blocks are edited in place: a re-teach slot is added for anything under 3/5 (it takes the first 20 minutes of Monday's evening block), dropped problems are placed into Saturday's block A, and anything you scored 5/5 on twice gets its flashcards spaced out. The changes and reasons are written under next week's heading.
5. **The review file** is written: `progress/log/YYYY-MM-DD-week-review.md`, with all of the above and your one-line note on how the week actually felt (tired, fine, bored: it matters for the next cut).

Then the career task. Then stop for the day.

---

## 6. The monthly protocol

Two checkpoints: **end of week 4 (Sun 2026-10-18)** and **end of week 8 (Sun 2026-11-15)**. On those Sundays the week review is replaced by a longer one, 15:00–17:30, and the career task moves to the following Monday's carry-over.

Type **`month review`**. What happens:

1. **Re-diagnostic.** A fresh, shorter version of the Phase 0 assessment: 12 written questions across the tracks covered so far, 2 cold code-reading snippets, 1 timed medium, and 3 "defend your code" questions on what you shipped this month. Graded exactly like Phase 0.
2. **`diagnostic/RESULTS-week-4.md`** (or `-week-8.md`): every track scored 0–5 next to its Phase 0 score. Anything that has not moved by at least one level in four weeks is named, and the reason is diagnosed (not enough hours, wrong method, or it was never actually the gap).
3. **Portfolio audit.** Every item in `projects/hardening/README.md` and the DocDrop table is checked: deployed, tested, written up, or not. Anything half-done is either finished in the next two weekends or explicitly cut, with the cut written down.
4. **Application funnel.** Sent, screens, OAs, rounds, offers from the tracker. If ten applications produced zero screens, the resume variant or the tier targeting is wrong and gets changed before the next batch. If interviews are happening, every real-interview rejection gets its "what went wrong" mapped to a plan change.
5. **Re-allocation.** The effort table in `CLAUDE.md` is redone for the remaining weeks from the evidence above. What moved and why is written into `PLAN.md` at the top of the next week.
6. **Month 2 specifics (Day 56).** The re-diagnostic is the full Phase 0 set minus the self-report. Then the weeks 9–12 plan is written into `PLAN.md`: applications continue at ten a week, one timed set and one mock a week, the revision queue until empty, and per-interview prep via the "I have an interview at <company>" prompt.

---

## 7. Things you type, and what they do

| You type | What happens |
|---|---|
| `diagnostic done` | §0. Grading, RESULTS, replan, week-1 curriculum, Day 1. |
| `Day 1 starts now` | Week-1 curriculum and drills generated; `/today`. |
| `/today` | The day's blocks from `PLAN.md` plus carry-over from the last log. |
| `/readcode` | Today's drill. `check` after answering. |
| `/review` | Flashcards due; DSA re-solves due are listed too. |
| `/stuck <problem>` + what you tried | One hint level at a time. |
| `/explain <topic>` | Internals-first teaching at your measured level, then a test on it. Use "assume my mental model is wrong, not incomplete" when something will not click. |
| `/quiz <module>` | 6–8 questions, graded 0–5, what was missing. |
| `quiz me` (inside a module) | 5 questions from that module's `interview-qa.md`. |
| `timed set` | Saturday's two unseen problems, 45 min. `time` to stop. |
| `/critique <file>` | Senior PR review before you push portfolio code. |
| `/mock <dsa\|java-spring\|fullstack\|lld\|behavioural\|full-loop>` | In-character mock; feedback file written. |
| `week review` | §5. |
| `month review` | §6. |
| `/progress` | Where you are against the plan, by track, with what is slipping. |
| `/replan` | Re-cuts the remaining days from where you actually are. Use after missed days. No catching up, ever. |
| `I have an interview at <company> for <role> on <date>. JD: ...` | Company loop research, JD mapped to your level, three exposure points, a targeted mock. Written to `interview/company-research/<company>.md`. |
| `logged` | State file updated from today's log. |

---

## 8. Rules you will be held to

1. The reading drill is never skipped. Ask to skip it and you will be refused once with the cost, then it is your call.
2. Same for DSA.
3. No looking things up during quizzes, drills, timed sets or mocks. Interviews do not have tabs.
4. A weak answer is called weak, and you are told exactly what was missing. That is the product; do not argue with it, fix it.
5. If you ask to grow the GenAI track at the expense of DSA or Java: "GenAI is a differentiator, not a foundation."
6. If you disappear for days: come back, type `/replan`, continue. No apology needed, no catching up allowed.
7. Every resume bullet must be true. Five are not yet (`career/resume/README.md`). They become true on the scheduled days or get reworded.
8. Sleep before study. Seven hours. Week 7 needs you functional.

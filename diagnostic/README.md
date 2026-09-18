# Phase 0 — Diagnostic

This is not a test you pass. It is a measurement. Every question is designed to expose a specific misconception, and a wrong answer with honest reasoning is worth more to the plan than a right answer you looked up.

## Rules

1. **No searching, no docs, no AI, no IDE autocomplete while answering.** Interviews don't have them. If you don't know, write "I don't know" and then write your best guess, labelled as a guess. Guesses reveal how you think; blanks reveal nothing.
2. **Time-box each part** as listed below. When time runs out, stop and mark where you were. Speed is part of the measurement.
3. **Write answers in `diagnostic/answers/`**, one file per part, using the skeletons already there. Keep the question numbers.
4. **Answer out loud first** for parts 02 and 04, then write what you said. The interview is spoken. If you can record yourself on your phone, do it; you don't need to share the recording, but you'll learn something listening back.
5. **Do the parts in order.** Part 04 is deliberately last because it is the most uncomfortable.

## Parts and time budget

| Part | File | Time | What it measures |
|---|---|---|---|
| 01 | `01-written-assessment.md` | 90 min | Java internals, JS semantics, SQL, HTTP, complexity |
| 02 | `02-code-reading.md` | 60 min | Reading unfamiliar code cold (your stated weakness) |
| 03 | `03-dsa-problems.md` | 70 min | Timed problem solving in Java, no hints |
| 04 | `04-defend-your-code.md` | 90 min | Explaining your own shipped code under interrogation |
| 05 | `05-self-report.md` | 20 min | Topics you have never touched |

Total ≈ 5.5 hours. That is one weekend day. Do 01–03 on Saturday and 04–05 on Sunday if you'd rather split it.

## After you finish

Tell me "diagnostic done" (or run `/quiz diagnostic`). I will grade every part, write `diagnostic/RESULTS.md` with per-topic levels 0–5, revise the effort allocation with reasons, and only then generate `PLAN.md` and the curriculum.

Read `CODE-AUDIT.md` **after** part 04, not before. It contains answers to several part 04 questions.

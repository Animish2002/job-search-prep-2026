# Resume

`animish-chopade-resume-2026-09.md` is the current resume as received on 2026-09-19 (Markdown export). Still wanted: the PDF you actually send out and the source (`.docx` / Google Doc / `.tex`) so the week-1 edit produces a file you can submit, not just text.

## Week-1 edit (Sat 2026-09-26, 2 h) — what changes and why

Reframe, do not rewrite. Specific fixes, in order:

1. **Qnopy bullets undersell platform ownership.** "Migrated the entire legacy UI" reads as CSS work. It was: four production modules moved to a new design system, a shared SCSS token system, and a component library (tables, search fields, date pickers, buttons, single/multi-select, toasts, sidebars) with RxJS underneath that every module now depends on. Lead with scope and reuse; add the component types and RxJS explicitly (recruiters keyword-match on them).
2. **Quantify only what is true.** Modules migrated (4), shared components (count them), and any honest measure of duplicate code removed. No invented percentages.
3. **Surface the patent** into the summary's first line and keep the Achievements block.
4. **Aug 2024 – Oct 2025** must read as deliberate independent product work (PrepArena, Kcal, Technical Spark all shipped in that window), not as a gap. Add a one-line "Independent Product Engineer / Freelance" entry with dates.
5. **Resolve claims the code does not support** (from `diagnostic/CODE-AUDIT.md` §1 and §5):
   - "provider-agnostic AI abstraction ... zero-route-change swaps": the main `/api/analyze` route bypasses the factory. Either route it through `getAIProvider` (2 h, scheduled Day 45) or soften the wording.
   - "per-user rate limiter (20 req/hr)": it is per-isolate. Fix (Durable Object or Rate Limiting binding, scheduled Day 45) or say "best-effort".
   - "spaced repetition ... per-problem confidence tracking": intervals are fixed; confidence is stored and ignored. Implement SM-2 (≈30 lines, Day 40) or say "scheduled revision".
   - "Gemini 2.0 Flash": code uses `gemini-2.5-flash-lite`. Match the resume to the code.
   - "Spring Data JPA / Hibernate": stays, and becomes defensible in week 2 (persistence context, lazy loading, N+1, `@Transactional`).
6. **Skills ordering** for the Java-backend variant: Java, Spring Boot, Spring Data JPA/Hibernate, MySQL/PostgreSQL, REST, then TypeScript/React.

## Variants (generated after the edit)

- `variant-java-backend.md` — primary. Sent to Java/Spring roles.
- `variant-full-stack.md` — Angular/React design-system work and PrepArena lead.
- `variant-ai-engineering.md` — Kcal + the RAG/agent feature from week 7 lead; only used for AI-product roles.

# Hardening PrepArena and Kcal

Ordered by interview signal per hour (from `diagnostic/CODE-AUDIT.md` §7). Each item gets a write-up file here when done: what was wrong, the evidence, the fix, the numbers. These write-ups are what you talk from in interviews.

| # | Item | Day | Est. | Write-up |
|---|---|---|---|---|
| 0 | Confirm whether the battle WebSocket authenticates in production (audit §5.5 `[VERIFY]`) | 0 | 15 min | in `01` |
| 1 | Missing indexes on both databases, `EXPLAIN QUERY PLAN` before/after for three queries | 6 | 2 h | `01-indexes-explain.md` |
| 2 | Reproduce and fix the Kcal `daily_summaries` lost update; unique constraint | 13 | 1.5 h | `02-lost-update.md` |
| 3 | Vitest + unit tests on the pure functions; GitHub Actions on both repos | 20 | 3 h | `03-tests-ci.md` |
| 4 | Idempotent `/internal/battles/:id/complete` with `WHERE status='active'` and `db.batch` | 20 | 1 h | `04-idempotent-completion.md` |
| 5 | List every `await` in the DOs the input gate does not cover | 32 | 30 min | `05-do-concurrency.md` |
| 6 | BattleRoom fixes: WS auth, one clock from accept, server-decided completion, verified solves, atomic accept, fair problem selection; `onError` + zod on battle routes | 34 | 2.5 h | `06-battleroom-fixes.md` |
| 7 | Kcal AI layer: route through `getAIProvider`, JSON schema output, retry only on 5xx with backoff, 502 mapping, key in header; per-user rate limiter on a DO or the Rate Limiting binding | 45 (48) | 2.5 h | `07-kcal-ai-layer.md` |
| 8 | SM-2 in `scheduleRevisions` so "confidence tracking" is true | 40 or 48 | 30 min | in `08` |
| 9 | RAG or agent feature in PrepArena with an eval set and numbers | 48 | 2.5 h | `08-rag-feature.md` |
| 10 | READMEs for hiring managers (PrepArena, Kcal, DocDrop) | 55 | 2.5 h | in each repo |

Not scheduled, do if a weekend runs long: R2 lifecycle rule for orphaned images, constant-time password compare, `?token=` only on the upgrade route, `NetworkFirst` cache cleared on logout, the two definitions of "week" merged.

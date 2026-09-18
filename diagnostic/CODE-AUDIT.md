# Code Audit — PrepArena, Kcal backend, Kcal frontend

Read on 2026-09-19 from fresh clones (PrepArena @ d8db03b, kcalapp-backend @ 384050c, kcal.app-frontend @ 6a46ad9).
This is written to be used, not to be pleasant. Every claim cites a file so you can check it.

---

## 1. Verdict in five lines

1. You ship. Three deployed products, a browser extension that patches `fetch`/XHR inside LeetCode, three Durable Objects, OAuth with CSRF state, cron jobs, R2 lifecycle. Most 2-YOE candidates have a todo app.
2. You build *around* the data layer, not *with* it. No non-unique index exists in either database. Read-modify-write counters. Five sequential writes with no transaction. Table scans everywhere. This is the single biggest technical gap and it maps directly onto the Java/Spring/SQL interview.
3. You use concurrency primitives (Durable Objects, alarms, WebSockets) correctly by instinct and incorrectly by reasoning. The code works at 10 users because nothing races at 10 users.
4. Zero tests, zero CI, zero runtime validation of request bodies in PrepArena. An interviewer opening either repo sees that in the first 30 seconds.
5. Several resume claims are stronger than the code: "provider-agnostic AI layer" (the main route bypasses it), "20 req/hr per-user rate limiter" (per-isolate, resets randomly), "spaced repetition with confidence tracking" (fixed intervals; confidence is stored and ignored). These must become true or be reworded before week 2.

---

## 2. What the code proves you can genuinely do

- **End-to-end product thinking.** PrepArena has auth → problems → progress → XP → challenges → battles → chat → extension. Each feature has a schema, a route, a store, a page. Nothing is half-wired.
- **Cloudflare platform fluency.** Hibernation WebSocket API with `serializeAttachment` (`apps/api/src/durable/BattleRoom.ts:76-77`), alarms (`:72`), `idFromName` routing, `ctx.waitUntil` in the scheduled handler, KV with TTL for OAuth state (`routes/auth.ts:69`), R2 custom metadata. This is real and uncommon.
- **Good security instincts in places.** OAuth `state` stored in KV with a 10-minute TTL and deleted on use (`routes/auth.ts:99-104`). Generic "invalid email or password" on login (`kcalapp-backend/src/routes/auth.ts:83-85`). Image ownership enforced by key prefix (`routes/images.ts:47-50`). API tokens stored as SHA-256 hashes (`middleware/auth.ts:48-55`). Personal tokens prefixed `pa_` so the middleware can branch cheaply.
- **Atomic SQL increments where it matters most.** `awardXp` uses `sql\`${userXp.totalXp} + ${xpGained}\`` inside an upsert (`routes/progress.ts:86-95`) rather than read-then-write. You know this pattern exists. You just don't apply it consistently (see §5.4).
- **Canonical pair ordering.** `[userA, userB].sort()` so a conversation between two users has one row (`routes/chat.ts:83`), backed by a unique index. Correct and elegant.
- **Cursor pagination** on messages by `sent_at` (`routes/chat.ts:131-141`) instead of OFFSET. You did it right where it mattered, and used OFFSET where it didn't (`routes/problems.ts:74`).
- **Client resilience.** Reconnect with capped exponential backoff and a 30 s heartbeat in all three WebSocket hooks. Debounce in the extension's service worker with a self-cleaning map (`extension/src/background.ts:26-36`).
- **Extension engineering.** Injecting into the page world to monkey-patch `fetch` and `XMLHttpRequest` while guarding every access so a bug never leaks into LeetCode's own error handlers (`extension/src/inject.ts`). This is a genuinely hard, unusual thing to have shipped.
- **Kcal is structurally better than PrepArena.** Global `onError` with a typed `AppError` (`kcalapp-backend/src/index.ts:21-30`), zod validation on meal bodies (`lib/validators.ts`), a clean state machine in `LogPage.tsx` (`capture → analyzing → result`), the React Compiler enabled. Kcal was written after PrepArena and it shows. That trajectory is a good sign.

## 3. Patterns you reach for by habit

| Habit | Where | Assessment |
|---|---|---|
| `Promise.all` over a list, each element doing its own queries | `routes/chat.ts:29-54`, `routes/leaderboard.ts:83-112`, `routes/friends.ts:220+` | This is the N+1 problem wearing a parallelism costume. Ten friends = 40 queries. You reach for it because it *looks* fast. |
| `await c.req.json<{...}>()` with a type assertion and no validation | Every PrepArena route | The type is a lie the compiler believes. `opponent_id` can be `undefined`, `problem_index` can be `"3"`. |
| JSON stringified into a `text` column | `problem_ids`, `tags`, `payload`, `metadata`, `ingredients`, `workout_types` | Reasonable for opaque blobs, wrong for things you query (`JSON_EXTRACT` on `activity_log.payload` at `routes/challenges.ts:656` forces a full scan). |
| Status as free-text `'pending' \| 'active' \| 'completed'` with the enum in a comment | All schemas | No `CHECK` constraint, no TypeScript enum shared with the DB. A typo is a silent bug. |
| `try { ... } catch {}` around anything network-shaped | DO broadcasts, feed pushes, `endBattle` | Sometimes right (best-effort broadcast), sometimes wrong (battle results lost silently, §5.2). You don't distinguish. |
| Helper functions copy-pasted across route files | `weekStart`, `monthStart`, `getStreak`, `broadcastToUser` exist in 3–4 files each | And they are not identical: two definitions of "week" (§5.6). |
| Non-null assertions on untrusted input | `url.searchParams.get('user_id')!` (`BattleRoom.ts:37-38`) | Works because the Worker sets it. Still a habit interviewers dislike. |
| Comments that explain *intent* | Throughout | Genuinely good. Keep this. |

## 4. Works, but for reasons you probably can't articulate

These are the questions you will be asked about your own code. Each is a `04-defend-your-code.md` item.

1. **Why does BattleRoom not corrupt state when both players send `problem_solved` at the same millisecond?** Because a Durable Object is single-threaded and its input gate blocks new events while `ctx.storage.get/put` are in flight. You rely on that guarantee without naming it. But the same guarantee does *not* cover the `await fetch()` and `await env.DB.prepare()` calls in `ChatRoom.webSocketMessage` — other messages interleave there.
2. **Why does `serializeAttachment` exist and what happens to `this` fields when the DO hibernates?** Anything in memory is gone. You correctly kept state in `ctx.storage` and identity in the attachment. Can you say why the alternative (a `Map<WebSocket, userId>` field) breaks?
3. **Why does `awardXp` use `sql\`x + y\`` but `POST /api/meals` uses `existing.total_calories + body.calories`?** One is atomic in the database, one is a lost-update race. You wrote both.
4. **Why `idFromName(battleId)` rather than `newUniqueId()`?** Deterministic routing so any Worker can find the room. What is the cost? (Global uniqueness lookup on first access; and anyone who knows the name can address it, which is why the Worker must gate access.)
5. **Why SHA-256 for API tokens but PBKDF2 with 100k iterations for passwords?** Tokens are 122-bit random UUIDs, so brute force is infeasible and a fast hash is fine. Passwords are low-entropy, so the hash must be slow. If you can't say this, the PBKDF2 choice looks copied.
6. **Why does the OAuth flow put the JWT in the redirect URL?** Because the cookie domain `.animishchopade.in` is not sent to `workers.dev`. That is a correct diagnosis and a bad fix (§5.7).

## 5. Weaknesses, by category, with evidence

### 5.1 Concurrency and correctness in the Durable Object code

- **Any client can end the battle.** `webSocketMessage` treats `{type:'battle_complete'}` from either socket as authoritative (`BattleRoom.ts:127-129`). A losing player sends it from the console and the battle ends with the current score.
- **Any client can claim any solve.** `problem_solved` is honour-system (`BattleRoom.ts:107-126`). No submission is verified against LeetCode, the extension, or `user_progress`. The whole scoring system trusts the browser.
- **The 45-minute timer starts on first WebSocket connect, not on accept.** `setAlarm(Date.now() + BATTLE_DURATION_MS)` at `BattleRoom.ts:72` while `startedAt` is read from D1 at `:58`. If the opponent accepts at 10:00 and the challenger opens the page at 10:07, the alarm fires at 10:52 but elapsed-time tie-breaking is measured from 10:00. Two clocks, one battle.
- **Battle results are persisted by the DO calling its own Worker over the public internet** (`BattleRoom.ts:160-172`) with a shared secret header, wrapped in `try/catch {}`. The DO has `env.DB` already. If `WORKER_URL` is wrong, the fetch times out, or the Worker 500s, the DO says "completed" and D1 says "active" forever. No retry, no dead-letter, no log. The comment calls this "best-effort". Rating changes are not best-effort.
- **`/internal/battles/:id/complete` is not idempotent** (`routes/battles.ts:285-353`). Called twice (a retry, a duplicate alarm, a replay) it applies `rating + 35` twice. There is no `WHERE status = 'active'` guard on the update.
- **Five writes in `Promise.all`, no transaction** (`routes/battles.ts:308-341`). D1 has `db.batch()`. If write 3 fails, the battle is marked completed but ratings are half-applied.
- **Accept is a check-then-act race** (`routes/battles.ts:244-250`). Read status, then `UPDATE ... SET status='active'` with no `WHERE status='pending'`. Accept and decline can both succeed.
- **Problem selection favours the challenger.** `selectBattleProblems(db, challengerId)` draws from the *challenger's already-solved* problems (`routes/battles.ts:44-115`). The challenger has seen four of the five problems before. An interviewer will find this in two minutes; it is the first thing to fix and the best story about "what I got wrong in my own design".
- **ChatRoom writes to D1 synchronously in the message hot path** (`ChatRoom.ts:69-81`), two round trips per message before broadcast, and the input gate does not cover them, so `last_message_preview` can be set out of order by interleaved messages.
- **Reconnect loop after completion.** `useBattleWebSocket.ts:89-100` schedules `connect` on every close, including after `battle_result`. The DO responds with `status:'completed'` each time, so it is harmless but wasteful, and it shows the state machine wasn't drawn.

### 5.2 Error handling

- PrepArena has no global error handler. An unhandled throw in any route is a bare 500 with Hono's default body. Kcal has `app.onError` — copy it back.
- Errors that matter are swallowed: battle persistence (`BattleRoom.ts:173-175`), feed pushes, the extension's non-OK statuses ("silent fail (don't spam the user)", `background.ts:92`). Silence is a choice; it needs a log line at minimum.
- Kcal's retry (`services/gemini.ts:21-37`) retries `AI_SERVICE_ERROR`, which includes a 400 from Gemini for a malformed request. Retrying a 400 immediately, with no backoff, doubles cost and never succeeds.
- `INVALID_AI_RESPONSE` maps to HTTP 500 (`prompt.ts:77`). The upstream misbehaved; that is a 502.

### 5.3 Test coverage and CI

- **Zero test files in all three repos.** `kcalapp-backend/package.json` has `"test:api": "tsx tests/api.test.ts"` and the file is not committed.
- **No `.github/` in any repo.** No lint, typecheck, or test runs on push. `apps/api` has no lint script at all.
- Pure functions that beg for tests and have none: `determineWinner`, `pickWithVariety`, `getMondayWeekStart`/`weekStart`, `parseProviderResponse`, `recalculateDailySummary`, `getStreak`, `isAccepted` in the extension.

### 5.4 Data modelling, queries and indexes

- **No non-unique index in either database.** Check `apps/api/drizzle/0000_fast_komodo.sql` and `kcalapp-backend/migrations/0000_initial.sql`. Every one of these is a full table scan today:
  - `messages WHERE conversation_id = ? ORDER BY sent_at DESC` (needs `(conversation_id, sent_at)`)
  - `activity_log WHERE user_id = ? AND type = 'solved'` (needs `(user_id, type, created_at)`)
  - `revision_schedule WHERE user_id = ? AND due_date <= ? AND completed = 0`
  - `battles WHERE challenger_id = ? OR opponent_id = ?`
  - `problems WHERE leetcode_slug = ?` (hit on every extension call)
  - `meals WHERE user_id = ? AND date = ?`, `daily_summaries WHERE user_id = ? AND date = ?`
  - `meals WHERE image_key IS NOT NULL AND image_expires_at < ?` (daily cron)
- **Lost update.** `POST /api/meals` reads `daily_summaries`, adds in JavaScript, writes back (`routes/meals.ts:44-74`). Two concurrent logs lose one. `PATCH` and `DELETE` recalculate from scratch instead. Two strategies for the same invariant in one file.
- **Missing unique constraint** on `daily_summaries(user_id, date)`. The race above can also insert two summary rows.
- **`getStreak` loads every activity row into JavaScript** to compute a streak (`routes/leaderboard.ts:31-50`). For the friends leaderboard it does this once per friend. This is a window-function query.
- **N+1 everywhere it's easy to be lazy:** conversation list (`chat.ts:29-54`, 2 queries per conversation), friends leaderboard (`leaderboard.ts:83-112`, 4 queries per friend plus the streak scan), topic leaderboard, pending friend requests, `autoCreateWeeklyChallenge` (a `COUNT` per topic in a loop, `challenges.ts:663-672`).
- **`scheduleRevisions` is 10 sequential round trips per solve** (`progress.ts:43-70`): 5 × (select + insert). One `INSERT ... ON CONFLICT DO NOTHING` with a unique index on `(user_id, problem_id, due_date)` replaces it.
- **Two code paths for "solved".** `POST /progress/:id/solve` awards XP, schedules revisions, logs activity, updates the challenge. `POST /api/progress/complete` (the extension path, `routes/extension.ts`) does none of that. Solving via the extension silently earns nothing. Duplicate business logic in two routes is how this happens.
- **Spaced repetition is not spaced repetition.** Intervals are fixed at 1/3/7/15/30 days (`progress.ts:27`) regardless of the confidence the user just reported. Confidence is stored (`user_progress.confidence`) and never read by the scheduler. The resume says "spaced-repetition revision with per-problem confidence tracking". Make it true (SM-2 is 30 lines) or say "scheduled revision".
- **Time is handled three ways.** ISO strings (Kcal), Unix ms integers (PrepArena), and `'YYYY-MM-DD'` text. Kcal derives `date` from `toISOString()` (`meals.ts:20`, `useTodayLog.ts:6`), which is UTC. An Indian user logging breakfast at 08:00 IST on Monday writes it to Monday, fine, but at 02:00 IST it lands on *Sunday*. Users will notice.
- **Booleans as integers** with `=== 1` comparisons scattered through route code rather than a `{ mode: 'boolean' }` column (which you *did* use once, `health_profiles.smokes`).

### 5.5 Security

- **JWT in the redirect URL** (`routes/auth.ts:179`). It lands in browser history, `Referer` headers, Cloudflare logs, and any analytics script. 7-day token, HS256, no rotation.
- **JWT in `localStorage`** in both apps. Any XSS reads it. The `httpOnly` cookie you also set is the right primitive; it just needs the API on a subdomain of `animishchopade.in` so the browser sends it.
- **[VERIFY] The battle WebSocket has no credentials in production.** `useBattleWebSocket.ts:45` opens `${VITE_API_URL}/api/battles/${id}/ws` with no `?token=`, unlike the feed and chat hooks. `authMiddleware` then needs the cookie, and the cookie is scoped to `.animishchopade.in` while the API is on `workers.dev` (`apps/api/wrangler.toml:79`). Unless there is a custom domain on the API that isn't in the repo, this returns 401 and battles are broken in production. Test it this weekend.
- **`?token=` accepted on every route** (`middleware/auth.ts:20-21`), not just the WebSocket upgrade. Tokens in query strings get logged.
- **No request body validation in PrepArena.** `POST /battles/challenge` with `{}` → `opponentId` undefined → `eq(users.id, undefined)` → whatever Drizzle does with that. `problem_index: "2"` passes `typeof === 'number'`? No, but `problem_index: 1e308` does.
- **Kcal `verifyPassword` uses `===` on hex strings** (`crypto.ts:54`). Not constant-time. Interviewers ask; the answer is `crypto.subtle.timingSafeEqual` or comparing digests.
- **Register is check-then-insert** (`kcal auth.ts:35-57`). Concurrent duplicate registrations hit the unique index and return a raw 500 instead of 409.
- **Rate limiter is per-isolate** (`middleware/rateLimit.ts:7`). Cloudflare runs your Worker in many isolates across many data centres; each has its own `Map`. The real limit is roughly "20 per hour per isolate that happens to serve you", and it resets whenever the isolate is evicted. Correct implementations: a Durable Object per user, KV with a short TTL (approximate), or Cloudflare's Rate Limiting binding.
- **Orphaned R2 objects.** `/api/analyze` with `save_image=true` writes to R2 *before* the user confirms the meal (`routes/analyze.ts:43-57`). If they cancel, no `meals` row references the key, so the cron (`cron/cleanupImages.ts`), which queries `meals`, never deletes it. Storage leaks forever. R2 object lifecycle rules (`expire after 15 days`) fix this with zero code.
- **Gemini API key in the query string** (`providers/gemini.ts:32`). Documented by Google, still ends up in logs. Use the `x-goog-api-key` header.
- **PWA caches authenticated API responses** (`kcal-frontend/vite.config.ts:31-41`, `NetworkFirst` on `/api/meals`). On a shared device, after logout, the service-worker cache still holds the previous user's meals.

### 5.6 Things that are just bugs

- **Two definitions of "week" in one file.** `getMondayWeekStart` (Monday, UTC) and `weekStart` (Sunday, `setHours`, local) both live in `routes/challenges.ts:56-69`. Weekly XP resets Sunday; weekly challenges run Monday to Monday.
- **`webSocketClose` calls `ws.close()` on a socket that is already closing** (`BattleRoom.ts:132-134`, same in the other two DOs). Harmless, but it shows the handler's purpose was guessed.
- **`resolveUsername` is 11 sequential queries worst-case** (`routes/auth.ts:33-44`) and still not race-safe under the unique index.
- **AI abstraction bypassed.** `services/ai/index.ts` exports `getAIProvider`, used only by the health report. The meal-analysis route calls `analyzeWithGemini`, which does `new GeminiProvider(apiKey)` directly (`services/gemini.ts:15`). Switching `AI_PROVIDER=openai` changes the health report and not the feature the app is named after.
- **Model name drift.** The code says `gemini-2.5-flash-lite` (`providers/gemini.ts:21`, commit "model changed ti cheaper"). Your brief and resume say Gemini 2.0 Flash. Pick one; interviewers Google it.
- **`autoCreateWeeklyChallenge` runs `JSON_EXTRACT` on every activity row** to count solves per topic (`challenges.ts:646-659`). The `problems.topic` join already gives you the topic; the JSON filter is redundant *and* forces a scan.
- **Base64 via string concatenation** (`routes/analyze.ts:28-34`): a 10 MB image becomes a 10 M-iteration loop building a 13 MB string, inside a Worker with a 128 MB memory limit and CPU-time billing. The comment says "safe for any buffer size", which is true for stack depth and false for everything else.

### 5.7 Typing discipline

- TypeScript is used as documentation, not enforcement. `as GoogleUser`, `as Record<string, unknown>`, `c.req.json<T>()`, `!` on query params. Kcal's zod usage on `/api/meals` is the model; the other 90% of routes don't follow it.
- `type` fields on events are string unions in the frontend (`WSMessage` in `useBattleWebSocket.ts:17-21`) and untyped `data.type === '...'` string comparisons in the DOs. No shared event schema despite having a `packages/shared` workspace for exactly that.

### 5.8 Documentation and repo hygiene

- Both READMEs are install instructions. Neither says what the hard problem was, draws the architecture, or admits a limitation.
- `account_id`, D1 IDs, and KV IDs committed in `wrangler.toml`. Not secrets, but a reviewer notices.
- `.env.production` committed in the Kcal frontend (contains only the API URL; the habit is the issue).
- `[vars] OPENAI_API_KEY = ""` in Kcal's `wrangler.toml` — placeholder secrets as plaintext vars.

## 6. Provisional level from code alone (0–5)

These are what the code *shows*. The diagnostic will confirm or overturn them.

| Area | Level | Why |
|---|---|---|
| Building and shipping features | 4 | Three deployed products with real user flows. Not in question. |
| TypeScript / JavaScript fluency | 3 | Idiomatic, readable, async handled competently. Loses a point for treating types as comments and for no runtime validation. |
| React | 3 | Hooks used correctly, refs used to dodge stale closures, state machines where needed. Can't judge whether you can *explain* reconciliation or effect semantics from code alone. |
| Cloudflare / edge runtime | 4 | Uses the platform's hard features. Loses a point for not knowing the DO input/output gate model that makes them safe. |
| Data modelling and SQL | 2 | No indexes, JSON columns queried with `JSON_EXTRACT`, lost updates, N+1 as a default pattern, no transactions. This is the widest gap and the most examinable. |
| Concurrency and distributed reasoning | 2 | Non-idempotent handlers, check-then-act races, trust-the-client scoring, fire-and-forget persistence of results that matter. |
| Security | 2.5 | Good instincts on CSRF, ownership, hashing. Bad on token transport and storage, no input validation, non-global rate limiting. |
| Error handling and observability | 2 | Kcal is decent; PrepArena has none. Silent catches on important paths. No structured logs anywhere. |
| Testing | 0 | None. |
| DevOps / CI | 1 | `wrangler deploy`. No pipeline. |
| Java / Spring | — | Zero evidence in public code. The diagnostic carries all of this. |
| GenAI engineering | 2.5 | Working vision feature with a prompt that includes portion references and a clean provider interface. Loses for regex-stripping code fences instead of JSON mode, no evals, no prompt versioning, abstraction bypassed. |

## 7. How this reweights the curriculum

The brief's allocation put databases at 8% and system design at 8%. The code says databases are your weakest examinable skill and your projects are your strongest system-design material. Proposed changes, to be finalised after the diagnostic:

1. **Databases 8% → 12%.** Indexes, transactions, isolation, and N+1 are not abstract for you; every bug above is a concrete exercise on your own schema. Week 1 includes adding the missing indexes to PrepArena with `EXPLAIN QUERY PLAN` before/after. That is the "query optimisation I can talk about from memory" from §12A, and it costs an evening.
2. **Java/Spring stays at 25% but shifts earlier and heavier on JPA/Hibernate and transactions**, because §5.4 shows you have not internalised transactional thinking in any language yet, and `@Transactional` is where interviewers test it.
3. **DSA stays at 30%**, with a caveat raised in the summary message: 160 problems in ~65 hours is 24 minutes per problem including review. Expect to cut to 110–120 and keep the timed sets.
4. **System design (LLD) 8% → 10%**, taken from GenAI (7% → 5%), because the hardening work in §12A *is* LLD practice on your own code: idempotent handlers, a proper rate limiter, the DO state machine drawn out.
5. **Portfolio hardening priorities, in order of interview signal per hour:**
   1. Fix battle WebSocket auth if §5.5's [VERIFY] is confirmed. A broken headline feature is worse than no feature.
   2. Indexes + `EXPLAIN` on PrepArena (2 h).
   3. Tests on `determineWinner`, `pickWithVariety`, `parseProviderResponse`, `recalculateDailySummary` + GitHub Actions running them (4 h).
   4. Make `/internal/battles/:id/complete` idempotent and use `db.batch` (2 h).
   5. Route `/api/analyze` through `getAIProvider`, switch to Gemini JSON mode with a schema, delete the regex (2 h).
   6. Rate limiter on a Durable Object or the Rate Limiting binding (2 h).
   7. Fix `selectBattleProblems` fairness (1 h) and write it up as your "mistake in my own design" story.
   8. READMEs for hiring managers (3 h).

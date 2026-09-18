# Part 04 — Defend your own code (90 minutes, 15 per item)

This is the interview moment you said you fear most: the interviewer has your GitHub open and asks "why?" until you run out of answers. So that is what this is.

**Do this out loud, then write.** Open the cited file, read it cold (you wrote it months ago; that is the point), and answer each question the way you would to a person across a table. Then write the answers in `answers/04-defend.md`. Mark any question where you had to guess with `[GUESS]`. "I don't know, but here's how I'd find out" is a legitimate answer and scores higher than a confident wrong one.

Do **not** read `CODE-AUDIT.md` before this part.

---

## Item 1 — `BattleRoom` Durable Object

File: `PrepArena/apps/api/src/durable/BattleRoom.ts`

1. Explain, in your own words, what a Durable Object *is* and why you chose one over a plain Worker plus D1 for battle state.
2. Both players send `problem_solved` in the same millisecond. Walk through what happens inside `webSocketMessage` for both. Can the scores end up wrong? What guarantee, if any, prevents that, and where does that guarantee come from?
3. The class has no instance fields except `ctx` and `env`. Why? What would go wrong if you kept `state` in a class field and `Map<WebSocket, string>` for user IDs?
4. What does `serializeAttachment` do, and what problem does it solve that a plain JavaScript object wouldn't?
5. A player closes the tab and reopens it 10 minutes later. Trace what they receive and why. What if the battle ended while they were away?
6. What happens if a player sends `{"type":"battle_complete"}` from the browser console while losing?
7. What happens if a player sends `{"type":"problem_solved","problem_index":0}` five times, and then for a problem they never opened?
8. **At 10,000 concurrent battles:** what is the bottleneck? Where does each battle's DO physically run? What happens when two players are on different continents?

## Item 2 — The alarm-based 45-minute timer

Same file, `setAlarm` at the first connection and `alarm()`.

1. Why an alarm instead of `setTimeout(…, 45 * 60 * 1000)` inside the DO?
2. When exactly does the 45 minutes start? Is that the same moment `startedAt` refers to? What if the opponent accepts at 10:00 and the challenger connects at 10:07?
3. The DO is evicted from memory at minute 20. Does the alarm still fire? What runs when it does, and what state does it have access to?
4. The alarm fires, `endBattle` runs, and the `fetch` to `/internal/battles/:id/complete` fails (timeout, 500, wrong `WORKER_URL`). What is the state of the battle in the DO? In D1? In each player's UI? How would anyone ever find out?
5. Why does the DO persist results by calling its own Worker over HTTPS with a secret header, when it already holds `env.DB`? What was the reasoning, and do you still agree with it?
6. `/internal/battles/:id/complete` gets called twice for the same battle (retry, replay, bug). What happens to each player's rating? Is the handler idempotent? What one line would make it so?
7. The five D1 writes in that handler run in `Promise.all`. The third one fails. Describe the resulting database state. What would you use instead?
8. **At scale:** 10,000 alarms fire within the same second on Monday at 00:00. What happens?

## Item 3 — The `AIProvider` factory

Files: `kcalapp-backend/src/services/ai/index.ts`, `services/ai/types.ts`, `services/ai/providers/gemini.ts`, `services/gemini.ts`, `routes/analyze.ts`

1. Name the design pattern(s) here. What problem does each solve? What is the difference between the *interface* and the *factory* in terms of what each buys you?
2. Your resume says providers can be swapped "with no route changes". Trace the code path from `POST /api/analyze` to the Gemini HTTP call. Does it go through `getAIProvider`? What does `AI_PROVIDER=openai` actually change in production today?
3. `MEAL_ANALYSIS_PROMPT` asks for raw JSON, and `parseProviderResponse` strips markdown fences with regex anyway. Why both? What does Gemini offer that would make the regex unnecessary, and what would you lose or gain?
4. Walk through `analyzeWithGemini`'s retry. Which errors retry, which don't, and why? What happens on a 400 from Gemini? On a 503? How much does a retry cost, and what backoff is used?
5. How would you know if the model started returning worse calorie estimates next week? What would an evaluation harness for this feature look like: inputs, expected outputs, metric, threshold?
6. Temperature 0.1, max 1024 output tokens. Why those numbers? What happens to a plate with 12 components?
7. A user uploads a photo of a receipt, a photo of a dog, and a 9.9 MB photo of a thali. Trace each through validation, base64 encoding, the prompt, and the response.
8. **At 10,000 users/day:** what is the cost driver, what is the latency budget, and where would you add caching or a cheaper first pass?

## Item 4 — PBKDF2 password hashing

File: `kcalapp-backend/src/lib/crypto.ts`, plus `routes/auth.ts` and `lib/jwt.ts`

1. Why PBKDF2 and not bcrypt, scrypt, or Argon2? Was that a choice or a constraint of the runtime? What does each of those four do differently?
2. Why 100,000 iterations? What does the iteration count trade off? How would you decide whether to raise it?
3. What is the salt for, why is it random per user, and why is it safe to store it next to the hash in plaintext?
4. `verifyPassword` compares two hex strings with `===`. What is the concern? Does it matter here? What is the correct primitive?
5. The API tokens in PrepArena are hashed with plain SHA-256, no salt, no iterations (`PrepArena/apps/api/src/middleware/auth.ts`). Why is that acceptable there but not for passwords?
6. A user changes their password. What happens to their existing 30-day JWT? Should it? How would you implement "log out everywhere"?
7. Register does "select existing, then insert". Two identical registration requests arrive together. What does the user see? What in the schema saves you, and what does the user see instead of a 409?
8. **At scale:** login is now 20% of your Worker CPU time. Why, and what are your options?

## Item 5 — The rate limiter

File: `kcalapp-backend/src/middleware/rateLimit.ts`

1. Explain the algorithm. Which of these is it: fixed window, sliding window, token bucket, leaky bucket? Draw the difference between fixed window and sliding window for a limit of 20/hour when a user sends 20 requests at 10:59 and 20 more at 11:01.
2. Where does `store` live? How many copies of it exist right now in production? What happens to it when Cloudflare recycles the isolate?
3. A user in Pune and the same user on a VPN in Frankfurt both hit `/api/analyze`. Do they share a limit?
4. Is there any scenario where this limiter blocks a user who has made fewer than 20 requests in the hour? Any scenario where it allows 200?
5. Design the correct version on Cloudflare. Give at least two options, their consistency guarantees, and their cost per request.
6. Now do the same limiter in a Spring Boot service running three instances behind a load balancer. Where does the state live? What does the atomic operation look like?
7. What should the 429 response include so a well-behaved client can back off correctly?
8. **At scale:** the limiter itself becomes the bottleneck. How?

## Item 6 — The Drizzle schemas

Files: `PrepArena/apps/api/src/db/schema.ts`, `PrepArena/apps/api/drizzle/0000_fast_komodo.sql`, `kcalapp-backend/src/db/schema.ts`, `kcalapp-backend/src/routes/meals.ts`

1. List every index that exists in the PrepArena database. Now list the five most frequent queries in the app. Which of them can use an index?
2. `GET /api/progress/revisions/today` on a user with 3,000 revision rows. Describe what SQLite does to answer it. What index would you add, with columns in which order, and why that order?
3. `problem_ids` is a JSON string in `battles` and `weekly_challenges`. What can you not do with it that you could with a `battle_problems(battle_id, problem_id, position)` table? When is the JSON column the *right* choice?
4. `POST /api/meals` in Kcal updates `daily_summaries` by reading the row, adding in JavaScript, and writing back. `PATCH` and `DELETE` recompute the row from `meals`. Why are they different? Which one is correct under concurrent requests, and what does the wrong one do?
5. Two meals logged simultaneously on a day with no summary row yet. How many `daily_summaries` rows exist afterwards? What constraint is missing?
6. `messages`, `activity_log`, and `solve_sessions` all have a `text` UUID primary key. What does that cost in SQLite compared to an integer rowid, and when does it matter?
7. What does `references(() => users.id)` actually enforce in D1 today? Does deleting a user work? What should happen to their messages?
8. **At scale:** `activity_log` reaches 50 million rows. Which queries break first, and what is the migration plan while the app stays online?

---

## Closing (10 minutes)

Three questions, honestly:

1. Which item did you find hardest to *explain* even though you remember *building* it?
2. Which decision in your code, on reflection, was wrong? Say what you would do instead.
3. Which question here would you least like to be asked in a real interview next week?

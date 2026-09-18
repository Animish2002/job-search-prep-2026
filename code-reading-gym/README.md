# Code-reading gym

One drill per day, 15 minutes, before anything else. Each drill is a 20–60 line sample you did not write, plus four questions:

1. What does it do?
2. What does it return / print for the given input?
3. Where is the bug or the edge case?
4. How would you refactor it?

Write your answers in the drill file under "Your answers" **before** reading the model answers. Time yourself. Log the time and a 0–4 score (one point per question) in the day's log. Roughly one drill a week is your own code from months ago; those are the ones that simulate "explain your project" on the spot.

Drills are generated seven at a time with the week's curriculum, as `NN-slug.md`.

## Themes for all 56

| # | Day | Theme | Language |
|---|---|---|---|
| 01 | Mon 09-21 | `Collectors.groupingBy` pipeline with a counting downstream | Java |
| 02 | Tue 09-22 | A `HashSet` that "loses" elements: `equals` without `hashCode` | Java |
| 03 | Wed 09-23 | Closure over a `var` loop variable with `setTimeout` | JS |
| 04 | Thu 09-24 | Removing from an `ArrayList` inside for-each | Java |
| 05 | Fri 09-25 | Array method chain over a sparse array with `map`/`filter`/holes | JS |
| 06 | Sat 09-26 | **Own code:** `apps/api/src/routes/progress.ts` `scheduleRevisions` | TS |
| 07 | Sun 09-27 | `String` interning, `==`, and the compile-time constant rule | Java |
| 08 | Mon 09-28 | Field `@Autowired` vs constructor injection in a unit test | Java/Spring |
| 09 | Tue 09-29 | `setTimeout` vs `.then` vs `await` ordering | JS |
| 10 | Wed 09-30 | Lazy collection touched outside a transaction | Java/JPA |
| 11 | Thu 10-01 | `@Transactional` self-invocation | Java/Spring |
| 12 | Fri 10-02 | `forEach` with an `async` callback vs `for...of` | JS |
| 13 | Sat 10-03 | **Own code:** `apps/api/src/durable/BattleRoom.ts` | TS |
| 14 | Sun 10-04 | A query plus its `EXPLAIN` output | SQL |
| 15 | Mon 10-05 | `submit` vs `execute` swallowing an exception | Java |
| 16 | Tue 10-06 | Double-checked locking without `volatile` | Java |
| 17 | Wed 10-07 | Event emitter that leaks listeners on reconnect | JS |
| 18 | Thu 10-08 | `CompletableFuture` chain: where the exception goes | Java |
| 19 | Fri 10-09 | A Mockito test that passes for the wrong reason | Java |
| 20 | Sat 10-10 | **Own code:** `apps/api/src/middleware/auth.ts` | TS |
| 21 | Sun 10-11 | Recursive tree walk mutating a shared list | Java |
| 22 | Mon 10-12 | Window-function query: what each row gets | SQL |
| 23 | Tue 10-13 | `PriorityQueue` with a broken `Comparator` | Java |
| 24 | Wed 10-14 | Strategy via enum with a subtle state bug | Java |
| 25 | Thu 10-15 | A Builder that leaks a mutable list | Java |
| 26 | Fri 10-16 | `reduce` building an object; accumulator identity | JS |
| 27 | Sat 10-17 | **Own code:** `apps/api/drizzle` schema | TS/SQL |
| 28 | Sun 10-18 | `JdbcTemplate` `RowMapper` off-by-one | Java |
| 29 | Mon 10-19 | `this` in a class method passed as a callback | JS |
| 30 | Tue 10-20 | Prototype chain: which method runs | JS |
| 31 | Wed 10-21 | `useEffect` with a stale closure | React |
| 32 | Thu 10-22 | Index keys on a list with delete | React |
| 33 | Fri 10-23 | Stream `pipe` without backpressure | Node |
| 34 | Sat 10-24 | **Own code:** `useBattleWebSocket.ts`; draw the state machine | TS |
| 35 | Sun 10-25 | Durable Object `fetch` handler with a race across an `await` | TS |
| 36 | Mon 10-26 | Singleton: enum vs holder vs synchronized | Java |
| 37 | Tue 10-27 | Decorator over `InputStream`: wrapper order | Java |
| 38 | Wed 10-28 | Retry with backoff that retries the wrong errors | Java |
| 39 | Thu 10-29 | Multi-stage Dockerfile: what is in the final image | Dockerfile |
| 40 | Fri 10-30 | GitHub Actions workflow: when the cache misses | YAML |
| 41 | Sat 10-31 | **Own code:** `kcalapp-backend/src/services/ai/index.ts` | TS |
| 42 | Sun 11-01 | Idempotency-key handler with a check-then-act gap | Java |
| 43 | Mon 11-02 | Cosine similarity with a normalisation bug | TS |
| 44 | Tue 11-03 | Chunking function with an off-by-one at boundaries | TS |
| 45 | Wed 11-04 | Record + sealed interface + pattern-matching switch | Java 21 |
| 46 | Thu 11-05 | Generator pipeline: what is consumed when | JS |
| 47 | Fri 11-06 | Virtual thread vs platform thread snippet | Java 21 |
| 48 | Sat 11-07 | **Own code:** `kcalapp-backend/src/cron/cleanupImages.ts` | TS |
| 49 | Sun 11-08 | `LinkedHashMap` LRU via `removeEldestEntry` (optional, Diwali) | Java |
| 50 | Mon 11-09 | `HashMap` resize: which bucket each key lands in | Java |
| 51 | Tue 11-10 | Full event-loop ordering quiz | JS |
| 52 | Wed 11-11 | `ConcurrentHashMap.compute` vs get-then-put | Java |
| 53 | Thu 11-12 | SQL script showing one isolation anomaly; name it | SQL |
| 54 | Fri 11-13 | **Own code:** `extension/src/inject.ts`, cold read | TS |
| 55 | Sat 11-14 | Spring Security filter: order, and what a bad token does | Java/Spring |
| 56 | Sun 11-15 | Mixed interview-style snippet | Java + JS |

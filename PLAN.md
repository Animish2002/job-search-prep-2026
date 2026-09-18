# PLAN.md — eight weeks, 2026-09-21 to 2026-11-15

Written 2026-09-19. Day 1 is **Monday 2026-09-21**. If you start later, run `/replan` and every date shifts; nothing else changes.

## 0. Read this first

**What this plan is calibrated on.** You said you are starting from the beginning. So the plan assumes you are rusty on fundamentals (big-O, recursion, memory model, indexing) and starts each track at its floor, and it takes its weighting from `diagnostic/CODE-AUDIT.md` §6, which is the only measured signal that exists yet: data modelling 2, concurrency 2, testing 0, CI 1, Java/Spring unmeasured.

**The diagnostic still runs this weekend (Sat 19 – Sun 20 Sept, 5.5 h).** It does not block the plan. It changes week 2 onward: after grading, `diagnostic/RESULTS.md` gets written and `/replan` re-cuts weeks 2–8. Week 1 is the same either way, because week 1 is foundations you need regardless.

**The two things that decide your outcome** are DSA and Java/Spring depth. Everything else is arranged around them. The JPA/Hibernate bullet on your resume is a landmine until week 2 ends; the plan defuses it in week 2 because applications start in week 2.

## 1. Your day

Constraints: office 11:00–20:00, gym in the morning, Pune commute. That gives two study windows, not one. The plan is built on both. Neither is optional on a Mon–Thu.

### Weekday template (Mon–Thu, 3 h 15 min)

| Time | Block | What |
|---|---|---|
| 06:30 | Wake | |
| ~07:00–08:15 | Gym | Not touched. |
| **08:30–08:45** | **Code-reading gym** | One drill from `code-reading-gym/`. 15 min hard stop. Never skipped. |
| **08:45–09:30** | **DSA** | Due re-solves first (max 2, 10 min each), then today's new problem(s). |
| **09:30–09:40** | **Flashcards** | `/review`. |
| 09:40–10:00 | Buffer | Finish the DSA write-up, or read the evening module's README so the evening starts warm. |
| 10:00–11:00 | Commute / office | |
| 11:00–20:00 | Office | |
| 20:00–21:15 | Home, dinner | |
| **21:15–22:30** | **Module** | The day's curriculum module: theory, source reading, build-it. |
| **22:30–22:55** | **Exercises / portfolio** | The module's `exercises/` or the scheduled portfolio task. |
| **22:55–23:00** | **Log** | `progress/log/YYYY-MM-DD.md`. Three lines minimum: done, not done, one thing that confused you. |
| 23:30 | Sleep | 7 h. Non-negotiable; week 7 needs you functional. |

If the gym runs late and the morning block is under 60 min: keep the code-reading drill and flashcards in the morning and move DSA to 21:15, pushing the module later. Never drop DSA to fit the morning.

### Friday (1 h 30 min, evening off)

Morning block only: code-reading drill, DSA, flashcards. Evening is the weekly rest. This is the rest day the brief asked for, placed where you are most likely to actually take it.

### Saturday (6 h)

| Time | Block |
|---|---|
| 09:00–09:15 | Code-reading drill |
| 09:15–10:00 | **Timed set:** 2 unseen problems, 45 min, no hints. Graded honestly in the log. |
| 10:00–10:15 | Flashcards |
| 10:15–12:30 | Module / deep-dive block A |
| 12:30–15:00 | Break |
| 15:00–17:30 | Portfolio block B (hardening, Spring project, or GenAI) |
| 17:30–18:15 | Applications (from week 2): 10 sent, tracker updated |

### Sunday (5 h 30 min, evening off)

| Time | Block |
|---|---|
| 09:00–09:15 | Code-reading drill |
| 09:15–10:15 | DSA: due re-solves + one new |
| 10:15–11:45 | **Mock interview** (from week 3) or walkthrough rehearsal |
| 11:45–12:30 | Mock feedback written to `interview/mocks/` |
| 12:30–15:00 | Break |
| 15:00–16:30 | **Week review:** quiz on the week, scored, lagging items named, next week adjusted |
| 16:30–17:30 | Career task of the week (stories, LinkedIn, hard-question answers) |
| Evening | Off |

### Hour budget

| | Per week |
|---|---|
| Mon–Thu 4 × 3.25 h | 13.0 h |
| Fri | 1.5 h |
| Sat | 6.0 h |
| Sun | 5.5 h |
| **Total** | **26 h** |

26 h × 8 = 208 h. Minus the 10% the brief says you will lose to life ≈ **187 h**. The plan below is sized to ~190 h, not the brief's 215. That is why the problem count is 110–120 rather than 160 and why GenAI is one week, not a track.

## 2. Effort allocation (final)

The provisional table in `CLAUDE.md` summed to 104%. Fixed here: JS/React/Node 12 → 10 (the audit rates your React at 3; you need reasoning, not teaching), system design 10 → 8 (most of it is done through hardening your own code, which also counts under DB and DevOps).

| Track | Share | Hours (of ~190) | Where it lives |
|---|---|---|---|
| DSA | 30% | 57 | Every morning; Saturday timed set |
| Java core + Spring Boot | 25% | 47 | Weeks 1–3 evenings, week 4/6 Spring project, week 8 Java 9–21 |
| SQL / DB internals | 12% | 23 | Week 1 Sat, week 2 Sat, week 4 Mon–Tue, Spring project schema |
| JS / React / Node / Workers | 10% | 19 | Week 5 |
| System design (LLD-heavy) | 8% | 15 | Week 4 Wed–Thu, week 6 Mon–Wed, mocks 4 and 6 |
| DevOps / SDLC | 5% | 9.5 | Week 3 Sat (CI), week 6 Thu (Docker/K8s), week 7 Sat (git, Agile) |
| GenAI | 5% | 9.5 | Week 7 |
| Career / behavioural / mocks | 5% | 9.5 | Week 1 resume + LinkedIn, Sat applications, Sun mocks |

Portfolio work is inside these rows, not extra: PrepArena/Kcal hardening ≈ 15 h (DB, SD, DevOps, JS), the Spring project ≈ 12 h (Java/Spring, DB, DevOps), READMEs and walkthroughs ≈ 5 h (Career).

## 3. The eight weeks at a glance

| Wk | Dates | DSA patterns | Evening modules | Weekend portfolio | Career | Mock |
|---|---|---|---|---|---|---|
| 1 | 21–27 Sep | Arrays/hashing, two pointers, sliding window | Java memory & identity, HashMap internals, LinkedHashMap/LRU, ArrayList/generics | Indexes + `EXPLAIN` on PrepArena D1 | Resume edit + 3 variants, LinkedIn | — |
| 2 | 28 Sep – 4 Oct | Stack, prefix sum, binary search, linked lists | Spring IoC + DI container, JPA persistence context, N+1, `@Transactional`; streams/exceptions | Lost-update fix in Kcal; Spring project scoped | Target companies, tracker, **first 10 applications**, hard-question answers | — |
| 3 | 5–11 Oct | Trees, intervals | Threads/executors/thread pool, JMM/CHM, Spring testing, Spring Security JWT | PrepArena tests + GitHub Actions; idempotent battle completion | 4 core STAR stories | 1: DSA |
| 4 | 12–18 Oct | Heaps/top-K, backtracking, tries | Joins/EXPLAIN deep, hard SQL, SOLID + patterns on your code, rate-limiter LLD | Spring project session 1 | Applications | 2: Java/Spring |
| 5 | 19–25 Oct | Graphs, union-find, greedy | JS event loop/closures/prototypes, mini Promise, React internals + component API design, Next.js, Node/Workers/Durable Objects | BattleRoom concurrency fixes, validation, `onError`; mini router | PrepArena 4-min walkthrough | 3: Full-stack |
| 6 | 26 Oct – 1 Nov | 1D DP, knapsack | HLD fundamentals, redesign PrepArena battles, webhook idempotency, feed; Docker/K8s | Spring project session 2 (security, CI, Docker); mini connection pool | Applications | 4: LLD |
| 7 | 2–8 Nov | 2D DP, bits, mixed | Embeddings + vector store, RAG, structured output, agent loop, MCP | Kcal AI fixes; ship RAG feature into PrepArena; git workflows | All STAR stories, 90-s versions | 5: Behavioural |
| 8 | 9–15 Nov | Revision only, daily timed sets | Java 9–21, gaps from mocks, walkthroughs ×4 | READMEs for hiring managers | Negotiation guide, weeks 9–12 plan | 6: Full loop |

Applications: 10 per week from Saturday 2026-10-03, Tier 3 first. Rejections in weeks 3–5 are data.

## 4. Standing rules

1. **Code-reading drill first, every day, 15 minutes.** Even on Friday, even on a mock day.
2. **DSA hint protocol:** nudge → bigger nudge → approach without code → code. Ask `/stuck <problem>` with what you tried.
3. **Spaced repetition:** each solved problem is re-solved from scratch at +1, +3, +7, +21 days. Queue in `dsa/revision/queue.md`. Two clean re-solves graduate it. Re-solves come before new problems.
4. **Core vs stretch.** Problems marked † are stretch. Solve them only when the core list and the revision queue are both clear that day. Core = 112 new + 22 timed-set, stretch = 14 (`dsa/problem-list.md`). When a day lists three and the re-solve queue is heavy, drop the third to Saturday's block A.
5. **Timed set every Saturday.** Two unseen problems, 45 min, no hints, scored 0/1/2 each in the log.
6. **Week review every Sunday.** Quiz, honest scores, what slipped, next week adjusted in this file under the week's heading.
7. **Applications from Sat 2026-10-03, 10 per week**, logged in `career/application-tracker.md`.
8. **Build-it exercises are not optional.** They are your interview stories: MiniHashMap (D3), LRU (D3), MiniArrayList (D4), DI container (D9), thread pool (D16), mini Promise (D30), mini router (D34), connection pool (D41), vector store (D43).
9. If you go quiet, come back and type `/replan`. No catching up on missed days; the plan re-cuts.

## 5. Day by day

Format per day: **AM** = 08:30–10:00 block (drill, DSA, flashcards). **PM** = 21:15–23:00 block (module, exercise, log). **Done when** = what must exist in the repo at 23:00. `Gym NN` refers to `code-reading-gym/` drill NN.

---

### Week 0 — Sat 2026-09-19 and Sun 2026-09-20: Diagnostic

- Sat: `diagnostic/01`, `02`, `03` (3 h 40 min).
- Sun: `diagnostic/04`, `05` (1 h 50 min). Then say "diagnostic done".
- Also: drop the resume PDF and source into `career/resume/`.
- Also: confirm whether the battle WebSocket works in production (CODE-AUDIT §5.5 `[VERIFY]`). Open a battle on the live site with the console open. If it 401s, that becomes Day 33's first task.

---

### Week 1 — Foundations, and make the resume true (21–27 Sep)

**Goal:** by Sunday you can explain, out loud, what `new HashMap<>().put(k, v)` does from the hash spread to the bucket, and your resume no longer claims anything the code contradicts.

Module folders this week: `curriculum/01-java-core/01-memory-and-object-identity`, `02-hashmap-internals`, `03-linkedhashmap-treemap-lru`, `04-arraylist-generics-erasure`, `curriculum/03-databases-sql/01-btree-indexes-explain`.

#### Day 1 — Mon 2026-09-21
- **AM:** Gym 01 (Java `Collectors.groupingBy` pipeline). DSA, arrays/hashing: **Two Sum**, **Contains Duplicate**, **Valid Anagram**. Before coding each, write its time and space complexity and why. Flashcards: none due; instead write 5 cards from the audit's "defend your code" list.
- **PM:** Java 01, memory and identity: stack frames vs heap, what `new` allocates, object header and references, `==` vs `equals`, `Integer` cache (−128..127), String pool and `intern()`, immutability and why `String` is final. Ten predict-the-output questions in `exercises/`. Quiz graded in the log.
- **Done when:** 3 problem files in `dsa/problems/arrays-hashing/`, quiz score in `progress/log/2026-09-21.md`.

#### Day 2 — Tue 2026-09-22
- **AM:** Gym 02 (a `HashSet` that "loses" elements: broken `equals`/`hashCode`). DSA: re-solve Day 1's three problems from scratch (+1 day; 5 min each, they should be fast), then **Group Anagrams**, **Top K Frequent Elements** (hash counting only today; the heap version returns in week 4).
- **PM:** Java 02, `HashMap` source walkthrough (JDK 8 `HashMap.java`): `table`, `Node<K,V>`, `hash()` spreading (`h ^ (h >>> 16)`), index `(n-1) & hash`, `putVal`, collision chaining, `TREEIFY_THRESHOLD = 8`, `UNTREEIFY_THRESHOLD = 6`, `MIN_TREEIFY_CAPACITY = 64`, `DEFAULT_LOAD_FACTOR = 0.75f`, `resize()` and the lo/hi split. The `hashCode`/`equals` contract and what breaks if you violate it. Start `build-it/MiniHashMap.java` (put/get/remove, chaining).
- **Done when:** you can draw the bucket array for 6 specific keys on paper; `MiniHashMap` compiles with put/get.

#### Day 3 — Wed 2026-09-23
- **AM:** Gym 03 (JS closure over a `var` loop variable with `setTimeout`). DSA: re-solves due per `dsa/revision/queue.md` (Day 2's two problems), then two pointers: **Valid Palindrome**, **Two Sum II**, **3Sum**. From here on the queue file is the source of truth for re-solves; the day blocks only list new problems.
- **PM:** Finish `MiniHashMap`: load factor, `resize()`, the test suite in `build-it/` must pass (collisions forced with a constant `hashCode`, resize at 0.75, 10k inserts). Then Java 03: `LinkedHashMap` (the `before/after` links, `accessOrder`, `removeEldestEntry`) and `TreeMap` (red-black, `O(log n)`, when to use). Build **LRU cache** from scratch: `HashMap` + doubly linked list, `get`/`put` O(1), tests.
- **Done when:** both test suites green; LRU also stored under `dsa/problems/design/lru-cache.md` (it is LeetCode 146).

#### Day 4 — Thu 2026-09-24
- **AM:** Gym 04 (`ArrayList` remove-inside-for-each: `ConcurrentModificationException`). DSA: **Container With Most Water**, **Trapping Rain Water**†. Due re-solves from the queue.
- **PM:** Java 04: `ArrayList` source (`elementData`, `DEFAULT_CAPACITY = 10`, `grow()` = old + old>>1, `modCount`, why fail-fast iterators exist), `ArrayList` vs `LinkedList` honestly (cache lines, when `LinkedList` wins: almost never), generics and type erasure (why `List<String>` and `List<Integer>` are one class at runtime, bridge methods, `? extends` vs `? super`). Build `MiniArrayList` with growth + tests.
- **Done when:** `MiniArrayList` tests green; one flashcard each for grow factor, erasure, fail-fast.

#### Day 5 — Fri 2026-09-25 (morning only)
- **AM:** Gym 05 (JS array method chain on a sparse array). DSA, sliding window: **Best Time to Buy and Sell Stock**, **Longest Substring Without Repeating Characters** (you saw it in the diagnostic; solve it clean now). Flashcards.
- **PM:** Rest.

#### Day 6 — Sat 2026-09-26
- 09:00 Gym 06 (own code: `apps/api/src/routes/progress.ts` `scheduleRevisions`; what does it do, how many queries, what breaks).
- 09:15 **Timed set 1:** Move Zeroes + Longest Subarray of 1's After Deleting One Element. 45 min.
- 10:15 **Block A, DB 01:** B-tree pages and why a lookup is `O(log n)` page reads, clustered vs secondary index (InnoDB) vs SQLite's rowid tables, composite indexes and the left-prefix rule, covering indexes, when an index is ignored (function on column, leading wildcard, low selectivity). Read `EXPLAIN QUERY PLAN` output for SQLite/D1 and `EXPLAIN` for MySQL.
- 15:00 **Block B, portfolio:** add the missing indexes from CODE-AUDIT §5.4 to PrepArena (`messages(conversation_id, sent_at)`, `activity_log(user_id, type, created_at)`, `revision_schedule(user_id, due_date, completed)`, `problems(leetcode_slug)`, battles by challenger/opponent) and Kcal (`meals(user_id, date)`, `daily_summaries(user_id, date)` unique). Record `EXPLAIN QUERY PLAN` before and after for three queries in `projects/hardening/01-indexes-explain.md`. Migration committed.
- 17:30 **Resume edit** (2 h, runs into the evening): follow `career/resume/README.md`. Output: edited master + `variant-java-backend.md`.
- **Done when:** the indexes are deployed, the before/after file exists, the Java-backend variant is ready to send.

#### Day 7 — Sun 2026-09-27
- 09:00 Gym 07 (Java `String` interning and `==` quiz).
- 09:15 DSA: due re-solves; new: **Longest Repeating Character Replacement**, **Permutation in String**. **Minimum Window Substring**† if clear.
- 10:15 **LinkedIn rewrite:** headline ("Java/Spring Boot + React full-stack engineer · Cloudflare Workers · granted patent"), About (patent in sentence one, Qnopy platform work, PrepArena), experience bullets mirrored from the resume, skills reordered Java-first. Make animishchopade.in lead with PrepArena. Full-stack and AI variants of the resume (45 min).
- 15:00 **Week 1 review:** `/quiz java-core` (memory, HashMap, ArrayList, generics) + `/quiz db-indexes`. Scores in `progress/log/2026-09-27-week-review.md`. Anything under 3/5 is re-taught Monday night before the new module.
- 16:30 Write the first draft answer to "Explain lazy loading and the N+1 problem" **without studying it** and save it. You will rewrite it on Day 11 and the diff is the point.
- **Week 1 exit criteria:** 17 core problems solved, MiniHashMap/LRU/MiniArrayList green, indexes shipped with numbers, resume + LinkedIn done.

---

### Week 2 — Spring internals and the JPA landmine; applications begin (28 Sep – 4 Oct)

**Goal:** the resume bullet "Spring Data JPA / Hibernate" survives a ten-minute interrogation. First 10 applications sent.

Modules: `02-spring-boot/01-ioc-bean-lifecycle-di`, `02-jpa-hibernate-persistence-context`, `03-n-plus-one-and-transactional`, `01-java-core/05-streams-optional-exceptions`, `03-databases-sql/02-transactions-isolation-locking`.

Note: Fri 2 Oct is Gandhi Jayanti. If the office is closed, run the Saturday template on Friday (timed set, block A, block B) and use Saturday's block B for Spring project session 0. Keep Friday evening off regardless.

#### Day 8 — Mon 2026-09-28
- **AM:** Gym 08 (Spring: field `@Autowired` vs constructor injection snippet, what happens in a unit test). DSA, stack: **Valid Parentheses** (diagnostic re-solve), **Min Stack**, **Evaluate Reverse Polish Notation**.
- **PM:** Spring 01: what `SpringApplication.run` does, `BeanDefinition` → instantiate → populate → `Aware` callbacks → `BeanPostProcessor` before-init → `@PostConstruct`/`InitializingBean` → after-init (this is where AOP proxies are created) → ready → `@PreDestroy`. The four injection routes (constructor, setter, field, method) and why constructor wins. Scopes (singleton, prototype, request) and the prototype-in-singleton trap. Exercises: order-of-lifecycle-log question, circular dependency question.
- **Done when:** you can list the lifecycle from memory in order, in under a minute, into the log.

#### Day 9 — Tue 2026-09-29
- **AM:** Gym 09 (JS Promise ordering: `setTimeout` vs `.then` vs `await`). DSA: **Daily Temperatures**, **Car Fleet**, **Largest Rectangle in Histogram**†.
- **PM:** Build **mini DI container** (`build-it/`): scan a package for `@Component`, constructor injection by type, singleton scope, circular-dependency detection with a clear error. Tests. This is the "I built a DI container to understand Spring" story.
- **Done when:** container tests green; one paragraph in `interview-qa.md` on what real Spring does that yours does not (BeanPostProcessors, proxies, lazy init).

#### Day 10 — Wed 2026-09-30
- **AM:** Gym 10 (JPA entity with a lazy collection touched outside a transaction). DSA, prefix sum + binary search: **Subarray Sum Equals K**, **Binary Search**, **Search a 2D Matrix**.
- **PM:** Spring 02, JPA/Hibernate: `EntityManager` and the persistence context (first-level cache), entity states (transient, managed, detached, removed), dirty checking at flush, flush modes and when SQL actually runs, `@Id` generation strategies and why `IDENTITY` disables batching, lazy vs eager, Hibernate proxies, `LazyInitializationException`, open-session-in-view and why it hides the problem. Second-level cache in one paragraph (what it is, why you probably have not needed it). Ground every item in a Qnopy-shaped example: a `Project` with `List<Sample>`.
- **Done when:** exercise set graded; rewrite the Day 7 lazy-loading answer, save both.

#### Day 11 — Thu 2026-10-01
- **AM:** Gym 11 (`@Transactional` self-invocation: which method actually runs in a transaction). DSA: **Koko Eating Bananas**, **Find Minimum in Rotated Sorted Array**, **Search in Rotated Sorted Array**.
- **PM:** Spring 03: the N+1 problem reproduced with SQL logging on, fixed three ways (`JOIN FETCH`, `@EntityGraph`, `@BatchSize`), and which to pick. `@Transactional`: the AOP proxy (JDK dynamic proxy vs CGLIB, why `final` methods and self-calls escape it), propagation (`REQUIRED`, `REQUIRES_NEW`, and when `NESTED` is a trap), `rollbackFor` and the checked-exception surprise, `readOnly`, where the transaction actually begins and commits in `TransactionInterceptor`. Map it back to CODE-AUDIT §5.1: five writes in `Promise.all` with no transaction is the same mistake in TypeScript.
- **Done when:** you can answer "explain lazy loading and N+1" in 90 s out loud, recorded; the recording is listened to once.

#### Day 12 — Fri 2026-10-02 (morning only; Gandhi Jayanti, see week note)
- **AM:** Gym 12 (JS `forEach` with `async` callback vs `for...of`). DSA, linked lists: **Reverse Linked List**, **Merge Two Sorted Lists**, **Linked List Cycle**.
- **PM:** Rest.

#### Day 13 — Sat 2026-10-03
- 09:00 Gym 13 (own code: `BattleRoom.ts`, cold read: what happens on `problem_solved`, what state lives where).
- 09:15 **Timed set 2:** Find Peak Element + Asteroid Collision.
- 10:15 **Block A:** Java 05 (streams are lazy pipelines: `Spliterator`, intermediate vs terminal, why `peek` misleads, `Optional` correctly, the exception hierarchy and when to make your own unchecked) 1 h. Then DB 02: ACID, isolation levels and the anomaly each permits (dirty read, non-repeatable read, phantom, lost update, write skew), InnoDB MVCC vs locking reads, `SELECT ... FOR UPDATE`, deadlocks and how InnoDB picks a victim. 1 h 15.
- 15:00 **Block B, portfolio:** reproduce the Kcal lost update on `daily_summaries` with two concurrent requests (a 20-line script), then fix it: atomic `UPDATE ... SET total = total + ?` plus the unique index from Day 6. Write it up in `projects/hardening/02-lost-update.md`. (1.5 h) Then **Spring project scoping** (1 h): read `projects/spring-service/README.md` (DocDrop), confirm the five entities, draw the schema.
- 17:30 **Career:** `career/target-companies.md` filled to 30 companies across tiers; **first 10 applications** (Tier 3), tracker updated.
- **Done when:** lost-update write-up, 10 rows in the tracker.

#### Day 14 — Sun 2026-10-04
- 09:00 Gym 14 (a SQL query plus its `EXPLAIN` output; say what it will do at 10× rows).
- 09:15 DSA: due re-solves; new: **Middle of the Linked List**, **Reorder List**, **Remove Nth Node From End**.
- 10:15 **Walkthrough draft:** the Qnopy design-system migration, 4 minutes, spoken, recorded, transcribed to `projects/walkthroughs/qnopy-design-system.md`. Structure: problem → decision (one configurable component vs per-module copies) → sequencing across four modules → what broke → what you'd change.
- 15:00 **Week 2 review:** `/quiz spring-ioc`, `/quiz jpa-hibernate`, `/quiz transactions`.
- 16:30 **Hard-question drafts** (`interview/hard-questions.md`): leaving under a year, 3.5 LPA, ETC → software, Aug 2024–Oct 2025, Angular → React, expected CTC. Honest, non-defensive, 60–90 s each. Interviews can start in week 3.
- **Week 2 exit criteria:** JPA/`@Transactional` quiz ≥ 4/5, DI container green, 10 applications out, hard questions drafted.

---

### Week 3 — Concurrency, testing, security; first mock (5–11 Oct)

**Goal:** you can explain what a thread pool does with a task, PrepArena has green CI, and you have sat one mock.

Modules: `01-java-core/06-threads-executors-completablefuture`, `07-jmm-synchronized-volatile-chm`, `02-spring-boot/04-testing`, `05-security-jwt`, `08-devops-sdlc/01-github-actions-and-git`.

#### Day 15 — Mon 2026-10-05
- **AM:** Gym 15 (`ExecutorService.submit` swallowing an exception vs `execute`). DSA, trees: **Invert Binary Tree**, **Maximum Depth**, **Diameter of Binary Tree**.
- **PM:** Java 06: `Thread` vs `Runnable` vs `Callable`, `ThreadPoolExecutor` internals (core size, max size, the queue, when a new thread is actually created, rejection policies, why `Executors.newFixedThreadPool` has an unbounded queue), `Future` vs `CompletableFuture` (`thenApply` vs `thenCompose`, `join`, exception propagation), what happens on `shutdown`. Map to the Node event loop you know: one loop vs many threads.
- **Done when:** exercise set graded; you can describe the path of one `submit()` call through the executor.

#### Day 16 — Tue 2026-10-06
- **AM:** Gym 16 (double-checked locking without `volatile`). DSA: **Balanced Binary Tree**, **Same Tree**, **Subtree of Another Tree**.
- **PM:** Build **mini thread pool** (`build-it/`): worker threads, a `BlockingQueue`, `submit` returning a `Future`, graceful shutdown. Tests. Then Java 07 part 1: the Java Memory Model in five sentences (happens-before, visibility, reordering), `synchronized` (monitor, reentrancy), `volatile` (visibility, not atomicity), `AtomicInteger` and CAS.
- **Done when:** thread pool tests green under 100 concurrent tasks.

#### Day 17 — Wed 2026-10-07
- **AM:** Gym 17 (JS event emitter that leaks listeners). DSA: **Lowest Common Ancestor of a BST**, **Binary Tree Level Order Traversal**, **Binary Tree Right Side View**.
- **PM:** Java 07 part 2: `ReentrantLock` vs `synchronized`, `ReadWriteLock`, `ConcurrentHashMap` in Java 8 (CAS on empty bin, `synchronized` on the bin head, no global lock, why `size()` is approximate, `computeIfAbsent` atomicity), `CopyOnWriteArrayList`, `BlockingQueue` families, deadlock demo and fix (lock ordering). Then Spring 04 part 1: the test pyramid for a Spring app.
- **Done when:** flashcards for JMM/CHM; deadlock demo runs and is fixed.

#### Day 18 — Thu 2026-10-08
- **AM:** Gym 18 (`CompletableFuture` chain: where does the exception go). DSA: **Count Good Nodes in Binary Tree**, **Validate Binary Search Tree**, **Kth Smallest Element in a BST**.
- **PM:** Spring 04: `@SpringBootTest` vs `@WebMvcTest` vs `@DataJpaTest` (what each loads), `MockMvc`, Mockito (`@MockBean` vs `@Mock`, verify, argument captors), Testcontainers for Postgres, why H2-for-tests lies to you. Spring 05: the Security filter chain (what `SecurityFilterChain` bean builds, `UsernamePasswordAuthenticationFilter`, `SecurityContextHolder` and its thread-local, a JWT `OncePerRequestFilter`, stateless sessions, refresh-token rotation, where to store tokens and why not `localStorage`; tie to CODE-AUDIT §5.5).
- **Done when:** exercise: write the JWT filter for DocDrop on paper, in order of operations.

#### Day 19 — Fri 2026-10-09 (morning only)
- **AM:** Gym 19 (a Mockito test that passes for the wrong reason). DSA, intervals: **Merge Intervals**, **Insert Interval**, **Non-overlapping Intervals**.

#### Day 20 — Sat 2026-10-10
- 09:00 Gym 20 (own code: `apps/api/src/middleware/auth.ts`).
- 09:15 **Timed set 3:** Symmetric Tree + Minimum Number of Arrows to Burst Balloons.
- 10:15 **Block A, DevOps 01:** GitHub Actions anatomy (workflow, job, step, matrix, cache), a workflow for a pnpm monorepo, branch protection. 45 min. Then DSA: **Construct Binary Tree from Preorder and Inorder**, **Meeting Rooms**, **Meeting Rooms II**.
- 15:00 **Block B, portfolio (4 h incl. after applications):** Vitest into `apps/api`; unit tests for `determineWinner`, `pickWithVariety`, `getMondayWeekStart` (and the Sunday `weekStart`, which exposes the bug), Kcal's `parseProviderResponse` and `recalculateDailySummary`. `.github/workflows/ci.yml` running lint, typecheck, tests on push for both repos. Then make `/internal/battles/:id/complete` idempotent (`WHERE status = 'active'`) and wrap its five writes in `db.batch`. Write `projects/hardening/03-tests-ci.md` and `04-idempotent-completion.md`.
- 17:30 Applications: 10.
- **Done when:** green check on both repos' main branch.

#### Day 21 — Sun 2026-10-11
- 09:00 Gym 21 (Java recursive tree walk mutating a shared list).
- 09:15 DSA: re-solves; new: **Binary Tree Maximum Path Sum**†, **Serialize and Deserialize Binary Tree**†.
- 10:15 **MOCK 1: DSA round** (`/mock dsa`, 60 min): one medium, one medium-hard, thinking aloud, interviewer interrupts. Feedback in `interview/mocks/2026-10-11-mock-1-dsa.md` with hire/no-hire and two fixes.
- 15:00 **Week 3 review:** `/quiz concurrency`, `/quiz spring-testing`, `/quiz spring-security`.
- 16:30 **STAR stories, batch 1** (`interview/behavioural/stories.md`): I interview you for the four core stories: Qnopy migration, shared component library (the case a module needed something the component couldn't do), PrepArena battle system, the patent.
- **Week 3 exit criteria:** thread pool green, CI green on two repos, mock 1 feedback written, four stories in STAR form.

---

### Week 4 — Databases deep, LLD, Spring project begins; mock 2 (12–18 Oct)

**Goal:** you can read an `EXPLAIN` plan and write a window function cold; DocDrop has entities, repositories, one JdbcTemplate path, and a Testcontainers test.

Modules: `03-databases-sql/03-joins-normalisation-explain-deep`, `04-hard-sql-windows-ctes`, `07-system-design/01-solid-and-patterns-on-your-code`, `02-lld-exercises/rate-limiter`.

#### Day 22 — Mon 2026-10-12
- **AM:** Gym 22 (a window-function query; what does each row get). DSA, heaps: **Kth Largest Element in a Stream**, **Last Stone Weight**, **K Closest Points to Origin**.
- **PM:** DB 03: how joins execute (nested loop, hash join, merge join; MySQL 8 has hash join, [VERIFY] since which minor), `EXPLAIN` columns in MySQL (`type`, `key`, `rows`, `Extra: Using filesort / Using temporary / Using index`) and Postgres (`Seq Scan`, `Index Scan`, `Bitmap Heap Scan`, cost vs actual with `EXPLAIN ANALYZE`), normalisation to 3NF with your PrepArena schema as the worked example, when to denormalise (your `daily_summaries` is a denormalisation; say why it exists).
- **Done when:** three `EXPLAIN` plans annotated in `exercises/`.

#### Day 23 — Tue 2026-10-13
- **AM:** Gym 23 (`PriorityQueue` with a broken `Comparator`). DSA: **Kth Largest Element in an Array** (quickselect), **Task Scheduler**, **Merge K Sorted Lists** (k-way merge).
- **PM:** DB 04, hard SQL: window functions (`ROW_NUMBER`, `RANK`, `DENSE_RANK`, `LAG`/`LEAD`, `SUM() OVER`), CTEs and recursive CTEs, self-joins, gaps-and-islands. Ten problems in `exercises/`; the tenth is `getStreak` from `leaderboard.ts` rewritten as one query.
- **Done when:** 8/10 SQL problems correct without hints.

#### Day 24 — Wed 2026-10-14
- **AM:** Gym 24 (Strategy pattern via enum with a subtle bug). DSA, backtracking: **Subsets**, **Combination Sum**, **Permutations**.
- **PM:** SD 01: SOLID with your code as the examples (SRP: `routes/battles.ts` does five jobs; OCP/DIP: `AIProvider`; LSP: a `ReadOnlyRepository` that throws). Patterns that actually appear: Strategy and Factory (name what `getAIProvider` is and what it is not), Builder (with immutability), Observer (your `UserFeed` broadcasts), Singleton done right (enum, holder idiom, and why DI made it mostly irrelevant), Adapter, Decorator (`java.io` streams). Java code for each in `exercises/`.
- **Done when:** you can say which pattern each of your own abstractions is, and one thing you'd change.

#### Day 25 — Thu 2026-10-15
- **AM:** Gym 25 (a Builder that leaks a mutable list). DSA: **Subsets II**, **Combination Sum II**, **Word Search**.
- **PM:** LLD exercise, **rate limiter**: token bucket, leaky bucket, fixed window, sliding window log, sliding window counter; class design, interface, tests in Java. Then contrast with Kcal's `Map`-per-isolate limiter: what it actually guarantees and what a Durable Object per user would guarantee.
- **Done when:** `RateLimiter` interface with two implementations and tests green.

#### Day 26 — Fri 2026-10-16 (morning only)
- **AM:** Gym 26 (JS `reduce` building an object; what's wrong with the accumulator). DSA, tries: **Implement Trie**, **Design Add and Search Words**.

#### Day 27 — Sat 2026-10-17
- 09:00 Gym 27 (own code: `apps/api/drizzle` schema; find three indexes you still lack and one type that should be a constraint).
- 09:15 **Timed set 4:** Top K Frequent Words + Generate Parentheses.
- 10:15 **Block A:** DSA: **Palindrome Partitioning**, **Letter Combinations of a Phone Number**, **Word Search II**†, **N-Queens**†. Then read `projects/spring-service/README.md` again and set up the repo skeleton (Spring Initializr, Postgres in docker-compose, Flyway).
- 15:00 **Block B, Spring project session 1 (2.5 h):** entities (`User`, `Centre`, `Document`, `PrintJob`, `ClaimToken`), Spring Data repositories, the `PrintJob` state machine with `@Version` optimistic locking, one `JdbcTemplate` reporting query (jobs per centre per day, window function), Flyway migration with real indexes, one `@DataJpaTest` on Testcontainers.
- 17:30 Applications: 10.
- **Done when:** `docker compose up` + tests green locally.

#### Day 28 — Sun 2026-10-18
- 09:00 Gym 28 (`JdbcTemplate` `RowMapper` with an off-by-one).
- 09:15 DSA: re-solves; new: **Find Median from Data Stream**†.
- 10:15 **MOCK 2: Java/Spring deep-dive** (`/mock java-spring`, 60 min): HashMap, thread pool, JPA persistence context, `@Transactional`, testing. Feedback written.
- 15:00 **Week 4 review:** `/quiz sql-hard`, `/quiz lld-patterns`.
- 16:30 Career: refresh the tracker, note any interview calls, adjust Tier targeting.
- **Week 4 exit criteria:** DocDrop runs with tests; rate limiter LLD done; mock 2 feedback; window functions cold.

Heads-up: Tue 2026-10-20 (Dussehra, [VERIFY] date) may be an office holiday. If so, use it as a bonus Saturday-template day for DocDrop.

---

### Week 5 — JavaScript, React, Node, Workers; mock 3 (19–25 Oct)

**Goal:** you can explain the code you already write in React and on Workers, and BattleRoom is correct under concurrency.

Modules: `04-javascript-deep/01-event-loop-closures-this-prototypes`, `02-promises-async-generators-modules`, `05-react-nextjs/01-reconciliation-hooks-effects-memo`, `02-component-api-design-and-rxjs-mapping`, `03-nextjs-rendering-hydration-cwv`, `06-node-backend/01-node-event-loop-streams-middleware`, `02-cloudflare-workers-and-durable-objects`.

#### Day 29 — Mon 2026-10-19
- **AM:** Gym 29 (`this` inside a class method passed as a callback). DSA, graphs: **Number of Islands**, **Clone Graph**, **Max Area of Island**.
- **PM:** JS 01: the event loop as it actually runs (call stack, macrotask queue, microtask queue drained fully between macrotasks, `requestAnimationFrame`, Node's phases in one paragraph), closures and the lexical environment, `this` binding rules (default, implicit, explicit, `new`, arrow), prototype chain and `Object.create`, hoisting and the temporal dead zone, coercion rules that appear in quizzes (`==` algorithm, `[] + {}`). Twenty predict-the-output questions.
- **Done when:** ≥ 16/20 on the output set.

#### Day 30 — Tue 2026-10-20 (possible holiday, see note)
- **AM:** Gym 30 (a prototype-chain snippet: which method runs). DSA: **Pacific Atlantic Water Flow**, **Rotting Oranges**, **Course Schedule** (diagnostic re-solve), **Course Schedule II**.
- **PM:** Build **mini Promise** (`build-it/`): states, `then` chaining with the resolution procedure, `catch`, `all`, `race`, microtask scheduling via `queueMicrotask`. Tests. Then `async`/`await` desugared to promises, generators and iterators, ESM vs CJS (live bindings, top-level await).
- **Done when:** mini Promise passes the ordering tests; you can say why `await` in a loop serialises.

#### Day 31 — Wed 2026-10-21
- **AM:** Gym 31 (React `useEffect` with a stale closure). DSA, union-find: **Redundant Connection**, **Number of Connected Components**, **Graph Valid Tree**.
- **PM:** React 01: fiber and reconciliation (why keys matter, what a key change actually does), the rules of hooks and why (the hooks array), `useEffect` dependency semantics and cleanup ordering, `useMemo`/`useCallback`/`memo` and when they cost more than they save, context and re-render scope, state options (local, lifted, Zustand, server state). React 02: component API design (compound components, controlled vs uncontrolled, render props vs children, headless patterns) told through your Qnopy table/date-picker/multi-select decisions; RxJS → React mapping (subject vs store, operators vs derived state, subscriptions vs effects); Angular DI/services vs context/hooks. Write and record the answer to "you've mainly done Angular, why React?".
- **Done when:** recorded answer under 90 s; component API notes in `interview-qa.md`.

#### Day 32 — Thu 2026-10-22
- **AM:** Gym 32 (a list rendered with index keys and a delete button). DSA: **Network Delay Time** (Dijkstra), **Min Cost to Connect All Points** (Prim), **Word Ladder**†.
- **PM:** React 03: SSR vs SSG vs ISR vs RSC in the App Router, hydration and hydration errors, Core Web Vitals and what moves them. Node 01: Node's event loop phases, streams and backpressure (`pipe` vs `pipeline`, `highWaterMark`), clustering and worker threads, middleware architecture and error handling (what Hono/Express do with a thrown error). Node 02: Workers runtime (V8 isolates, no Node APIs, CPU-time limits, cold starts), Durable Objects: the single-threaded actor, **input and output gates** (exactly which `await`s let other events interleave), storage consistency, alarms (at-least-once, retry), hibernation. Re-read `BattleRoom.ts` and `ChatRoom.ts` with that lens and list every `await` the gate does not cover.
- **Done when:** the list of unprotected awaits exists in `projects/hardening/05-do-concurrency.md`.

#### Day 33 — Fri 2026-10-23 (morning only)
- **AM:** Gym 33 (Node stream `pipe` without backpressure handling). DSA, greedy: **Maximum Subarray**, **Jump Game**, **Jump Game II**.

#### Day 34 — Sat 2026-10-24
- 09:00 Gym 34 (own code: `useBattleWebSocket.ts`; draw its state machine).
- 09:15 **Timed set 5:** Keys and Rooms + Is Graph Bipartite.
- 10:15 **Block A:** build **mini Express-style router** (`build-it/`): path params, middleware chaining with `next`, error middleware, 404. Tests. 1.5 h. DSA: **Gas Station**, **Hand of Straights**, **Partition Labels**.
- 15:00 **Block B, portfolio (2.5 h):** BattleRoom fixes from Day 32's list: (1) fix WebSocket auth if Day 0 found it broken; (2) timer starts on accept, one clock; (3) `battle_complete` only from the alarm or a verified condition; (4) verify `problem_solved` against `user_progress`/extension; (5) accept is `UPDATE ... WHERE status = 'pending'`; (6) `selectBattleProblems` draws from problems neither player has solved. Add `app.onError` and zod validation to the battle routes. Write `06-battleroom-fixes.md` including the fairness bug as your "mistake in my own design" story.
- 17:30 Applications: 10.
- **Done when:** fixes deployed, CI green, write-up done.

#### Day 35 — Sun 2026-10-25
- 09:00 Gym 35 (a Durable Object `fetch` handler with a race across an `await`).
- 09:15 DSA: re-solves; new: **Surrounded Regions**, **Cheapest Flights Within K Stops**†.
- 10:15 **MOCK 3: full-stack cross-examination** (`/mock fullstack`, 75 min): JS output questions, React re-render reasoning, then "walk me through PrepArena's architecture" with follow-ups on DOs. Feedback written.
- 15:00 **Week 5 review:** `/quiz js-deep`, `/quiz react`, `/quiz durable-objects`.
- 16:30 **PrepArena 4-minute walkthrough** with a diagram, recorded, transcribed to `projects/walkthroughs/preparena.md`. Kcal 2-minute version too.
- **Week 5 exit criteria:** mini Promise and router green, BattleRoom fixes shipped, walkthroughs recorded, mock 3 feedback.

---

### Week 6 — System design, DP, DevOps; mock 4 (26 Oct – 1 Nov)

**Goal:** DocDrop is complete with security, CI and Docker; you can redesign PrepArena's battle system on a whiteboard and say where the shipped version is wrong.

Modules: `07-system-design/03-hld-fundamentals`, `04-design-walkthroughs-from-your-projects`, `02-lld-exercises/{parking-lot,notification-service}`, `08-devops-sdlc/02-docker-compose-k8s`, `02-spring-boot/06-config-profiles-actuator-controlleradvice`, `03-databases-sql/05-connection-pooling-mysql-vs-postgres`.

#### Day 36 — Mon 2026-10-26
- **AM:** Gym 36 (Singleton: enum vs lazy holder vs synchronized). DSA, 1D DP: **Climbing Stairs**, **Min Cost Climbing Stairs**, **House Robber**. For each, write the recurrence in words before code.
- **PM:** SD 03, HLD fundamentals at conversation depth: load balancing (L4/L7, sticky sessions and why your WebSockets care), caching layers and invalidation, CAP and what it does not say, SQL vs NoSQL selection, message queues and at-least-once delivery, idempotency keys, rate limiting placement, CDNs. One paragraph each, one question each.
- **Done when:** flashcards for each; you can explain at-least-once vs exactly-once in 30 s.

#### Day 37 — Tue 2026-10-27
- **AM:** Gym 37 (Decorator over `InputStream`; what order do the wrappers run). DSA: **House Robber II**, **Longest Palindromic Substring**, **Palindromic Substrings**.
- **PM:** SD 04a: **design a real-time 1v1 coding-battle system** from requirements: matchmaking, room state, timers, scoring verification, persistence, reconnect, 10k concurrent battles. Then compare against what you shipped, item by item. Diagram saved.
- **Done when:** `design-battle-system.md` with diagram and the "shipped vs designed" table.

#### Day 38 — Wed 2026-10-28
- **AM:** Gym 38 (retry with exponential backoff that retries the wrong errors; compare Kcal's `gemini.ts`). DSA: **Decode Ways**, **Coin Change**, **Maximum Product Subarray**.
- **PM:** SD 04b: **payment webhook with idempotency** (Technical Spark and Razorpay: signature verification, idempotency key on the event id, out-of-order events, retries, reconciliation job). SD 04c: **notification/activity feed** (fan-out on write vs read, your `UserFeed` DO, what breaks with a user who has 50k followers). LLD: **notification service** class design (Strategy per channel, Observer, retry with backoff), Java skeleton.
- **Done when:** two design docs and the notification-service skeleton compiles.

#### Day 39 — Thu 2026-10-29
- **AM:** Gym 39 (read a multi-stage Dockerfile; what's in the final image). DSA, knapsack: **0/1 Knapsack** (GFG), **Partition Equal Subset Sum**, **Target Sum**.
- **PM:** DevOps 02: multi-stage Dockerfile for DocDrop (Maven build stage → JRE runtime, layered jar, non-root user) and for a Node/Hono service; `docker-compose` with Postgres and healthchecks; Kubernetes conceptually with a 30-minute hands-on in kind or minikube: pod, deployment, service, ingress, configmap, secret, liveness/readiness. Spring 06: profiles and `application-*.yml`, `@ConfigurationProperties`, actuator endpoints (`health`, `metrics`, `info`), `@ControllerAdvice` with a problem-details error body, Bean Validation.
- **Done when:** DocDrop image builds and runs in compose; `/actuator/health` answers.

#### Day 40 — Fri 2026-10-30 (morning only)
- **AM:** Gym 40 (read a GitHub Actions workflow; when does the cache miss). DSA: **Word Break**, **Longest Increasing Subsequence**.
- **Optional evening, 30 min, only if you feel like it:** implement SM-2 in PrepArena's `scheduleRevisions` so "confidence tracking" becomes true. Otherwise it is Day 48.

#### Day 41 — Sat 2026-10-31
- 09:00 Gym 41 (own code: `kcalapp-backend/src/services/ai/index.ts` factory; what the factory returns for each `AI_PROVIDER`, and where it is not used).
- 09:15 **Timed set 6:** Delete and Earn + Perfect Squares.
- 10:15 **Block A:** DB 05: connection pooling (HikariCP internals: pool size formula, `connectionTimeout`, leak detection, why a pool of 10 beats 100), MySQL vs Postgres differences that matter in interviews (MVCC implementation, clustered PK, `UPSERT` syntax, JSON, `EXPLAIN` format). Build **mini connection pool** (`build-it/`): bounded, blocking acquire with timeout, release, health check. Tests. DSA: **Coin Change II**, **Unbounded Knapsack** (GFG).
- 15:00 **Block B, Spring project session 2 (2.5 h):** Spring Security JWT with refresh-token rotation, `@ControllerAdvice`, validation, the claim flow as an idempotent state transition (`UPDATE ... WHERE status = 'PENDING'`), scheduled expiry job (`@Scheduled`), before/after `EXPLAIN` on the jobs-by-centre query recorded in the project README, GitHub Actions running tests with Testcontainers.
- 17:30 Applications: 10.
- **Done when:** DocDrop CI green on GitHub; README has the EXPLAIN numbers.

#### Day 42 — Sun 2026-11-01
- 09:00 Gym 42 (an idempotency-key handler with a TOCTOU gap).
- 09:15 DSA: re-solves; new: **Edit Distance** (early, because it is the canonical 2D DP).
- 10:15 **MOCK 4: LLD round** (`/mock lld`, 60 min): parking lot or a variant, then "now make it concurrent". Feedback written.
- 15:00 **Week 6 review:** `/quiz hld`, `/quiz dp-1d`, `/quiz devops`.
- 16:30 DocDrop 2-minute walkthrough recorded; `projects/walkthroughs/docdrop.md`.
- **Week 6 exit criteria:** DocDrop feature-complete with CI and Docker, three design docs, mock 4 feedback, connection pool green.

---

### Week 7 — GenAI, 2D DP, behavioural; mock 5 (2–8 Nov)

**Goal:** the Kcal resume claims are true; one RAG or agent feature is live in PrepArena; 8–10 STAR stories in 90-second form.

Modules: `09-genai-agents/01-embeddings-vector-store`, `02-rag-pipeline-and-evals`, `03-structured-output-tool-calling-agent-loop-mcp`, `08-devops-sdlc/03-git-workflows-and-agile`.

Note: Sun 2026-11-08 is Diwali (Lakshmi Puja) [VERIFY]. Mock 5 moves to Saturday evening; Sunday is a rest day. Recruiter activity drops Nov 6–11; front-load this week's applications to Monday–Wednesday evenings (10 min each night) rather than Saturday.

#### Day 43 — Mon 2026-11-02
- **AM:** Gym 43 (a cosine-similarity implementation with a normalisation bug). DSA, 2D DP: **Unique Paths**, **Longest Common Subsequence**.
- **PM:** GenAI 01: what an embedding vector represents, cosine vs dot product vs Euclidean, why dimensionality matters, ANN in one paragraph (HNSW as a graph, not a formula). Build **mini vector store** (`build-it/`, TypeScript): `upsert`, `topK` by cosine, brute force, then compare against pgvector/Qdrant's tradeoffs. Tests.
- **Done when:** vector store green; flashcards.

#### Day 44 — Tue 2026-11-03
- **AM:** Gym 44 (a chunking function with an off-by-one at boundaries). DSA: **Best Time to Buy and Sell Stock with Cooldown**, **Interleaving String**†.
- **PM:** GenAI 02: RAG end to end: chunking strategies (fixed, sentence, semantic, overlap), embedding, retrieval, reranking, context assembly, citation; retrieval evaluation (recall@k on a hand-labelled set of 20 questions); the failure modes (chunk boundary loss, lost-in-the-middle, stale index). Decide the PrepArena feature: retrieval over problem editorials/hints, or a weekly-plan agent from solve history. Design it in one page.
- **Done when:** design page + a labelled eval set of 20 Q/A pairs.

#### Day 45 — Wed 2026-11-04
- **AM:** Gym 45 (Java record + sealed interface + pattern-matching switch: what does it print). DSA, bits: **Single Number**, **Number of 1 Bits**, **Counting Bits**, **Reverse Bits**.
- **PM:** GenAI 03 part 1: structured output with a JSON schema (Gemini `responseSchema`), validation with zod, why it replaces retry-on-malformed; prompt versioning; evals as tests. **Portfolio:** route Kcal's `/api/analyze` through `getAIProvider`, switch to JSON mode with schema, delete the regex, fix retry to skip 4xx and add backoff, map `INVALID_AI_RESPONSE` to 502, move the Gemini key to a header. Write `projects/hardening/07-kcal-ai-layer.md`. Rate limiter onto a Durable Object or the Rate Limiting binding if time (else Day 48).
- **Done when:** Kcal deployed with the AI fixes; the resume's AI-layer bullet is now true.

#### Day 46 — Thu 2026-11-05
- **AM:** Gym 46 (a JS generator pipeline; what is consumed when). DSA: **Missing Number**, **Sum of Two Integers**, one mixed medium from the revision queue.
- **PM:** GenAI 03 part 2: tool/function calling, the agent loop written from scratch (plan → call tool → observe → repeat, with a step cap and a cost cap) before any framework; MCP in one page (what a server exposes, why it exists); production concerns (cost per call, latency budgets, token limits, hallucination mitigation, guardrails, logging prompts). Then **STAR stories, batch 2** (45 min): hardest bug, disagreement with a colleague, deadline, mistake that reached production, unblocking someone, why leaving.
- **Done when:** agent loop runs against one tool; six more stories drafted.

#### Day 47 — Fri 2026-11-06 (morning only)
- **AM:** Gym 47 (Java virtual thread snippet vs platform thread). DSA: revision queue only.

#### Day 48 — Sat 2026-11-07
- 09:00 Gym 48 (own code: `cron/cleanupImages.ts`; what it misses, per CODE-AUDIT §5.5).
- 09:15 **Timed set 7:** Minimum Path Sum + Longest Common Substring (GFG).
- 10:15 **Block A, DevOps 03:** git beyond the basics with a scratch repo: interactive-free rebase (`git rebase main`), `cherry-pick`, `bisect` on a planted bug, resolving a real conflict, `reflog` recovery. Agile vocabulary you'll be asked about (sprint, ceremonies, story points, DoD, velocity) framed from Qnopy. 1 h. Then: SM-2 into PrepArena if not done; per-user rate limiter if not done. 1 h.
- 15:00 **Block B, ship the GenAI feature (2.5 h):** the Day 44 design into PrepArena, behind a flag, with the eval set run once and numbers in the write-up (`projects/hardening/08-rag-feature.md`).
- 18:00 **MOCK 5: behavioural/HR** (`/mock behavioural`, 60 min): all eight hard questions plus four STAR probes with "why" ×3. Feedback written.
- **Done when:** feature live, mock 5 feedback.

#### Day 49 — Sun 2026-11-08 (Diwali)
- Rest. If you want 30 minutes: Gym 49 (Java `LinkedHashMap` LRU via `removeEldestEntry`) and the flashcards. Nothing else.
- **Week 7 exit criteria:** vector store green, Kcal AI fixes live, RAG feature live with eval numbers, 8–10 stories, mock 5 feedback.

---

### Week 8 — Consolidation and the full loop (9–15 Nov)

**Goal:** nothing new. Every weak item from the six mocks and eight week reviews gets re-taught and re-tested. Four walkthroughs fluent. READMEs rewritten. You leave the week interview-ready and with a plan for weeks 9–12.

Modules: `01-java-core/08-java-9-to-21`; otherwise gaps only.

#### Day 50 — Mon 2026-11-09
- **AM:** Gym 50 (`HashMap` resize: which bucket does each key land in). DSA: **timed set 8** in the morning slot (2 problems, 45 min) drawn from patterns you scored lowest on.
- **PM:** Java 08: what changed after 8 and how to say it: `var`, HTTP client, `Optional` additions (11); records, sealed types, pattern matching for `instanceof` and `switch`, text blocks (17); virtual threads and what they change about thread pools, sequenced collections (21). Exercises: rewrite three Java 8 snippets in 21 idiom. Then re-teach the lowest-scoring week-1/2 item.
- **Done when:** flashcards for versions; the re-taught item re-quizzed ≥ 4/5.

#### Day 51 — Tue 2026-11-10
- **AM:** Gym 51 (full JS event loop ordering quiz). DSA: revision queue + timed set 9.
- **PM:** Re-teach the lowest-scoring week-3/4 item (likely concurrency or `EXPLAIN`). Rehearse walkthrough 1 (PrepArena, 4 min) and 2 (Qnopy, 4 min) twice each, timed.
- **Done when:** both under 4:30 and without notes.

#### Day 52 — Wed 2026-11-11
- **AM:** Gym 52 (`ConcurrentHashMap.compute` vs get-then-put). DSA: revision queue + timed set 10.
- **PM:** Re-teach the lowest-scoring week-5/6 item. Rehearse walkthrough 3 (Kcal, 2 min) and 4 (DocDrop, 2 min). Hard questions out loud, all eight, recorded, listened to.
- **Done when:** recordings exist and you have written one correction per answer.

#### Day 53 — Thu 2026-11-12
- **AM:** Gym 53 (a SQL script that shows one isolation anomaly; name it). DSA: revision queue + timed set 11.
- **PM:** `interview/salary-negotiation.md` finalised: expected-CTC answer as a researched range, the "your current CTC is low" script, fixed vs variable vs ESOP, competing offers, benchmarks by tier marked `[VERIFY]` against AmbitionBox/Glassdoor/levels.fyi.
- **Done when:** you can state your range and its justification in 20 s.

#### Day 54 — Fri 2026-11-13 (morning only)
- **AM:** Gym 54 (own code: `extension/src/inject.ts`, cold read). DSA: revision queue.

#### Day 55 — Sat 2026-11-14
- 09:00 Gym 55 (a Spring Security filter snippet; what order, what happens on a bad token).
- 09:30 **MOCK 6: full loop** (`/mock full-loop`, ~3 h with breaks): DSA 45 min → Java/Spring 45 → LLD 45 → HR 30. Verdict per round, overall hire/no-hire, top three fixes.
- 15:00 **READMEs for hiring managers** (PrepArena, Kcal, DocDrop): problem, architecture diagram, three hardest decisions with tradeoffs, known limitations, what changes at 100×. 2.5 h.
- **Done when:** three READMEs pushed; mock 6 feedback.

#### Day 56 — Sun 2026-11-15
- 09:00 Gym 56 (mixed interview-style snippet).
- 09:15 DSA: revision queue, last pass.
- 10:15 `/progress` final: every track scored against week-1 baseline; `diagnostic/RESULTS.md` re-scored as `diagnostic/RESULTS-week-8.md`.
- 15:00 **Weeks 9–12 plan** written into this file: application cadence continues at 10/week, weekly timed set and one mock stay, per-interview prep via the "I have an interview at ..." prompt, revision queue until empty.
- **Week 8 exit criteria:** mock 6 verdict written, READMEs live, walkthroughs fluent, negotiation range fixed.

## 6. Milestones

| By end of | Must be true |
|---|---|
| Week 1 | MiniHashMap, LRU, MiniArrayList green. Indexes shipped with EXPLAIN numbers. Resume variants and LinkedIn done. 17 problems. |
| Week 2 | Can explain persistence context, lazy loading, N+1, `@Transactional` proxies aloud in 90 s. 10 applications sent. Hard questions drafted. |
| Week 3 | Thread pool green. CI green on PrepArena and Kcal. Mock 1 done. Four STAR stories. ~60 problems. |
| Week 4 | DocDrop runs with Testcontainers. Window functions cold. Rate limiter LLD. Mock 2. |
| Week 5 | Mini Promise and router green. BattleRoom correct and deployed. Walkthroughs recorded. Mock 3. ~100 problems. |
| Week 6 | DocDrop complete, Dockerised, CI. Three design docs. Mock 4. |
| Week 7 | Kcal AI claims true. RAG feature live with evals. 8–10 stories. Mock 5. ~115 problems. |
| Week 8 | Mock 6 verdict. READMEs. Negotiation range. Weeks 9–12 plan. |

## 7. After week 8

Interview-ready is not offered. Weeks 9–12: keep the Saturday timed set, one mock per week targeted at whatever loop is next, applications at 10/week until an offer is signed, and revision until the queue empties. Per interview, use the "I have an interview at <company>" prompt from the brief and the plan generates a targeted mock the evening before.

## 8. Known risks

- **The JPA bullet before week 2 ends.** Do not accept an interview before 2026-10-05.
- **Battle WebSocket possibly broken in production** (CODE-AUDIT §5.5). Check on Day 0. A broken headline feature is worse than none.
- **Diwali week** (6–11 Nov) slows recruiters. Applications sent in weeks 2–6 are the ones that convert inside this window.
- **Sleep.** The weekday template leaves 7 h. If it slips below 6.5 for three nights, cut the evening block to 60 min for that week and say so in `/replan`; do not cut sleep.
- **Silence.** If you miss three days, do not catch up. Type `/replan`.

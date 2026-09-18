# Part 05 — Self-report (20 minutes)

Rate every line 0–3. Be stingy. The scale is about *explaining*, not *using*.

- **0** — never touched it / don't know what it is
- **1** — heard of it, could not explain it
- **2** — have used it, could explain roughly what it does but not how it works
- **3** — could explain how it works internally to a sceptical interviewer, with a concrete example

Copy this file to `answers/05-self-report.md` and fill the score column. Add a short note where a score needs one (e.g. "used at Qnopy, never configured it myself").

## Java

| Topic | Score | Note |
|---|---|---|
| Stack vs heap vs metaspace; what lives where | | |
| Object header, references, `==` vs `equals` | | |
| `hashCode`/`equals` contract | | |
| String pool, immutability, `intern()` | | |
| `HashMap` internals (buckets, treeify, resize) | | |
| `LinkedHashMap`, `TreeMap` internals and when to use | | |
| `ArrayList` vs `LinkedList` internals | | |
| `ConcurrentHashMap` internals | | |
| Generics and type erasure, wildcards (`? extends`, `? super`) | | |
| Streams: laziness, intermediate vs terminal, collectors | | |
| `Optional` semantics | | |
| Exception hierarchy, checked vs unchecked, try-with-resources | | |
| Threads, `Runnable`/`Callable`, `ExecutorService`, thread pools | | |
| `CompletableFuture` | | |
| `synchronized`, `volatile`, `ReentrantLock`, `AtomicInteger` | | |
| Java Memory Model (happens-before) | | |
| Garbage collection: generations, G1, what triggers a GC | | |
| Class loading, JIT (what happens when you run `java Main`) | | |
| Java 11/17/21: records, sealed types, pattern matching, virtual threads | | |
| Interfaces: default methods, functional interfaces, lambdas under the hood | | |
| Immutability and defensive copying | | |
| `Comparable` vs `Comparator` | | |
| Serialization | | |

## Spring / Spring Boot

| Topic | Score | Note |
|---|---|---|
| IoC container, `ApplicationContext`, bean lifecycle | | |
| `@Component` / `@Service` / `@Repository` / `@Controller` differences | | |
| Autowiring: constructor vs field vs setter, why constructor | | |
| Bean scopes (singleton, prototype, request) | | |
| Spring AOP: proxies, how `@Transactional` is implemented | | |
| `@Transactional`: propagation, isolation, rollback rules, self-invocation trap | | |
| Spring Data JPA: repositories, derived queries, `@Query` | | |
| Hibernate: persistence context, entity states, dirty checking | | |
| Lazy vs eager loading, `LazyInitializationException` | | |
| N+1 problem and fixes (`JOIN FETCH`, `@EntityGraph`, batch size) | | |
| First-level vs second-level cache | | |
| `@ControllerAdvice`, exception handling, `ResponseEntity` | | |
| Bean Validation (`@Valid`, `@NotNull`) | | |
| Spring Security: filter chain, authentication vs authorization | | |
| JWT with Spring Security, refresh tokens | | |
| Profiles, `application.yml`, `@ConfigurationProperties` | | |
| Actuator, health checks, metrics | | |
| `@SpringBootTest`, `@WebMvcTest`, MockMvc, Mockito | | |
| Testcontainers | | |
| Spring Boot auto-configuration (what `@SpringBootApplication` does) | | |
| Spring MVC request lifecycle (`DispatcherServlet` → controller) | | |
| JdbcTemplate | | |
| Maven lifecycle, dependency scopes, BOM | | |

## Databases

| Topic | Score | Note |
|---|---|---|
| B-tree / B+tree index structure | | |
| Composite indexes and the left-prefix rule | | |
| Covering indexes | | |
| Reading `EXPLAIN` / `EXPLAIN ANALYZE` | | |
| How joins execute (nested loop, hash, merge) | | |
| Normalisation to 3NF; when to denormalise | | |
| ACID | | |
| Isolation levels and their anomalies | | |
| Row locks, `SELECT ... FOR UPDATE`, optimistic locking | | |
| Deadlocks | | |
| Connection pooling (HikariCP) | | |
| Window functions (`ROW_NUMBER`, `RANK`, `LAG`) | | |
| CTEs and recursive CTEs | | |
| MySQL vs Postgres differences | | |
| SQLite specifics (D1) | | |
| Migrations strategy on a live system | | |
| Redis: data structures, TTL, use as cache | | |

## JavaScript / TypeScript

| Topic | Score | Note |
|---|---|---|
| Event loop: call stack, macrotask/microtask queues | | |
| Closures and lexical scope | | |
| `this` binding rules; `call`/`apply`/`bind` | | |
| Prototype chain; `class` as sugar | | |
| Hoisting, TDZ, `var`/`let`/`const` | | |
| Promises internals; `async`/`await` desugaring | | |
| Generators and iterators | | |
| Modules: ESM vs CommonJS | | |
| Type coercion rules | | |
| TypeScript: structural typing, generics, discriminated unions, `unknown` vs `any` | | |
| TypeScript: what erases at runtime; why `as` is unsafe | | |

## React / Next.js

| Topic | Score | Note |
|---|---|---|
| Reconciliation and the diffing algorithm; why keys | | |
| Fiber (what it is, why it exists) | | |
| Rules of hooks and why they exist | | |
| `useEffect`: dependency semantics, cleanup, stale closures | | |
| `useMemo` / `useCallback` / `React.memo`: when they hurt | | |
| Context re-render behaviour | | |
| Controlled vs uncontrolled components | | |
| Compound components, render props, headless components | | |
| Zustand internals (how it avoids re-renders) | | |
| React Compiler (what it does for you) | | |
| Next.js: SSR vs SSG vs ISR vs RSC; App Router | | |
| Hydration and hydration errors | | |
| Core Web Vitals (LCP, CLS, INP) | | |
| RxJS: observables, operators, subjects, unsubscription | | |
| Angular DI and change detection (to compare against React) | | |

## Node / edge

| Topic | Score | Note |
|---|---|---|
| Node event loop phases; libuv | | |
| Streams and backpressure | | |
| Cluster and worker threads | | |
| Express/Hono middleware model | | |
| Cloudflare Workers: V8 isolates, limits, cold starts | | |
| Durable Objects: input/output gates, storage consistency | | |
| Durable Objects: alarms, hibernation, WebSocket lifecycle | | |
| D1, KV consistency models (which is eventually consistent?) | | |
| R2 lifecycle rules | | |

## System design

| Topic | Score | Note |
|---|---|---|
| SOLID with real examples | | |
| Design patterns: Strategy, Factory, Builder, Observer, Singleton, Adapter, Decorator | | |
| LLD: parking lot, rate limiter, LRU cache, notification service, URL shortener | | |
| Load balancing (L4 vs L7, algorithms) | | |
| Caching: cache-aside, write-through, invalidation, TTLs | | |
| CAP theorem, consistency models | | |
| SQL vs NoSQL selection | | |
| Message queues (Kafka/RabbitMQ/SQS), at-least-once vs exactly-once | | |
| Idempotency keys | | |
| Rate limiting algorithms | | |
| CDNs | | |
| WebSockets vs SSE vs long polling | | |
| Consistent hashing | | |
| Database sharding and replication | | |

## DevOps / SDLC

| Topic | Score | Note |
|---|---|---|
| Docker: images vs containers, layers, multi-stage builds | | |
| docker-compose | | |
| Kubernetes: pods, deployments, services, ingress, configmaps, secrets | | |
| CI/CD: GitHub Actions | | |
| Jenkins | | |
| Git: rebase, cherry-pick, bisect, reflog, conflict resolution | | |
| Linux basics: processes, ports, `curl`, logs | | |
| Agile/Scrum ceremonies, story points, definition of done | | |
| Observability: logs, metrics, traces | | |

## GenAI

| Topic | Score | Note |
|---|---|---|
| Tokens, context windows, temperature | | |
| Embeddings and what a vector represents | | |
| Vector databases and ANN search | | |
| RAG pipeline: chunking, retrieval, evaluation | | |
| Prompt engineering: system prompts, few-shot, structured output | | |
| Function/tool calling | | |
| Agent loop from scratch | | |
| MCP | | |
| Evals and guardrails | | |
| Cost / latency / hallucination mitigation | | |

## DSA patterns (rate "could recognise and code from memory")

| Pattern | Score | Note |
|---|---|---|
| Two pointers | | |
| Sliding window | | |
| Fast/slow pointers | | |
| Merge intervals | | |
| Cyclic sort | | |
| In-place linked list reversal | | |
| BFS / DFS on trees | | |
| BFS / DFS on graphs; topological sort | | |
| Backtracking / subsets / permutations | | |
| Modified binary search | | |
| Heaps: top-K, k-way merge | | |
| Greedy | | |
| 1D DP | | |
| 2D DP / grid | | |
| Knapsack variants | | |
| Tries | | |
| Union-find | | |
| Bit manipulation | | |
| Monotonic stack | | |
| Prefix sums | | |

## Two last questions

1. How many LeetCode-style problems have you solved in the last 12 months, roughly? How many mediums without hints?
2. How many technical interviews have you sat in your life, and what happened in the last one?

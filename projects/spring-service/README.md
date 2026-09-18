# DocDrop — the Java/Spring Boot project

**Why this project.** Every public artefact you have is TypeScript on Cloudflare; all your Java is inside Qnopy's codebase. You are positioning as a Java/Spring engineer, so you need one small, deep Spring Boot service on GitHub that you can defend line by line. DocDrop is your granted patent (secure document transfer to local photocopy centres) turned into code. That gives you a project story and the patent story in one breath, and a real state machine with real concurrency to defend.

Deliberately small: five entities, one bounded flow, everything tested. Depth beats breadth. Code lives in its own repo (`github.com/Animish2002/docdrop`); this file is the spec and the log.

## The flow

1. A user uploads a document (store metadata + a blob on local disk or MinIO; the file itself is not the point) and chooses a centre.
2. The service creates a `PrintJob` in `PENDING` with a short-lived, single-use claim code.
3. A centre operator enters the code. The claim must succeed **exactly once** even if two operators submit it concurrently.
4. The centre marks the job `PRINTED`. Unclaimed jobs expire after 24 h by a scheduled job; expired documents are deleted.
5. A reporting endpoint returns jobs per centre per day with a running total.

## Entities

`User` · `Centre` · `Document` (owner, key, size, checksum, expires_at) · `PrintJob` (document, centre, status `PENDING → CLAIMED → PRINTED | EXPIRED`, `@Version`, claimed_at, printed_at) · `ClaimToken` (job, code hash, expires_at, used_at)

Indexes you must justify: `print_jobs(centre_id, status, created_at)`, `claim_tokens(code_hash)` unique, `documents(expires_at)` partial where not deleted.

## What it must demonstrate, and where each is scheduled

| Requirement | Day |
|---|---|
| Spring Boot layered properly (controller / service / repository), Spring Data JPA | 27 |
| One deliberate `JdbcTemplate` path: the reporting query, with a window function | 27 |
| Postgres via docker-compose, Flyway migrations, real indexes | 27 |
| `@DataJpaTest` on Testcontainers; unit tests on the state machine | 27 |
| Claim as an atomic state transition: `UPDATE ... WHERE status = 'PENDING'` plus `@Version`; a test that runs two claims concurrently and asserts one wins | 41 |
| Spring Security with JWT access + refresh-token rotation | 41 |
| `@ControllerAdvice` with problem-details bodies, Bean Validation | 41 |
| `@Scheduled` expiry job; idempotent on rerun | 41 |
| Documented before/after `EXPLAIN ANALYZE` on the reporting query | 41 |
| Multi-stage Dockerfile, docker-compose, GitHub Actions running Testcontainers | 39, 41 |
| README for a hiring manager: problem, diagram, three hardest decisions, limitations, 100× | 55 |
| Small React front end reusing Qnopy component-library thinking (optional, only if weeks 6–7 run ahead) | — |

## Decisions to be able to defend

- Why `IDENTITY` vs `SEQUENCE` for ids, and what it does to batch inserts.
- Why optimistic locking on `PrintJob` and a conditional `UPDATE` on claim, not `SELECT ... FOR UPDATE`.
- Why the claim code is stored hashed and why a fast hash is fine there but not for passwords (same reasoning as Kcal's tokens vs PBKDF2).
- Why the expiry job is idempotent and what happens if two instances run it.
- What `@Transactional` boundary each service method has and why.
- Where the N+1 would appear in the reporting endpoint if written with JPA, and why you dropped to `JdbcTemplate`.

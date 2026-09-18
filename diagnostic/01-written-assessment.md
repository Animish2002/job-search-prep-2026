# Part 01 — Written assessment (90 minutes)

26 questions. Short answers: 2–6 sentences, or a trace for "what does this print". Where a question says *why*, the why is the whole mark. Write in `answers/01-written.md`.

---

## A. Java internals (Q1–Q8)

**Q1.** Walk through exactly what happens, step by step, inside `HashMap` when this runs on a fresh map:

```java
Map<String, Integer> m = new HashMap<>();
m.put("apple", 1);
m.put("banana", 2);
m.get("apple");
```

Name the fields and methods involved (as many real ones as you can), how the bucket index is computed from the hash, what a collision is and how it's stored, and what happens after "enough" entries.

**Q2.** A class overrides `equals()` but not `hashCode()`. Two instances are `equals()` to each other. You `put` one as a key and `get` with the other. What happens and why?

**Q3.** What does this print, and why?

```java
Integer a = 127, b = 127;
Integer c = 128, d = 128;
String s1 = "hello", s2 = "hello";
String s3 = new String("hello");
System.out.println(a == b);
System.out.println(c == d);
System.out.println(s1 == s2);
System.out.println(s1 == s3);
System.out.println(s1.equals(s3));
```

**Q4.** What does this print? Then: what is the time complexity of building a string of *n* characters with `s += c` in a loop, and why?

```java
String s = "a";
s.concat("b");
s.toUpperCase();
System.out.println(s);
```

**Q5.** Two separate questions about `List<Integer> list = new ArrayList<>(List.of(10, 20, 30))`:
(a) What happens with `for (Integer x : list) { if (x == 20) list.remove(x); }` and why?
(b) What does `list.remove(1)` remove, and what would `list.remove(Integer.valueOf(1))` do? Why are they different?

**Q6.** What does this method return, and why?

```java
static int f() {
    try {
        throw new RuntimeException("boom");
    } catch (RuntimeException e) {
        return 1;
    } finally {
        return 2;
    }
}
```

Then: is `NullPointerException` checked or unchecked? What is the practical difference to a caller? Name the top of the hierarchy that both `Exception` and `Error` extend.

**Q7.** Two threads each run `for (int i = 0; i < 10_000; i++) counter++;` on a shared `volatile int counter`. What is the final value range and why? What does `volatile` actually guarantee, and what would you change to make this correct? Name at least two options.

**Q8.** (a) Does `List<Object> l = new ArrayList<String>();` compile? Why or why not?
(b) Why can't you write `new T()` inside a generic class `Box<T>`?
(c) What does this print, and what does it tell you about streams?

```java
Stream.of(1, 2, 3).peek(x -> System.out.println("saw " + x)).map(x -> x * 2);
System.out.println("done");
```

**Q9.** Where do these live at runtime: the `int[]` object created by `new int[1000]`, the local variable holding its reference, a `static final String NAME`, and a class's bytecode? When does the array become eligible for garbage collection? Give one concrete example of a memory leak in Java (there is no `free()`, so what leaks?).

## B. JavaScript semantics (Q10–Q16)

**Q10.** Write the exact output order:

```js
console.log('1')
setTimeout(() => console.log('2'), 0)
Promise.resolve().then(() => console.log('3'))
queueMicrotask(() => console.log('4'))
;(async () => {
  console.log('5')
  await null
  console.log('6')
})()
console.log('7')
```

Then explain the rule that produces this order, using the words *macrotask* and *microtask*.

**Q11.** What does each print, and why are they different?

```js
for (var i = 0; i < 3; i++) setTimeout(() => console.log(i))
for (let i = 0; i < 3; i++) setTimeout(() => console.log(i))
```

**Q12.** What does each line print?

```js
const obj = {
  name: 'kcal',
  regular() { return this.name },
  arrow: () => this?.name,
  nested() { return [1].map(function () { return this?.name }) },
}
console.log(obj.regular())
const f = obj.regular
console.log(f())
console.log(obj.arrow())
console.log(obj.nested())
console.log(obj.regular.call({ name: 'other' }))
```

State the four rules for what `this` is, in priority order.

**Q13.** Evaluate each. One line of reasoning each.

```js
[] + []
[] + {}
'5' - 2
'5' + 2
null == undefined
null === undefined
NaN === NaN
typeof null
typeof (() => {})
0.1 + 0.2 === 0.3
[1, 2, 10].sort()
```

**Q14.** `const arr = [1, 2]`. Explain how `arr.map` is found when you call it, naming every object visited. What does `arr.hasOwnProperty('map')` return? What is the difference between `__proto__` and `prototype`?

**Q15.** What happens on each line, and why?

```js
console.log(a)
var a = 1
console.log(b)
let b = 2
console.log(typeof c)
c()
function c() {}
d()
const d = () => {}
```

**Q16.** (a) What does an `async` function return if you `return 42` from it?
(b) What is the difference between these, in total time and in behaviour when one call rejects?

```js
for (const id of ids) results.push(await fetchOne(id))
const results = await Promise.all(ids.map(fetchOne))
```

(c) Rewrite `async function g() { return await fetch(url) }` so that `try/catch` around it behaves correctly, and explain when `return await` matters.

## C. SQL and databases (Q17–Q21)

**Q17.** Your PrepArena messages query is:

```sql
SELECT * FROM messages WHERE conversation_id = ? ORDER BY sent_at DESC LIMIT 40;
```

There is no index on `messages` except the primary key. (a) Describe what the database physically does to answer this on a table of 5 million rows. (b) Write the single best index. (c) Would `(sent_at, conversation_id)` work as well? Why or why not? (d) What is a B-tree, in two sentences, and why does it make (b) fast?

**Q18.** Two requests for the same user arrive at the same time. Each does:

```
row = SELECT total_calories FROM daily_summaries WHERE user_id=? AND date=?
UPDATE daily_summaries SET total_calories = row.total_calories + :meal WHERE id = row.id
```

What can go wrong? Name the anomaly. Give two different fixes, one that changes the SQL and one that uses a transaction feature.

**Q19.** (a) What is the difference between these two queries? Give a case where their results differ.

```sql
SELECT u.id, COUNT(b.id) FROM users u LEFT JOIN battles b ON b.challenger_id = u.id GROUP BY u.id;
SELECT u.id, COUNT(b.id) FROM users u LEFT JOIN battles b ON b.challenger_id = u.id WHERE b.status = 'completed' GROUP BY u.id;
```

(b) What is the difference between `COUNT(*)` and `COUNT(b.id)` in the first query?

**Q20.** `GET /chat/conversations` loads N conversations, then for each one runs a query for the other user and a query for the unread count. (a) Name this problem. (b) Write one SQL query that returns conversation id, other user's username, and unread count for a given user in a single round trip. (c) What is the cost of your version compared to the original when N = 200?

**Q21.** (a) What does ACID stand for, one line each, in terms of what a *bug* looks like when each is violated. (b) Name the four SQL isolation levels from weakest to strongest and, for each, one anomaly it still permits. (c) What is a deadlock and how does a database resolve one?

## D. HTTP and the web (Q22–Q25)

**Q22.** (a) When should an endpoint be `POST` vs `PUT` vs `PATCH`? Define *idempotent* and say which of the three are. (b) A client calls `POST /battles/:id/accept` on a battle that is already active. Which status code, and why not 400? (c) 401 vs 403: one sentence each.

**Q23.** Your Kcal frontend on `vercel.app` calls your API on `workers.dev`. (a) What is a CORS preflight, which request triggers it, and what does the browser check in the response? (b) Why does the browser do this at all, given the server could just reject the request? (c) What does `credentials: true` change?

**Q24.** JWT in `localStorage` (what both your apps do) vs JWT in an `httpOnly; SameSite=Lax; Secure` cookie. (a) Which attack does each defend against, and which does each remain vulnerable to? (b) Why did you end up putting the token in a redirect URL in PrepArena, and what is the risk of that? (c) What is the purpose of a refresh token, and what does your 7-day/30-day single-token design give up?

**Q25.** (a) Describe the WebSocket handshake: the request headers, the response status, and what changes about the TCP connection afterwards. (b) Why can't a browser's `new WebSocket(url)` send an `Authorization` header, and what are the two common workarounds? (c) What happens to a WebSocket held by a Durable Object when the DO hibernates?

## E. Complexity (Q26)

**Q26.** Give Big-O time (and space where asked) for each, with one line of justification:

(a) `for i in list: if list.contains(x)` over an `ArrayList` of n elements.
(b) `HashMap.get` — average, and worst case in Java 7 vs Java 8+. Why did it change?
(c) Binary search on a sorted array; then on a sorted linked list.
(d) Naive recursive `fib(n)`. Write the recurrence. Then with memoisation. Space for each.
(e) Your `getStreak`: load all activity rows for a user (r rows), build a `Set` of day numbers, sort it, scan. Time and space in r. Then: what would the SQL version cost?
(f) `ArrayList.add` is "O(1) amortised". What does amortised mean here, and what is the worst single call?
(g) Recursive DFS on a binary tree with n nodes and height h: time, and space on the call stack.

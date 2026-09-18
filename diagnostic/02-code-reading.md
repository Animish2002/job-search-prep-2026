# Part 02 — Code reading (60 minutes, 12 minutes per snippet)

Five snippets you did not write. For each, answer **in writing, after saying it out loud**:

1. **What does it do?** Two or three sentences, as if explaining to a teammate.
2. **What does it return / print** for the given input? Trace it. Show intermediate values.
3. **Where is the bug or edge case?** There is at least one real defect in every snippet. Some have two.
4. **How would you fix or refactor it?** Describe the change; code is optional.

Start a timer per snippet. If you run out, write "TIME" and move on. Write in `answers/02-code-reading.md`.

---

## Snippet 1 — Java, stream pipeline

```java
import java.util.*;
import java.util.stream.*;

class Order {
    final String customer;
    final String status;
    final double amount;
    Order(String customer, String status, double amount) {
        this.customer = customer; this.status = status; this.amount = amount;
    }
}

public class Report {
    static Map<String, Double> topSpenders(List<Order> orders, double minTotal) {
        return orders.stream()
            .filter(o -> !"CANCELLED".equals(o.status))
            .collect(Collectors.groupingBy(o -> o.customer,
                                           Collectors.summingDouble(o -> o.amount)))
            .entrySet().stream()
            .filter(e -> e.getValue() >= minTotal)
            .sorted(Map.Entry.<String, Double>comparingByValue().reversed())
            .limit(3)
            .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
    }

    public static void main(String[] args) {
        List<Order> orders = List.of(
            new Order("ana",  "PAID",      120.0),
            new Order("ben",  "PAID",       80.0),
            new Order("ana",  "CANCELLED", 500.0),
            new Order("cy",   "PAID",      200.0),
            new Order("ben",  "PAID",       70.0),
            new Order("dee",  "PAID",      150.0),
            new Order(null,   "PAID",       10.0)
        );
        System.out.println(topSpenders(orders, 100.0));
    }
}
```

Input: as in `main`. Questions 1–4 above. Extra: what does the caller of `topSpenders` probably *expect* about the returned map that this code does not guarantee?

---

## Snippet 2 — Java, `synchronized`

```java
public class TokenBucket {
    private int tokens;
    private long lastRefill;
    private final int capacity;
    private final long refillIntervalMs;

    public TokenBucket(int capacity, long refillIntervalMs) {
        this.capacity = capacity;
        this.tokens = capacity;
        this.refillIntervalMs = refillIntervalMs;
        this.lastRefill = System.currentTimeMillis();
    }

    public boolean tryAcquire() {
        refill();
        synchronized (this) {
            if (tokens > 0) {
                tokens--;
                return true;
            }
            return false;
        }
    }

    private void refill() {
        long now = System.currentTimeMillis();
        if (now - lastRefill >= refillIntervalMs) {
            synchronized (this) {
                tokens = capacity;
                lastRefill = now;
            }
        }
    }

    public int available() {
        return tokens;
    }
}
```

Input scenario: `new TokenBucket(1, 1000)`. Thread A and thread B both call `tryAcquire()` at t=0 ms. Then at t=1000 ms, A and B both call `tryAcquire()` again, and a third thread C calls `available()` at t=1001 ms.

Questions 1–4 above, and: can both A and B get `true` on the first call? Can `refill()` run its body twice for one interval? What might C see, and why is that not guaranteed? Is this a token bucket?

---

## Snippet 3 — JavaScript, closures and `this`

```js
function makeHandlers(labels) {
  const handlers = {}
  for (var i = 0; i < labels.length; i++) {
    handlers[labels[i]] = function () {
      return labels[i] + '#' + i
    }
  }
  return handlers
}

function debounce(fn, ms) {
  let timer
  return function (...args) {
    clearTimeout(timer)
    timer = setTimeout(() => fn.apply(this, args), ms)
  }
}

const h = makeHandlers(['save', 'cancel'])
console.log(h.save(), h.cancel())

const form = {
  name: 'signup',
  submit(evt) { return `${this.name}:${evt}` },
}
form.debouncedSubmit = debounce(form.submit, 100)
form.debouncedSubmit('click')
form.debouncedSubmit('click')
form.debouncedSubmit('enter')

const detached = form.debouncedSubmit
detached('key')
```

Questions 1–4 above, and: what does `console.log` print? How many times does `submit` eventually run across all four `debouncedSubmit`/`detached` calls, with what `this` and what argument each time? What is the minimal change to `makeHandlers` that fixes it, and *why* does that change fix it?

---

## Snippet 4 — JavaScript, async race

```js
// search box: fires on every keystroke
let latestResults = []

async function search(query) {
  const res = await fetch(`/api/problems?search=${query}`)
  const data = await res.json()
  latestResults = data.problems
  render(latestResults)
}

input.addEventListener('input', (e) => search(e.target.value))

// batch loader used on the dashboard
async function loadAll(ids) {
  const results = []
  ids.forEach(async (id) => {
    const r = await fetch(`/api/problems/${id}`)
    results.push(await r.json())
  })
  return results
}

async function init() {
  const problems = await loadAll(['p1', 'p2', 'p3'])
  console.log(problems.length)
}
init()
```

Scenario: the user types `t`, `tw`, `two` quickly. The request for `t` is slow and returns last.

Questions 1–4 above, and: what does the user see after all three responses arrive? What does `init` log, and why? Give two different fixes for `search` (one using a counter, one using `AbortController`) and one fix for `loadAll`.

---

## Snippet 5 — Java, recursive tree walk

```java
import java.util.*;

class Node {
    int val; Node left, right;
    Node(int v) { val = v; }
}

public class Paths {
    static List<List<Integer>> rootToLeaf(Node root) {
        List<List<Integer>> out = new ArrayList<>();
        walk(root, new ArrayList<>(), out);
        return out;
    }

    private static void walk(Node n, List<Integer> path, List<List<Integer>> out) {
        if (n == null) return;
        path.add(n.val);
        if (n.left == null && n.right == null) {
            out.add(path);
            return;
        }
        walk(n.left, path, out);
        walk(n.right, path, out);
        path.remove(path.size() - 1);
    }

    public static void main(String[] args) {
        Node r = new Node(1);
        r.left = new Node(2);
        r.right = new Node(3);
        r.left.left = new Node(4);
        System.out.println(rootToLeaf(r));
    }
}
```

Tree:

```
    1
   / \
  2   3
 /
4
```

Questions 1–4 above, and: trace `path` after every `add` and `remove`. What does `main` print exactly? There are two distinct defects; name both. What would `path.remove(n.val)` do instead of `path.remove(path.size() - 1)`, and why is that a trap?

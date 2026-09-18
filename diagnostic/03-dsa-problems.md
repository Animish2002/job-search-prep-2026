# Part 03 — DSA (70 minutes total, timed, no hints)

Rules: Java. Plain text editor or a file with autocomplete off if you can manage it. Start a timer per problem. No searching. When a timer ends, stop writing code and write what you had and where you were stuck.

For each problem record, in `answers/03-dsa.md`:

- your code (whatever state it's in),
- time taken,
- time and space complexity with one line of justification,
- **the moment you "saw" the approach**, or the moment you realised you hadn't,
- what you'd test it with (3 cases including one edge).

Do not paste these into LeetCode to check. I will run them.

---

## Problem 1 — Easy (10 minutes)

**Valid Parentheses.** Given a string containing only `(`, `)`, `{`, `}`, `[`, `]`, return `true` if every opening bracket is closed by the same type in the correct order.

```
"()[]{}"  → true
"([)]"    → false
"{[]}"    → true
"("       → false
""        → true
```

Signature: `static boolean isValid(String s)`

---

## Problem 2 — Medium (25 minutes)

**Longest Substring Without Repeating Characters.** Given a string, return the length of the longest substring with no repeated characters.

```
"abcabcbb" → 3   ("abc")
"bbbbb"    → 1
"pwwkew"   → 3   ("wke", not "pwke" which is a subsequence)
""         → 0
"abba"     → 2   (watch this one)
```

Signature: `static int lengthOfLongestSubstring(String s)`

Target: O(n) time. If you get O(n²) working first, note it, then try to improve in the remaining time.

---

## Problem 3 — Medium-hard (35 minutes)

**Course Schedule.** There are `numCourses` courses labelled `0 .. numCourses-1`. `prerequisites[i] = [a, b]` means you must take course `b` before course `a`. Return `true` if it is possible to finish all courses, `false` otherwise.

```
numCourses = 2, prerequisites = [[1,0]]        → true   (0 then 1)
numCourses = 2, prerequisites = [[1,0],[0,1]]  → false  (cycle)
numCourses = 4, prerequisites = [[1,0],[2,1],[3,2]] → true
numCourses = 3, prerequisites = []             → true
```

Signature: `static boolean canFinish(int numCourses, int[][] prerequisites)`

Before coding, write two sentences: what is this problem *really* asking, in graph terms? Then code.

---

## After all three

One paragraph: which of the three felt like recall, which felt like reasoning, and which felt like guessing? That distinction is what the DSA track will be built around.

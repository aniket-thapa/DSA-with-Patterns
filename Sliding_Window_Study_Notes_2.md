# Sliding Window Pattern — Complete Notes

*A self-contained, beginner-to-advanced guide built from the full lecture series. Designed to be revised in 15–20 minutes before an interview.*

---

## 1. What is Sliding Window?

**Window** = a continuous segment (a "chunk") of an array or string, marked by two pointers — `low` (start) and `high` (end).

**Sliding** = that window can move, and its size can grow or shrink, as you scan through the array/string once.

- Moving `high` forward → window **expands** (grows to the right).
- Moving `low` forward → window **shrinks** (cuts off from the left).

Think of it like a sliding door: the window always grows to the right (by moving `high`) and is trimmed from the left (by moving `low`). It never moves backward.

The Sliding Window technique is built directly on top of **Two Pointers** — `low` and `high` are the two pointers, and both only ever move forward (left → right), never backward.

> **Core idea:** Instead of recomputing information for every possible subarray/substring from scratch (Brute Force, usually O(n²) or worse), you reuse the work you already did for the previous window and just adjust for what entered and what left. That's what makes it fast.

---

## 2. When to Use Sliding Window?

### 2.1 The Flowchart (3 checks, in order)

Ask these three questions about the problem, in order. If any answer is "No," stop — Sliding Window does not apply.

```
        ┌───────────────────────────────────────┐
        │ Q1: Is this an ARRAY or STRING        │
        │     question? (NOT Linked List)        │
        └───────────────────┬───────────────────┘
                    NO ──────┤───► STOP. Not Sliding Window.
                             │
                            YES
                             ▼
        ┌───────────────────────────────────────┐
        │ Q2: Does it ask about a SUBARRAY or    │
        │     SUBSTRING — i.e., something        │
        │     CONTINUOUS?                        │
        └───────────────────┬───────────────────┘
                    NO ──────┤───► STOP. (Maybe Subsequence → DP)
                             │
                            YES
                             ▼
        ┌───────────────────────────────────────┐
        │ Q3: Are you asked to find one of:      │
        │  Maximum, Minimum, Longest, Shortest,  │
        │  Sum, Count, Average,                  │
        │  At Most K, At Least K, Exactly K      │
        └───────────────────┬───────────────────┘
                    NO ──────┤───► STOP. Not Sliding Window.
                             │
                            YES
                             ▼
              ✅  USE SLIDING WINDOW
                             │
              ┌──────────────┴───────────────┐
              ▼                               ▼
     Window size IS given             Window size NOT given
     ("subarray of size K")          ("find the longest/shortest")
              │                               │
              ▼                               ▼
        FIXED WINDOW                   VARIABLE WINDOW
```

If all three checks pass, there's a very high chance (90%+) this is a Sliding Window problem.

### 2.2 How to Identify Sliding Window in Interviews

- **Read the question in plain language first** — don't jump to code. Mentally restate what's actually being asked. Often the keyword "subarray"/"substring" isn't literally written (e.g., *Fruits into Baskets* never says "subarray" — it's a story about picking fruit left to right from trees, but it's really "longest subarray with at most 2 distinct values").
- Once you spot the 3 conditions above, **say it out loud to the interviewer**: *"This looks like a Sliding Window problem because it's about a contiguous subarray and we're optimizing for the longest/shortest/sum..."* — this signals strong pattern recognition early.
- It's not 100% guaranteed — a small fraction of look-alike problems are actually Greedy or DP. But starting with Sliding Window as your first hypothesis is the right strategy, because it's right far more often than it's wrong, and ruling it out is itself useful information.
- **Sliding Window shows up in roughly half of all "medium" interview questions.** It's one of the highest-yield patterns to master — much more frequently asked than Graphs or DP in a typical interview loop.

### 2.3 Array vs String vs Linked List

| Data structure | Sliding Window applies? |
|---|---|
| Array | ✅ Yes |
| String | ✅ Yes (a string is just an array of characters) |
| Linked List | ❌ No, in ~99.9% of cases |

**Why not Linked List?** Sliding Window relies on quick index arithmetic (`high - low + 1`, jumping pointers around, random access). Linked Lists don't give you that — you can't jump to "low - 1" or compute a length in O(1). So for practical purposes: if you see Linked List, stop thinking Sliding Window.

### 2.4 Subarray vs Substring vs Subsequence

This is the single most important distinction to get right before applying the pattern.

| Term | Meaning | Continuous? | Sliding Window? |
|---|---|---|---|
| **Subarray** | A contiguous chunk of an array | ✅ Yes | ✅ Applies |
| **Substring** | A contiguous chunk of a string | ✅ Yes | ✅ Applies |
| **Subsequence** | Any elements picked in order, but not necessarily adjacent | ❌ No | ❌ Does NOT apply (usually DP/Greedy/Recursion) |

**Example:** Array = `[1, 2, 3]`.
- Subarrays: `[1]`, `[2]`, `[3]`, `[1,2]`, `[2,3]`, `[1,2,3]` (must be back-to-back elements)
- A subsequence could be `[1, 3]` — skipping `2` entirely is allowed. This is **not** a valid subarray.

> ⚠️ **Common trap:** people see "subsequence" in a question and instinctively reach for Sliding Window. Don't. Subsequence = non-contiguous = Sliding Window will give wrong answers because it assumes elements are touching.

---

## 3. Types of Sliding Window

### 3.1 Fixed Size Window

Used when the problem **tells you the exact window size** — e.g., "subarray of size K," "substring of length 3."

- `low` and `high` start together, exactly `K` apart.
- As the window slides, **its size never changes** — one element leaves from the left for every element that enters from the right.

**Example:** *"Find the maximum sum of any subarray of size 3."* → Fixed window of size 3.

### 3.2 Variable Size Window

Used when the problem does **not** give you a fixed size — e.g., "find the longest substring...", "find the minimum length subarray...", "find the shortest window...".

- Both `low` and `high` start at index `0` (window size starts at 1, before even that, at 0).
- The window expands (`high++`) and shrinks (`low++`) dynamically based on a condition. Sometimes it's big, sometimes small — it breathes in and out as you scan.

**Rule of thumb:** No explicit size mentioned in the question → assume Variable Window. Don't overthink this step.

---

## 4. Core Intuition

### 4.1 Window Expansion and Shrinking

- `high++` → window **expands** → an element is **added** to the window's data.
- `low++` → window **shrinks** → an element is **removed** from the window's data.

The window only ever grows on the right and gets trimmed on the left — it never reverses direction. This one-directional movement is exactly what keeps the algorithm to O(n) instead of O(n²).

### 4.2 low / high Pointers

- `low` = start of the window (inclusive)
- `high` = end of the window (inclusive)
- **Window length** = `high - low + 1` (memorize this formula — you'll use it in every single Sliding Window problem)

### 4.3 Why Sliding Window is Efficient

**The Brute Force way:** for every possible subarray, re-traverse it from scratch to compute its sum/frequency/etc. This is wasteful — most of the window is identical to the previous one.

**The Sliding Window way — the "Bank Account" analogy:**
> If you have ₹1 lakh in your bank account, spend ₹100 on a coffee, and someone gives you ₹50 — does the bank empty your account and recount everything from zero? No. It just does `100,000 − 100 + 50`. That's exactly what Sliding Window does with sums, frequencies, or any other running "information."

So instead of recomputing from scratch:
```
new_info = old_info  -  (element leaving at low)  +  (element entering at high)
```

This turns an O(n × k) or O(n²) brute force into a clean **O(n)** pass — each element is added to the window exactly once and removed at most once.

### 4.4 The "Information" of a Window (4-Step Mental Model)

Every Sliding Window problem, no matter how different it looks, is solved using the same **4 steps**:

1. **Identify** — is this even a Sliding Window question? (Use the flowchart in Section 2.)
2. **Find the window type** — Fixed or Variable?
3. **Find the starting window's information** — "information" = whatever meaningful fact the window tells you (its sum, its max, its character frequencies, its count of distinct elements, etc.). Compute this for the very first window.
4. **Slide the window & update the information** — as `low`/`high` move, update the information incrementally (never recompute from scratch), and keep checking/recording your answer.

> **Interview gold:** Say this out loud — *"What information does my window need to track, and how do I update that information in O(1) when the window slides?"* — this is literally the whole algorithm in one sentence.

---

## 5. Fixed Window Template

### Generic Template (pseudocode)

```text
low = 0
high = K - 1            // window size is K, so high starts at K-1

// Step 1: Build the FIRST window's information manually
for i = low to high:
    info = info + element[i]      // e.g., sum, or whatever "information" means here

res = initial_value (e.g., INT_MIN for max, INT_MAX for min)

// Step 2: Slide the window across the rest of the array
while high < n:
    res = combine(res, info)      // record current window's info into the result

    // remove the leaving element (low), then move low forward
    info = info - element[low]
    low = low + 1

    // move high forward
    high = high + 1
    if high == n:
        break

    // add the newly entered element (high)
    info = info + element[high]

return res
```

### Step-by-Step Explanation

1. `low = 0`, `high = K - 1` — this is **always** your fixed-window starting point. If `K = 3`, `high` starts at index `2`.
2. Manually compute the information (sum/max/etc.) for this very first window only — this is the one time you do "real work."
3. Enter a loop that runs `while (high < n)`.
4. Record the current window's info into your answer (`res`).
5. Slide: remove the element at `low` from the info, increment `low`.
6. Increment `high`. **Check the boundary** — if `high == n`, you've gone past the array, so break immediately (don't try to read `array[high]`, that's an out-of-bounds access).
7. Add the new element at `high` into the info.
8. Repeat until the loop ends, then return `res`.

### Time & Space Complexity

| | Complexity | Why |
|---|---|---|
| **Time** | O(N) | The array is traversed once; `low` and `high` each move forward at most N times total. |
| **Space** | O(1) | Only a few variables are used — no extra data structure scales with input size (unless the problem specifically needs a hashmap, e.g. for distinct counts). |

---

## 6. Variable Window Template

### 6.1 The Big Secret: Maximum Window ≠ Minimum Window

This is the single most important — and most commonly missed — insight about Variable Windows: **the template for finding a Maximum/Longest window is the mirror opposite of the template for finding a Minimum/Shortest window.** Many learners memorize one version and get stuck the moment the other type shows up. Don't memorize the direction — understand *why* it flips, and you'll never get confused.

**The pattern always starts the same way, regardless of max or min:**

```text
low = 0, high = 0
for high = 0 to n-1:
    include high in the information
    ... (this is where Max and Min diverge) ...
return res
```

| | **Maximum / Longest Window** | **Minimum / Shortest Window** |
|---|---|---|
| **Typical condition phrasing** | "...should be **≤** K" / "at most K" / "exactly K" | "...should be **≥** K" / "at least K" |
| **When do you shrink `low`?** | While the info is **invalid** (broke the upper limit) | While the info is **valid** (already satisfies the lower limit) |
| **When do you record the answer?** | *After* shrinking — once info is valid again | *Before* shrinking — every single time info is valid |

**Why the condition direction always flips this way:**
- For a **maximum** window, the constraint must be "≤ something." If it were "≥ something" instead (e.g., "find the longest subarray with sum greater than 80"), then once you found *any* valid window, adding more elements (assuming non-negative values) keeps it valid forever — so the answer would trivially be the entire array. That's not a real question.
- For a **minimum** window, the constraint must be "≥ something" for the same reason in reverse — if it were "≤ something," a single element (or even an empty array) would often already satisfy it, making the question meaningless.

> **The Hiring & Firing Analogy (for Maximum-style problems):** A company needs a task done. It hires people one by one (`high++`) until the work gets done. Once the work is happening, the company gets greedy and starts firing people from the order they were hired (`low++`, FIFO) to see if fewer people can still get the job done. The moment firing breaks the task, it stops firing and goes back to hiring. This back-and-forth *is* the sliding window.

> **The reverse Hiring & Firing Analogy (for Minimum-style problems):** Same company, but now the goal is *minimum* headcount that gets the job done. As soon as the job **is** getting done with the current team, that's a valid headcount worth recording — and then you immediately try removing people to see if you can do it with even fewer. You only stop removing once the work *stops* getting done.

### 6.2 Maximum / Longest Window — Generic Template

```text
low = 0
res = INT_MIN          // (or however "no valid answer yet" is represented)

for high = 0 to n - 1:
    include(high) in info             // e.g. info[s[high]]++, or sum += a[high]

    while info is INVALID:             // e.g. distinct count > K, or sum > limit
        remove(low) from info
        low++

    // at this point info is guaranteed valid (or could still need an exact check)
    if info satisfies the exact required condition:     // e.g. == K for "exactly K"
        length = high - low + 1
        res = max(res, length)

return res
```

### 6.3 Minimum / Shortest Window — Generic Template

```text
low = 0
res = INT_MAX

for high = 0 to n - 1:
    include(high) in info

    while info is VALID:                // e.g. sum >= target
        length = high - low + 1
        res = min(res, length)          // record BEFORE shrinking further

        remove(low) from info
        low++

    // loop naturally exits once info becomes invalid — nothing more to do here

return (res == INT_MAX) ? 0 : res
```

### 6.4 Side-by-Side Comparison

| Step | Maximum Window | Minimum Window |
|---|---|---|
| Loop `high` from 0 to n | ✅ Same | ✅ Same |
| Include `high` in info | ✅ Same | ✅ Same |
| Shrink condition | `while (info invalid)` | `while (info valid)` |
| When result is updated | After the shrink loop, outside it | Inside the shrink loop, before each shrink step |
| What happens after the inner loop | Record result (if valid) | Nothing — already recorded inside |

---

## 7. Pattern Recognition Guide

### Keyword → Meaning Table

| Keyword in the question | What it usually means |
|---|---|
| **Maximum / Longest** | Use the **Maximum Window** template |
| **Minimum / Shortest** | Use the **Minimum Window** template |
| **Sum** | "Information" to track = running sum |
| **Count** | "Information" to track = a counter or frequency map |
| **Average** | Track sum + length, divide when needed |
| **At Most K** | Maximum-style; valid whenever `distinct/count ≤ K` (no extra "exact" check needed) |
| **At Least K** | Minimum-style; valid whenever `count/sum ≥ K` |
| **Exactly K** | Maximum-style, but needs an extra `if (info == K)` check before recording |
| **Fixed length given (e.g. "size K")** | Use **Fixed Window** |
| **No length given ("the longest…", "the minimum…")** | Use **Variable Window** |

### Deciding Which Template to Use — Quick Steps

1. Does the question give an exact window size? → **Fixed Window**.
2. If not → it's **Variable Window**. Now ask: is the question asking for the **longest/maximum-style** thing, or the **shortest/minimum-style** thing?
   - Longest / Maximum / At Most K / Exactly K → **Maximum Window template** (shrink while invalid, record after).
   - Shortest / Minimum / At Least K → **Minimum Window template** (shrink while valid, record during).
3. Figure out what single piece of "information" the window must track (sum? distinct count via hashmap? max frequency?).
4. Figure out the exact rule for "valid" vs "invalid" information, based on the question's wording.
5. Plug into the matching template.

---

## 8. Important Sliding Window Templates (Cheat-Code Versions)

### 8.1 Fixed Window Template

```cpp
int low = 0, high = K - 1, info = 0, res = INT_MIN; // or INT_MAX for min
for (int i = low; i <= high; i++) info += arr[i];

while (high < n) {
    res = max(res, info);          // process result
    info -= arr[low]; low++;       // remove left
    high++;
    if (high == n) break;
    info += arr[high];             // add right
}
return res;
```

### 8.2 Variable — Maximum Window (Generic)

```cpp
int low = 0, res = INT_MIN;
unordered_map<char,int> freq;       // or whatever info structure fits
for (int high = 0; high < n; high++) {
    freq[s[high]]++;
    while (/* info invalid, e.g. freq.size() > K */) {
        freq[s[low]]--;
        if (freq[s[low]] == 0) freq.erase(s[low]);
        low++;
    }
    if (/* exact condition met, e.g. freq.size() == K */)
        res = max(res, high - low + 1);
}
return res;
```

### 8.3 Variable — Minimum Window (Generic)

```cpp
int low = 0, res = INT_MAX, sum = 0;
for (int high = 0; high < n; high++) {
    sum += arr[high];
    while (sum >= target) {                 // info valid
        res = min(res, high - low + 1);      // record BEFORE shrinking
        sum -= arr[low];
        low++;
    }
}
return (res == INT_MAX) ? 0 : res;
```

### 8.4 Exactly K Distinct Template

```cpp
unordered_map<char,int> freq;
int low = 0, res = -1;
for (int high = 0; high < n; high++) {
    freq[s[high]]++;
    while (freq.size() > K) {
        freq[s[low]]--;
        if (freq[s[low]] == 0) freq.erase(s[low]);
        low++;
    }
    if (freq.size() == K)               // the "exact" check
        res = max(res, high - low + 1);
}
return res;
```

### 8.5 At Most K Distinct Template

```cpp
unordered_map<int,int> freq;
int low = 0, res = 0;
for (int high = 0; high < n; high++) {
    freq[arr[high]]++;
    while (freq.size() > K) {
        freq[arr[low]]--;
        if (freq[arr[low]] == 0) freq.erase(arr[low]);
        low++;
    }
    res = max(res, high - low + 1);     // no "if" needed — already ≤ K here
}
return res;
```

### 8.6 Longest Window Template (No Fixed K — "K = window size itself" trick)

Used for problems like "longest substring with all unique characters," where there's no explicit K — instead, the constraint is derived from the window's own length.

```cpp
unordered_map<char,int> freq;
int low = 0, res = 0;
for (int high = 0; high < n; high++) {
    freq[s[high]]++;
    int k = high - low + 1;             // K is recomputed every time — it's dynamic!
    while (freq.size() < k) {           // note: LESS THAN here, not greater than
        freq[s[low]]--;
        if (freq[s[low]] == 0) freq.erase(s[low]);
        low++;
        k = high - low + 1;             // recompute K since the window shrank too
    }
    res = max(res, high - low + 1);
}
return res;
```

### 8.7 Minimum Window (Substring Matching) Template

Used when you must return the *actual substring* (not just length) that contains all characters of another string `T`, including duplicate counts.

```cpp
vector<int> have(256, 0), need(256, 0);
for (char c : t) need[c]++;

bool isValid(vector<int>& have, vector<int>& need) {
    for (int i = 0; i < 256; i++)
        if (have[i] < need[i]) return false;
    return true;
}

int low = 0, res = INT_MAX, start = -1;
for (int high = 0; high < n; high++) {
    have[s[high]]++;
    while (isValid(have, need)) {                 // info VALID
        int len = high - low + 1;
        if (res > len) { res = len; start = low; } // record BEFORE shrinking
        have[s[low]]--;
        low++;
    }
}
return (res == INT_MAX) ? "" : s.substr(start, res);
```

---

## 9. Every Question Covered in the Lectures

### Question 1 — Maximum Sum Subarray of Size K *(Fixed Window)*

**Problem Statement:** Given an array, find the maximum sum among all subarrays of a given fixed size `K`.

**Intuition:** Brute force would extract every subarray of size `K` and sum it independently — wasteful, since consecutive subarrays overlap almost entirely. Instead, slide one window of fixed size `K` across the array, updating the sum incrementally.

**Why Sliding Window works:** It's an array question, it explicitly asks for a subarray, and we're finding a **maximum sum** — all three flowchart checks pass. Since the size `K` is explicitly fixed, it's a **Fixed Window**.

**Pattern Type:** Fixed Window.

**Dry Run:** Array = `[100, 200, 300, 400]`, `K = 2`.
| Window | Sum |
|---|---|
| `(100, 200)` | `100 + 200 = 300` (computed directly — first window) |
| `(200, 300)` | `300 − 100 + 300 = 500` |
| `(300, 400)` | `500 − 200 + 400 = 700` |

Maximum = **700**.

**Final Approach:**
```cpp
class Solution {
public:
    int maxSubarraySum(vector<int>& arr, int k) {
        int low = 0;
        int high = k - 1;
        int sum = 0;
        int res = INT_MIN;
        for (int i = low; i <= high; i++) {
            sum += arr[i];
        }
        while (high < arr.size()) {
            res = max(res, sum);
            low++;
            high++;
            if (high == arr.size()) {
                break;
            }
            sum = sum - arr[low - 1];
            sum = sum + arr[high];
        }
        return res;
    }
};
```

**Key Observation:** Each slide is just `sum − leaving_element + entering_element` — never recompute the whole sum. This is the foundational trick every other Fixed Window question reuses.

---

### Question 2 — Minimum Size Subarray Sum *(Variable — Minimum Window)*

**Problem Statement:** Given an array of positive integers and a `target`, return the length of the **shortest** subarray whose sum is `≥ target`. Return 0 if no such subarray exists.

**Intuition — Hiring/Firing analogy:** Imagine hiring people (`high++`) one at a time until the combined "work" (sum) meets the target. Once it does, start firing the earliest-hired person (`low++`, FIFO) to check if fewer people can still do the job. Keep firing while it still works; the moment firing breaks it, go back to hiring.

**Why Sliding Window works:** Array question ✅, subarray ✅, asking for **minimum length** subject to a sum constraint ✅. No fixed size is given, so it's **Variable**. Because the condition is "sum ≥ target," this is a **Minimum Window** problem (shrink while valid, record before shrinking).

**Pattern Type:** Variable — Minimum Window.

**Dry Run:** Array = `[1, 2, 4, 4]`, `target = 4`.
| Action | low | high | sum | Valid? | Recorded length |
|---|---|---|---|---|---|
| hire 1 | 0 | 0 | 1 | No | — |
| hire 2 | 0 | 1 | 3 | No | — |
| hire 4 | 0 | 2 | 7 | **Yes** | 3 |
| fire 1 | 1 | 2 | 6 | Yes | 2 |
| fire 2 | 2 | 2 | 4 | Yes | **1** |
| fire 4 | 3 | 2 | 0 | No | — |
| hire 4 | 3 | 3 | 4 | Yes | 1 (no improvement) |
| fire 4 | 4 | 3 | 0 | No | — |
| array exhausted | | | | | |

Minimum length = **1**.

**Final Approach:**
```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int low = 0;
        int high = 0;
        int sum = 0;
        int minLength = INT_MAX;
        for (high = 0; high < nums.size(); high++) {
            sum += nums[high];
            while (sum >= target) {
                minLength = min(minLength, high - low + 1);
                sum = sum - nums[low];
                low++;
            }
        }
        return (minLength == INT_MAX) ? 0 : minLength;
    }
};
```

**Key Observation:** This is the textbook **Minimum Window** shape: the `while` condition checks for *validity* (`sum >= target`), and the result is recorded **inside** that loop, right before each shrink — not after.

---

### Question 3 — Longest Substring with K Distinct Characters *(Variable — "Exactly K")*

**Problem Statement:** Given a string and an integer `K`, find the length of the longest substring containing **exactly** `K` distinct characters.

**Intuition:** Track character frequencies in a hashmap as the window slides. The hashmap's *size* (number of keys) tells you the count of distinct characters currently in the window.

**Why Sliding Window works:** String ✅, substring ✅, "longest" + "exactly K" ✅. No fixed length given → Variable Window. Since we want the longest, and the constraint can be framed as "distinct ≤ K" (with an exact check on top), this uses the **Maximum Window** template.

**Pattern Type:** Variable — Maximum Window, with an "exactly K" exact-match check.

**Dry Run:** String = `"AAB"`, `K = 2`.
| high | char | freq map | distinct | action |
|---|---|---|---|---|
| 0 | A | {A:1} | 1 | size < K → no shrink; size ≠ K → don't record |
| 1 | A | {A:2} | 1 | size < K → no shrink; size ≠ K → don't record |
| 2 | B | {A:2, B:1} | 2 | size == K → record length `3` |

Answer = **3**.

**Final Approach:**
```cpp
class Solution {
public:
    int longestKSubstr(string &s, int k) {
        unordered_map<char, int> freq;
        int low = 0;
        int maxLen = -1;
        for (int high = 0; high < s.size(); high++) {
            freq[s[high]]++;
            while (freq.size() > k) {
                freq[s[low]]--;
                if (freq[s[low]] == 0) {
                    freq.erase(s[low]);
                }
                low++;
            }
            if (freq.size() == k) {
                maxLen = max(maxLen, high - low + 1);
            }
        }
        return maxLen;
    }
};
```

**Key Observation:** Don't shrink `low` when `freq.size() < K` — shrinking can only ever *decrease* the distinct count further, moving you away from `K`, never towards it. You only shrink when `freq.size() > K`. **Also:** when a frequency hits zero after decrementing, you must `erase()` it from the map — leaving a zero-frequency key inflates `.size()` incorrectly.

---

### Question 4 — Fruits into Baskets *(Variable — "At Most K")*

**Problem Statement:** Fruit trees are arranged in a row; each tree has one type of fruit. You may collect fruit only while moving left to right, and your basket can hold **at most 2 distinct types** of fruit. Find the maximum number of fruits you can collect.

**Intuition:** Translated into Sliding Window language: *"Find the longest subarray with at most 2 distinct values."* It's the exact same shape as Question 3, except the bound is "at most" instead of "exactly," so the extra `if` check is unnecessary.

**Why Sliding Window works:** Array (of fruit types) ✅, contiguous walk (subarray) ✅, "maximum count" subject to "at most 2 distinct" ✅. Variable + Maximum Window.

**Pattern Type:** Variable — Maximum Window, "At Most K" (K = 2).

**Dry Run:** Fruits = `[0, 1, 2, 0]`. Window `(0,1)` → 2 distinct, length 2. Extending to include `2` pushes distinct to 3 → must shrink. Best valid run ends up being length 3 (final answer depends on full array, but the mechanics mirror Q3 without an exact-match check).

**Final Approach:**
```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        unordered_map<int, int> freq;
        int low = 0;
        int maxLen = 0;
        for (int high = 0; high < fruits.size(); high++) {
            freq[fruits[high]]++;
            while (freq.size() > 2) {
                freq[fruits[low]]--;
                if (freq[fruits[low]] == 0) {
                    freq.erase(fruits[low]);
                }
                low++;
            }
            maxLen = max(maxLen, high - low + 1);
        }
        return maxLen;
    }
};
```

**Key Observation:** "At most K" is actually *simpler* to code than "exactly K" — once the `while` loop ends, the window is guaranteed valid (`≤ K`), so you can record the result unconditionally, with no `if` needed.

---

### Question 5 — Longest Substring Without Repeating Characters *(Variable — Dynamic K)*

**Problem Statement:** Find the length of the longest substring with **no repeating characters** (i.e., every character in it must be unique).

**Intuition:** Without a given `K`, how do we know if a window is "all-unique"? Trick: a window of length `L` has all-unique characters **if and only if** its hashmap size also equals `L`. So `K` here isn't fixed — it **is the window's own current length**, recalculated every time the window changes.

**Why Sliding Window works:** String ✅, substring ✅, "longest" ✅. No fixed size → Variable Window.

**Pattern Type:** Variable — Maximum Window, but with a self-referential (dynamic) `K`.

**Dry Run:** `"A A B"` (indices 0,1,2):
| high | char | freq size | window size (K) | shrink? |
|---|---|---|---|---|
| 0 | A | 1 | 1 | size == K, fine |
| 1 | A | 1 | 2 | size(1) < K(2) → shrink low until they match → low becomes 1, K becomes 1, size 1 → matches |
| 2 | B | 2 | 2 | size == K, length 2 |

Final answer for this example = **2** (`"A B"`).

**Final Approach:**
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> freq;
        int low = 0;
        int maxLen = 0;
        for (int high = 0; high < s.size(); high++) {
            freq[s[high]]++;
            int k = high - low + 1;
            while (freq.size() < k) {
                freq[s[low]]--;
                if (freq[s[low]] == 0) {
                    freq.erase(s[low]);
                }
                low++;
                k = high - low + 1;
            }
            maxLen = max(maxLen, high - low + 1);
        }
        return maxLen;
    }
};
```

**Key Observation — the most important interview lesson in this whole pattern:** Don't blindly memorize "shrink when greater than K." In every earlier question, `K` was fixed, so shrinking could only ever *decrease* `freq.size()`, never `K` — meaning shrinking only helps when you're *above* `K`. Here, `K` itself shrinks alongside `low`, so shrinking can help even when `freq.size() < K`, because both numbers are moving and might converge. **Always reason about the actual relationship, don't pattern-match blindly.**

---

### Question 6 — Longest Repeating Character Replacement *(Variable — Maximum Window, Hard)*

**Problem Statement:** Given a string and an integer `K`, you may change any character to any other character, but at most `K` times. Find the length of the longest substring you can make consist of a single repeated character using at most `K` changes.

**Intuition — "majority + minority" thinking:** Think like a human, not a computer. Inside any window, one character appears most often (the **majority** character). The smartest move is to leave the majority character untouched and only change the **minority** characters — since there are fewer of them, you need fewer operations. (E.g., if a window is 70% one character and 30% everything else, changing the 30% costs far less than changing the 70%.)

So: `characters_to_change = window_length − count_of_most_frequent_character`. If that number is `≤ K`, the window is achievable; otherwise, it's not.

**Why Sliding Window works:** String ✅, substring ✅, "longest" with a transformation-budget constraint ✅. Variable + Maximum Window — the constraint "changes needed ≤ K" plays the role of the upper-bound condition.

**Pattern Type:** Variable — Maximum Window.

**Dry Run:** Window contains `A, A, B` with `K = 1`. Length = 3, max frequency (A) = 2. Difference = `3 − 2 = 1`. Since `1 ≤ K(=1)`, this window is valid — change the single `B` to `A`. If a `C` were also added (`A,A,B,C`), difference becomes `4 − 2 = 2 > K(=1)` → invalid → must shrink.

**Final Approach:**
```cpp
class Solution {
public:
    int characterReplacement(string s, int k) {
        unordered_map<char, int> freq;
        int low = 0;
        int maxFreq = 0;
        int maxLen = 0;
        for (int high = 0; high < s.size(); high++) {
            freq[s[high]]++;
            maxFreq = max(maxFreq, freq[s[high]]);
            while ((high - low + 1) - maxFreq > k) {
                freq[s[low]]--;
                low++;
            }
            maxLen = max(maxLen, high - low + 1);
        }
        return maxLen;
    }
};
```

**Key Observation:** The "information" being tracked here isn't just a frequency map — it's a **derived quantity**: `window_length − maxFrequency`. This is a great example of how the *same* shrink-while-invalid / record-after template applies, even when the validity condition is more elaborate than a simple count comparison.

---

### Question 7 — Minimum Window Substring *(Variable — Minimum Window, Hard)*

**Problem Statement:** Given strings `S` and `T`, find the smallest substring of `S` that contains **every character of `T`**, including matching the required frequency of duplicates (order doesn't matter). Return the substring itself (not just its length).

**Intuition:** Build a `need` array (frequency of every character required, from `T`) and a `have` array (frequency of every character currently in the window). A window is "correct" exactly when, for every character, `have[char] ≥ need[char]`.

**Why Sliding Window works:** String ✅, substring ✅, "minimum window satisfying a containment condition" ✅. Since the condition is "have ≥ need" (a `≥`-style constraint), this is a **Minimum Window** problem.

**Pattern Type:** Variable — Minimum Window (the hardest variant — tracking two parallel frequency arrays and a custom validity check, plus returning the actual substring, not just a length).

**Dry Run (concept):** If `T = "ABC"`, any candidate window in `S` must contain at least one `A`, one `B`, and one `C` (anything else is allowed alongside them). As `high` expands the window, you check the `have` vs `need` arrays. The moment the window is correct, record `(length, start)`, then immediately try shrinking from `low` to see if a smaller correct window still exists — exactly mirroring Question 2's logic, just with a more complex "valid" check.

**Final Approach:**
```cpp
class Solution {
public:
    bool fun(vector<int>& have, vector<int>& need) {
        for (int i = 0; i < 256; i++) {
            if (have[i] < need[i])
                return false;
        }
        return true;
    }
    string minWindow(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<int> have(256, 0);
        vector<int> need(256, 0);
        int i;
        if (n < m)
            return "";
        for (i = 0; i < m; i++)
            need[t[i]]++;

        int low = 0, high = 0;
        int res = INT_MAX;
        int start = -1;
        for (high = 0; high < n; high++) {
            have[s[high]]++;

            while (fun(have, need)) {
                int len = high - low + 1;
                if (res > len) {
                    res = len;
                    start = low;
                }
                have[s[low]]--;
                low++;
            }
        }
        if (res == INT_MAX)
            return "";
        return s.substr(start, res);
    }
};
```

**Key Observation:** This question looks intimidating (it's a LeetCode Hard), but it is the **exact same Minimum Window template** as Question 2 — only the "is this window valid?" check is more elaborate (comparing two 256-length arrays instead of a single sum). Once you trust the template, you don't need to memorize this as a separate algorithm — you derive it. Also note: because the answer must be a **substring**, track the window's `start` index (`= low` at the moment of recording) instead of just the length, then use it with `substr(start, length)` at the end.

---

### Bonus / Practice Question Mentioned (not walked through in code)

**Max Consecutive Ones III** — explicitly called out as an exercise: it is essentially the array version of Question 6 (Longest Repeating Character Replacement) — "flip at most K zeros to ones, find the longest run of ones." If you understand Q6's majority/minority logic, this is a direct, simpler application of the same Maximum Window template. Worth solving independently as a self-check.

---

## 10. Common Mistakes & Interview Tips

- ❌ **Confusing Subsequence with Subarray/Substring.** If elements don't need to be contiguous, Sliding Window will give wrong answers. Always check this first.
- ❌ **Forgetting to erase zero-frequency keys from a hashmap.** A key with frequency `0` still counts toward `.size()` in most languages — always `erase()`/remove it, or your distinct-count logic silently breaks.
- ❌ **Trying to apply Sliding Window to Linked Lists.** It almost never works cleanly — recognize this early and pivot.
- ❌ **Memorizing "shrink when greater than K" as a universal rule.** It is *not* universal (see Question 5) — always derive the shrink condition from what actually makes the information move toward validity.
- ❌ **Mixing up the Maximum-Window and Minimum-Window templates.** Maximum: shrink while invalid, record after. Minimum: shrink while valid, record during/before. Getting this backward is the single most common bug in variable-window code.
- ❌ **Off-by-one errors with `high - low + 1`.** This is the formula for window length — always inclusive on both ends.
- ❌ **Not handling the boundary check in Fixed Window** (`if (high == n) break;`) before accessing `array[high]` — this causes out-of-bounds errors, especially for small `K` or small arrays.
- ✅ **Always state the 4 steps out loud in an interview:** (1) Is this Sliding Window? (2) Fixed or Variable? (3) What's the window's "information"? (4) How does that information update when the window slides? This signals strong structured thinking, independent of whether you instantly recall the exact code.
- ✅ **For "exactly K" problems, re-use the "at most K" shrink logic** and simply add an `if (== K)` check before recording — don't write new shrink logic from scratch.
- ✅ **Time complexity of any two-pointer Sliding Window is O(N), never O(N²)** — even with a `while` nested inside a `for`, because `low` can advance at most N times total across the *entire* run, not per iteration of `high`. Be ready to explain this clearly if asked.

---

## 11. Quick Revision Sheet (1-Page Summary)

**Applies to:** Array / String only (not Linked List) + Subarray/Substring (continuous) + asking for Max/Min/Longest/Shortest/Sum/Count/Average/At Most K/At Least K/Exactly K.

**Window length formula:** `high - low + 1`

**Fixed Window** (size `K` given):
```
low = 0, high = K-1 → compute first window's info manually
while high < n:
    record(info)
    remove(low); low++
    high++; if high == n: break
    add(high)
```

**Variable Window — Maximum/Longest** (condition is "≤ K" style — at most K, exactly K):
```
for high in 0..n:
    add(high) to info
    while info invalid (too big):     shrink: remove(low); low++
    if info meets exact condition:    res = max(res, high-low+1)
```

**Variable Window — Minimum/Shortest** (condition is "≥ K" style — at least K):
```
for high in 0..n:
    add(high) to info
    while info valid (already enough):
        res = min(res, high-low+1)     ← record BEFORE shrinking
        remove(low); low++
```

**Always check:**
- distinct values → use a hashmap, `.size()` = distinct count, `erase()` when frequency hits 0
- "all unique" with no given K → use `K = high - low + 1` (dynamic K), shrink while `freq.size() < K`
- "majority + minority" style (replacement budget) → track `maxFreq`, validity = `(window length - maxFreq) ≤ K`
- need actual substring, not length → track `start = low` at the moment you record the best answer

---

## 12. Cheat Sheet of All Sliding Window Patterns

| Pattern Name | Window Type | Shrink Condition | Record Condition | Example Question |
|---|---|---|---|---|
| Fixed-size aggregate (sum/max/min) | Fixed | N/A (always slides by 1) | Every step | Max Sum Subarray of Size K |
| At Most K Distinct | Variable — Max | `distinct > K` | Always (after shrink loop) | Fruits into Baskets |
| Exactly K Distinct | Variable — Max | `distinct > K` | `distinct == K` | Longest Substring with K Distinct Characters |
| All Unique (dynamic K) | Variable — Max | `distinct < window_size` | Always (after shrink loop) | Longest Substring Without Repeating Characters |
| Replacement Budget (majority trick) | Variable — Max | `(length - maxFreq) > K` | Always (after shrink loop) | Longest Repeating Character Replacement |
| Minimum length meeting a sum/condition | Variable — Min | `info` already valid (≥ target) | Every time before shrinking | Minimum Size Subarray Sum |
| Minimum window containing all of T | Variable — Min | `have ≥ need` for all chars (valid) | Every time before shrinking | Minimum Window Substring |

**One-line memory hook:**
> *"Longest → shrink when wrong, write when right (after). Shortest → write when right (before), then shrink anyway to try for less."*

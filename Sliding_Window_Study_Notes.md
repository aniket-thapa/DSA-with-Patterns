# Sliding Window Pattern — Complete Study Notes

> Built from the full lecture series (Intro → Fixed Window → Variable Max Window → Variable Min Window → Revision → Minimum Window Substring) and all 7 problems on the pattern sheet.

---

## 1. Pattern Overview

### What is a Sliding Window?

A **window** is just a *contiguous segment* of an array or string, marked by two pointers:

- **`low`** — start of the window
- **`high`** — end of the window

"**Sliding**" means this window can move and resize itself, but only in one direction:

| Action | Code | Effect |
|---|---|---|
| Expand | `high++` | distance between `low` and `high` grows → window gets **bigger** |
| Shrink | `low++` | distance between `low` and `high` shrinks → window gets **smaller** |

The window only ever moves **rightward** — `low` and `high` never go backward. That's the entire mechanical idea; everything else in this pattern is about *when* to grow and *when* to shrink.

### Why Use It?

The naive (brute-force) way to solve "find something about every subarray/substring" is to **re-extract and re-compute** the information (sum, frequency, count, etc.) for every possible window from scratch. That's wasteful.

**The bank-account analogy:** If you have ₹1,00,000 in the bank, spend ₹100, and someone deposits ₹50, the bank doesn't recount your entire balance from zero. It just does `100000 - 100 + 50`. A sliding window does the exact same thing — when the window slides by one position, most of the elements are unchanged (still inside the window). Only **one element leaves** (at the old `low`) and **one element enters** (at the new `high`). So you update the existing information instead of recomputing it:

```
new_info = old_info  -  (element leaving at low)  +  (element entering at high)
```

### Time Complexity Benefit

| Approach | Time Complexity |
|---|---|
| Brute force (recompute every window from scratch) | O(N·K) or O(N²) |
| Sliding Window (incremental update) | **O(N)** |

`high` traverses the array once, and `low` also traverses the array (forward only) over the entire run — never more than `n` total steps for each pointer, even though `low`'s movement is "hidden" inside a `while` loop. Space stays **O(1)** (or O(26)/O(256) for character frequency, which is treated as constant).

---

## 2. Pattern Recognition (The Flowchart)

Before picking any algorithm, run the question through this 3-check flowchart. If all three pass, Sliding Window applies with very high confidence (~90%+).

### Check 1 — Data structure
- ✅ Array or **String** (a string is just an array of characters)
- ❌ **Never** applies to a Linked List (in ~99.9% of cases)

### Check 2 — Subarray / Substring, NOT Subsequence
- **Subarray / Substring** = a *continuous* chunk of the array/string. Sliding Window needs continuity to work, because it only adds/removes elements from the two ends.
- **Subsequence** = elements picked in order but **not necessarily continuous** (you can skip elements). This is a common trap — seeing "subsequence" and still reaching for Sliding Window. **Subsequence problems are usually DP, not Sliding Window.**

### Check 3 — What is the question actually asking for?
The question is almost always asking for one of these combinations:

| Maximum | Minimum | Longest | Shortest | Sum |
|---|---|---|---|---|
| Count | Average | At most K | At least K | Exactly K |

If Checks 1 and 2 are true, and the answer being asked for is one of the above — it's Sliding Window.

### Quick Recognition Table

| Question says... | Likely window type |
|---|---|
| "subarray/substring **of size K**" | Fixed Window |
| "**longest** / **at most K** / no explicit size" | Variable — **Maximum** Window |
| "**shortest** / **minimum length** / **at least K**" | Variable — **Minimum** Window |
| "subsequence" anywhere | ❌ Not Sliding Window |

### Instructor's confidence rule
> "If a question is a string/array problem, talks about a subarray/substring, and asks for max/min/longest/shortest/sum/count/average/atmost-K/atleast-K/exactly-K — start with Sliding Window in an interview. Don't waste time guessing between Graph/DP/Greedy first. Worst case, you discover in a minute that it doesn't fit and pivot — but starting here is the highest-probability bet."

Also: a question doesn't need to use the literal word "subarray." Story-style questions (e.g., "fruit trees on a farm," "people standing in a line") are often Sliding Window in disguise. **Translate the question into plain language first** — "What am I really being asked to find about a continuous segment?" — before deciding it doesn't fit.

---

## 3. Types of Sliding Window

### 3.1 Fixed Size Window
Used when the problem **explicitly gives you a size K** (e.g., "subarray of size K", "window of length 3"). The window slides but never changes size — one element leaves from `low`, one enters at `high`, every single step.

- `low` starts at `0`
- `high` starts at `K - 1`
- Both move together; window size stays exactly `K` forever.

### 3.2 Variable Size Window
Used when **no size is given** — the question only describes a *property* the window must satisfy (longest, shortest, sum equal to/at most/at least something). Both pointers start at `0`, and the window grows/shrinks based on whether its current content is "valid" or "invalid."

Variable windows split into **two mirror-image sub-types** — this is the single most important insight in the whole pattern, and the one most people get wrong:

#### (a) Variable — Maximum / Longest type
- The condition is always of the form **`info ≤ something`** (at most K distinct, sum ≤ target, no duplicates, etc.)
- *Why always ≤, never ≥?* Because "longest window with sum **greater than** K" makes no sense for positive numbers — you'd just take the whole array (adding more elements only increases the sum further). A "longest, with an upper-bound condition" is the only version of this question that's actually solvable.

#### (b) Variable — Minimum / Shortest type
- The condition is always of the form **`info ≥ something`** (sum ≥ target, contains all characters of T, etc.)
- *Why always ≥, never ≤?* Because "shortest window with sum **less than** K" is trivial — a single element already satisfies it, so the answer is always 1 (or the question makes no sense). Only a "shortest, with a lower-bound condition" is meaningful.

### The Big Insight: Max and Min Are Mirror Images

Many learners assume the same shrink-logic ("shrink while the window looks wrong") works for both. **It doesn't — the logic flips completely:**

| | Maximum Window | Minimum Window |
|---|---|---|
| Shrink `low` while... | the window is **INVALID** | the window is **VALID** |
| Record the result... | **after** the shrink loop ends (window just became valid) | **inside** the shrink loop, every time it's valid (before shrinking further) |
| Intuition | Push `high` out as far as possible; only pull back when forced | Keep pulling `low` in for as long as it still works, to find something even smaller |

**The Hiring & Firing analogy (used for Minimum windows):**
> A company doesn't know how many people it needs. It keeps *hiring* (`high++`) until the work gets done. The moment work is happening, it records the headcount, then starts *firing* people from the front (`low++`, in hire order — first-in-first-out) to see if fewer people can still do the job. It keeps firing — and keeps recording smaller counts — until the work stops. Then it hires again. This loop of "validate → record → try to shrink → repeat" is exactly the Minimum Window template.

---

## 4. Universal Problem-Solving Flow

Every sliding window problem — easy or hard — is solved with the same **4 steps**. Nothing in the entire pattern falls outside these steps.

| Step | Question to ask | What you do |
|---|---|---|
| **1. Identify the Pattern** | Does this qualify for Sliding Window? | Run the flowchart from Section 2. |
| **2. Find the Window Type** | Fixed size given? Or variable — and if variable, is it Max-type or Min-type? | Decide `low/high` starting positions and shrink direction. |
| **3. Find the Starting Window's Information** | What does this window "mean"? (sum? frequency map? count of distinct elements?) | Compute the info for the very first window using a simple loop. |
| **4. Slide & Update Information** | When the window moves, how does the info change? | Add the new `high` element, remove the old `low` element — **incrementally**, never recompute from scratch. |

### Checklist before writing a single line of code
1. Array/String? Subarray/Substring (not subsequence)? Asking for max/min/longest/shortest/sum/count/avg/atmost/atleast/exactly? → **Sliding Window applies.**
2. Is a size `K` explicitly given? → **Fixed.** Otherwise → **Variable.**
3. If Variable: is the condition an upper bound (≤, "at most", "no more than")? → **Max-type.** Is it a lower bound (≥, "at least", "must contain")? → **Min-type.**
4. What single piece of information defines "valid" for this window? (a sum, a hashmap size, a max-frequency, a containment check…)
5. How do I update that information in O(1) when `high` enters or `low` leaves?

### "Think Like a Human, Not a Computer"
Before writing any loop, manually trace 2–3 windows by hand on paper. This is how the instructor consistently de-mystifies "hard" questions:
- For sums: don't re-add from scratch — subtract the leaving element, add the entering one.
- For "longest substring with K replacements allowed" (the BJP/majority-party analogy): the cheapest way to make a window uniform is to **keep the most frequent character as-is** and only change the minority characters. So `characters_to_change = window_length − max_frequency`. Checking this single number tells you instantly whether the window is achievable within the allowed K changes.

---

## 5. Templates

> All templates use C++; the same 4-step logic translates directly to any language.

### 5.1 Fixed Window Template

```cpp
int low = 0, high = k - 1;
int sum = 0;

// Step 3: compute the FIRST window's information directly
for (int i = low; i <= high; i++) sum += arr[i];

int res = sum;

// Step 4: slide one step at a time
while (high < n) {
    res = max(res, sum);     // record current window's info

    low++;
    high++;
    if (high == n) break;    // guard: no element left to bring in

    sum = sum - arr[low - 1] + arr[high];  // remove old `low-1`, add new `high`
}
return res;
```

**Line-by-line:**
- `low = 0, high = k - 1` → the window must start at the array's beginning and span exactly `K` elements.
- First `for` loop → builds the only window we can't update incrementally (there's nothing "before" it).
- `while (high < n)` → keeps sliding until `high` would run off the array.
- `res = max(res, sum)` → record the *current* window before moving on.
- `low++; high++` → slide the window one step right (size stays `K`).
- `if (high == n) break;` → after incrementing, `high` might now be out of bounds — stop before touching `arr[high]`.
- `sum = sum - arr[low-1] + arr[high]` → the incremental update: the element that just left is at index `low - 1` (since `low` was already incremented); the element that just entered is at `high`.

### 5.2 Variable Window — Maximum Template

```cpp
int low = 0, res = 0;          // or INT_MIN if 0 isn't a valid baseline
// `info` = whatever you're tracking: int sum = 0; or unordered_map<char,int> freq;

for (int high = 0; high < n; high++) {
    // Step 1: include `high` in the information
    freq[s[high]]++;

    // Step 2: while the window VIOLATES the upper-bound condition, shrink from low
    while (/* info is invalid, e.g. freq.size() > K */) {
        freq[s[low]]--;
        if (freq[s[low]] == 0) freq.erase(s[low]);
        low++;
    }

    // Step 3: window is now guaranteed valid — try to record it
    res = max(res, high - low + 1);   // for "at most K" / "no duplicates" style problems
    // for "exactly K" style problems, wrap this line in:  if (freq.size() == K)
}
return res;
```

**Why the result is recorded *after* the `while`:** by the time the `while` loop exits, the window is guaranteed to no longer violate the upper bound — so it's safe to record. For "exactly K"-style questions, a window can be valid-but-not-yet-`==K` (still smaller than K distinct elements) — in that case wrap the recording line in an `if` so you only count windows that hit the exact target.

### 5.3 Variable Window — Minimum Template

```cpp
int low = 0, res = INT_MAX;
// `info` = int sum = 0; or two frequency arrays for containment checks

for (int high = 0; high < n; high++) {
    // Step 1: include `high` in the information
    sum += arr[high];

    // Step 2: while the window SATISFIES the lower-bound condition,
    //         it's valid right now — record it, then try to shrink further
    while (/* info is valid, e.g. sum >= target */) {
        res = min(res, high - low + 1);

        sum -= arr[low];
        low++;
    }
}
return (res == INT_MAX) ? 0 : res;
```

**Why the result is recorded *inside* the `while`:** the loop only runs while the window is valid — meaning right now is exactly the moment to capture the length, before you shrink and possibly break validity. This is the reverse of the Maximum template, and is the #1 thing beginners get backwards.

### 5.4 Max vs Min — Side by Side

| Aspect | **Maximum** Window | **Minimum** Window |
|---|---|---|
| Typical condition | `info ≤ K` (at most / no more than) | `info ≥ K` (at least / must contain) |
| `res` initial value | `0` or `INT_MIN` | `INT_MAX` |
| Inner `while` runs while... | info is **invalid** | info is **valid** |
| What happens inside the `while` | shrink only (remove `low`, `low++`) | **record result first**, then shrink |
| Where the final record happens | **after** the `while` (outside it) | **inside** the `while` (every iteration it runs) |
| If `while` never runs | window was already valid; record it anyway | window never became valid this round; nothing to record |
| Empty-result handling | usually `0` is a safe default | check for leftover `INT_MAX` → return `0` |

---

## 6. Important Patterns & Tricks

### Frequency tracking: array vs hashmap
- For character-frequency questions, an **array of size 256** (covers all ASCII characters, including punctuation/space) is faster and simpler than a hashmap — no hashing overhead, and finding the **maximum frequency** (needed for the Character Replacement problem) is just a linear scan over a fixed-size array, which is O(1) since 256 is constant.
- If the alphabet is guaranteed lowercase-only, a size-26 array also works (and is what's used as the constant-space justification in complexity analysis).

### The "erase when zero" rule (hashmaps only)
Decrementing a hashmap entry to `0` does **not** remove the key. If you rely on `map.size()` to count "distinct elements currently in the window," a zero-frequency leftover key will be counted incorrectly. **Always check `if (freq[x] == 0) freq.erase(x);` after decrementing.** This issue doesn't apply to plain frequency *arrays* — there you just compare the value to `0` directly, no removal needed.

### Why it's O(N), not O(N²)
A `while` loop sitting inside a `for` loop looks like nested iteration, but it isn't: `low` never moves past `high`, and across the *entire* run of the algorithm, `low` advances at most `n` times in total — the inner `while` doesn't reset and restart `low` from `0` on every outer iteration. So total work is `O(n) [for high] + O(n) [for low, summed across all iterations] = O(n)`.

### The incremental-update rule
Never recompute sum/frequency/average from scratch when the window slides. Always derive the new value from the old one:
```
new_sum = old_sum - (element leaving) + (element entering)
```

### `INT_MAX` / `INT_MIN` initialization rule
- Looking for a **minimum** → start `res = INT_MAX` (any real answer found will be smaller and will naturally overwrite it).
- Looking for a **maximum** → start `res = INT_MIN` (or `0` when lengths can't be negative).

### The "majority character" trick (Character Replacement family)
For "longest substring achievable with K replacements" problems:
- `chars_to_change = window_length − max_frequency_in_window`
- A window is achievable within budget `K` exactly when `chars_to_change ≤ K`.
- `maxFreq` can either be **recomputed** by scanning the fixed-size frequency array after every shrink (simple, still O(1) per scan since the array size is constant), **or** allowed to go slightly **stale** (never decreased even as you shrink). The stale version is a legitimate, widely-used optimization: since the algorithm only records `high - low + 1` and `low` only advances when forced, the window length reported can never exceed what was genuinely achievable — so a stale `maxFreq` never produces a wrong (too-large) answer, it only occasionally delays a shrink by one step.

### Edge cases & gotchas
- **Out-of-bounds after sliding:** in a Fixed window, always check `if (high == n) break;` right after `high++`, before indexing `arr[high]`.
- **No valid window exists:** for Minimum-type problems, if `res` is still `INT_MAX` at the end, return `0` (or `""` for substring problems) instead of the sentinel value.
- **Window smaller than K:** in "exactly K" problems, a window with fewer than K distinct elements is *not* invalid (no need to shrink) — it just isn't recorded yet. Don't shrink a window just because it hasn't reached the target; only shrink when it has *exceeded* an upper bound.
- **Positive numbers assumption:** the "≤ for Max / ≥ for Min" rule assumes non-negative array values (so that adding elements is monotonically non-decreasing). With negative numbers present, sliding window's monotonic-sum assumption breaks down and a different approach (e.g., prefix sums) may be needed.

### Common mistakes
1. **Treating "subsequence" as "subarray/substring."** Sliding Window requires continuity — subsequences need a different approach (commonly DP).
2. **Using the wrong shrink direction for Min-type problems.** ("Shrink while invalid" is correct for Max, but for Min you shrink **while valid**.) This single mix-up breaks half of all variable-window problems.
3. **Forgetting to `erase()` zero-frequency keys** from a hashmap, silently inflating `map.size()`.
4. **Recomputing sum/frequency from scratch** on every slide instead of updating incrementally — defeats the purpose of the pattern and often turns O(N) into O(N·K).
5. **Not handling the "no answer found" sentinel** (`INT_MAX`/`INT_MIN` leaking into the final return value).

---

## 7. Questions Breakdown

### Q1 — Maximum Sum Subarray of Size K (Fixed Window)
| | |
|---|---|
| **Problem** | Given an array and integer `K`, find the maximum sum among all subarrays of size exactly `K`. |
| **Key observation** | The window size is explicitly fixed at `K` — every subarray considered must be exactly that size. |
| **Why Sliding Window works** | Consecutive size-`K` windows overlap in `K-1` elements; only one element leaves the front and one enters the back each slide. |
| **Approach** | Build the sum of the first window `[0, K-1]` directly. Then repeatedly: record the max, slide both pointers forward, and update the sum by subtracting the outgoing element and adding the incoming one. Stop once `high` runs out of bounds. |
| **Pattern used** | Fixed Window |
| **Takeaway** | Whenever the window size is explicitly given, default immediately to the Fixed Window template — it's the simplest version of the pattern. |

```cpp
int maxSubarraySum(vector<int>& arr, int k) {
    int low = 0, high = k - 1, sum = 0, res = INT_MIN;
    for (int i = low; i <= high; i++) sum += arr[i];
    while (high < arr.size()) {
        res = max(res, sum);
        low++; high++;
        if (high == arr.size()) break;
        sum = sum - arr[low - 1] + arr[high];
    }
    return res;
}
```

---

### Q2 — Minimum Size Subarray Sum (Variable, Minimum)
| | |
|---|---|
| **Problem** | Given an array of positive integers and a `target`, find the length of the shortest subarray whose sum is `≥ target`. |
| **Key observation** | No size is given — only a lower-bound condition (`sum ≥ target`). This signals Variable **Minimum**. |
| **Why Sliding Window works** | Since all numbers are positive, expanding the window only ever increases the sum, and shrinking only ever decreases it — a clean monotonic relationship the two pointers can exploit. |
| **Approach (Hiring & Firing)** | "Hire" by expanding `high` and adding to `sum` until `sum ≥ target` ("work is getting done"). The instant it's valid, record the current length, then start "firing" from `low` (subtract, `low++`) — recording each new, smaller valid length — until the sum drops below target. Then resume hiring. |
| **Pattern used** | Variable **Minimum** Window |
| **Takeaway** | For Minimum-type problems, shrink **while valid**, and record the result **inside** the shrink loop — the opposite of the Maximum template. |

```cpp
int minSubArrayLen(int target, vector<int>& nums) {
    int low = 0, sum = 0, minLength = INT_MAX;
    for (int high = 0; high < nums.size(); high++) {
        sum += nums[high];
        while (sum >= target) {
            minLength = min(minLength, high - low + 1);
            sum -= nums[low];
            low++;
        }
    }
    return (minLength == INT_MAX) ? 0 : minLength;
}
```

---

### Q3 — Longest Substring with K Distinct Characters (Variable, Maximum, "exactly K")
| | |
|---|---|
| **Problem** | Given a string and integer `K`, find the length of the longest substring containing **exactly** `K` distinct characters. |
| **Key observation** | No length is given, but the distinct-character condition has both a meaningful upper bound (`> K` is definitely invalid) and a target match (`== K` is what we want, not just `≤ K`). |
| **Why Sliding Window works** | As `high` advances, the number of distinct characters (hashmap size) can only stay the same or grow; shrinking `low` (and erasing zero-frequency entries) can only shrink or maintain it — so once it overshoots `K`, shrinking is the only way back. |
| **Approach** | Include `high` in a frequency hashmap. While `freq.size() > K`, shrink `low` (decrement, erase if it hits zero). After the shrink loop, **if** `freq.size() == K`, record `high - low + 1`. |
| **Pattern used** | Variable **Maximum** Window, "exactly K" variant (needs the extra `if` check) |
| **Takeaway** | "Exactly K" problems use the same Maximum template as "at most K" — the only addition is an `if` guard before recording, since a window with *fewer* than K distinct characters is valid-but-not-yet-counted. |

```cpp
int longestKSubstr(string &s, int k) {
    unordered_map<char, int> freq;
    int low = 0, maxLen = -1;
    for (int high = 0; high < s.size(); high++) {
        freq[s[high]]++;
        while (freq.size() > k) {
            freq[s[low]]--;
            if (freq[s[low]] == 0) freq.erase(s[low]);
            low++;
        }
        if (freq.size() == k) maxLen = max(maxLen, high - low + 1);
    }
    return maxLen;
}
```

---

### Q4 — Fruit Into Baskets (Variable, Maximum, "at most 2")
| | |
|---|---|
| **Problem** | Fruit trees stand in a row; collect fruit walking left-to-right using a basket that can hold **at most 2 distinct types**. Find the maximum number of fruits collectible. |
| **Key observation** | This is a story problem — translated, it's: "find the longest **contiguous** subarray with at most 2 distinct values." No explicit subarray/substring wording, but the underlying ask is identical to Q3. |
| **Why Sliding Window works** | Same monotonic distinct-count logic as Q3 — fruit types map directly onto "distinct characters." |
| **Approach** | Identical template to Q3, but since the condition is "at most 2" rather than "exactly K," **every** window that survives the shrink loop (size ≤ 2) is automatically valid — no `if` check is needed; just record `high - low + 1` every iteration. |
| **Pattern used** | Variable **Maximum** Window, "at most K" variant (simplest form — no `if` needed) |
| **Takeaway** | Translating a real-world story into "subarray with property X" is the actual skill being tested — once translated, this is the *easier* sibling of Q3 (drop the `if`, otherwise identical code). |

```cpp
int totalFruit(vector<int>& fruits) {
    unordered_map<int, int> freq;
    int low = 0, maxLen = 0;
    for (int high = 0; high < fruits.size(); high++) {
        freq[fruits[high]]++;
        while (freq.size() > 2) {
            freq[fruits[low]]--;
            if (freq[fruits[low]] == 0) freq.erase(fruits[low]);
            low++;
        }
        maxLen = max(maxLen, high - low + 1);
    }
    return maxLen;
}
```

---

### Q5 — Longest Substring Without Repeating Characters (Variable, Maximum, no K at all)
| | |
|---|---|
| **Problem** | Find the length of the longest substring with **no repeating characters**. |
| **Key observation** | There's no `K` anywhere in this problem — but "all unique" can be tested by comparing the hashmap's size to the **window's own length**: if `freq.size() == window length`, every character is unique by definition. |
| **Why Sliding Window works** | The moment a duplicate enters the window, the hashmap size becomes smaller than the window length; shrinking from `low` removes characters one at a time until the duplicate is gone and the two values match again. |
| **Approach** | Include `high`. While `freq.size() < (high - low + 1)` (i.e., a duplicate exists in the window), shrink `low` (decrement, erase if zero), recomputing the window length each time. Once the `while` ends, the window is automatically duplicate-free — record `high - low + 1` directly, with no `if` needed. |
| **Pattern used** | Variable **Maximum** Window where `K` is **self-derived** as the window's own current length, rather than given by the problem. |
| **Takeaway** | When a problem gives no explicit bound, look for a way to define "correct" using the window's own properties (here: distinct count vs. window length) instead of assuming the pattern doesn't apply. |

```cpp
int lengthOfLongestSubstring(string s) {
    unordered_map<char, int> freq;
    int low = 0, maxLen = 0;
    for (int high = 0; high < s.size(); high++) {
        freq[s[high]]++;
        int k = high - low + 1;
        while (freq.size() < k) {
            freq[s[low]]--;
            if (freq[s[low]] == 0) freq.erase(s[low]);
            low++;
            k = high - low + 1;
        }
        maxLen = max(maxLen, high - low + 1);
    }
    return maxLen;
}
```

---

### Q6 — Longest Repeating Character Replacement (Variable, Maximum, with a budget K)
| | |
|---|---|
| **Problem** | Given a string and integer `K`, you may change up to `K` characters (to any character). Find the length of the longest substring achievable where all characters are the same. |
| **Key observation** | A window is achievable within budget exactly when `window_length − max_character_frequency ≤ K` — i.e., keep the most frequent character fixed and only the minority characters need changing (the "majority party" trick). |
| **Why Sliding Window works** | As `high` grows, `maxFreq` and window length change in a way that lets you check achievability in O(1) (using a constant-size frequency array), so each step's validity check stays cheap. |
| **Approach** | Use a 26/256-size frequency array. Include `high`, update `maxFreq = max(maxFreq, freq[s[high]])`. While `(high - low + 1) - maxFreq > K`, shrink `low`. Record `max(res, high - low + 1)` every iteration (this is an "at most K"-style condition, so no `if` is needed once the `while` ends). |
| **Pattern used** | Variable **Maximum** Window — same skeleton as Q4/Q5, with a smarter validity test built from `maxFreq`. |
| **Takeaway** | `maxFreq` is allowed to go slightly **stale** (it's never decreased even as the window shrinks) — this is a deliberate, safe optimization: because the algorithm only ever records the achieved window length, and `low` only advances when truly forced, a stale `maxFreq` can never cause an incorrect (too-large) answer to be recorded — it can only delay a shrink by a step. **Practice next:** *Max Consecutive Ones III* (flip at most K zeros to find the longest all-1s subarray) uses this exact same "at most K changes" template. |

```cpp
int characterReplacement(string s, int k) {
    unordered_map<char, int> freq;
    int low = 0, maxFreq = 0, maxLen = 0;
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
```

---

### Q7 — Minimum Window Substring (Variable, Minimum, Hard)
| | |
|---|---|
| **Problem** | Given strings `S` and `T`, find the smallest substring of `S` that contains every character of `T`, including duplicates, in any order. |
| **Key observation** | "Must contain at least all of T" is a lower-bound condition — this is a Minimum-type window, exactly like Q2, just with a richer definition of "valid." |
| **Why Sliding Window works** | Once a window contains "enough" of every required character, shrinking from the left can only reduce counts — so re-validating after each removal correctly detects the moment the window stops being sufficient. |
| **Approach** | Build a `need[256]` frequency array from `T`. Slide `high` through `S`, incrementing `have[s[high]]`. While a helper check (`have[i] ≥ need[i]` for all `i`) confirms the window is valid: record `(length, start)` if it's the smallest seen so far, then shrink `low` (decrement `have[s[low]]`, `low++`) — exactly the Minimum template (record **inside** the "while valid" loop, before shrinking). Return `S.substr(start, res)`, or `""` if no valid window was ever found. |
| **Pattern used** | Variable **Minimum** Window with a multi-character containment check as the "valid" condition. |
| **Takeaway** | A LeetCode "Hard" problem is solved with the *exact same* Minimum-window template as the "Easy" Q2 — the only real difference is that "valid" here is a function comparing two frequency arrays instead of a single sum comparison. Identify Max vs. Min first; the template does the rest. |

```cpp
bool isValid(vector<int>& have, vector<int>& need) {
    for (int i = 0; i < 256; i++)
        if (have[i] < need[i]) return false;
    return true;
}

string minWindow(string s, string t) {
    int n = s.size(), m = t.size();
    if (n < m) return "";

    vector<int> have(256, 0), need(256, 0);
    for (int i = 0; i < m; i++) need[t[i]]++;

    int low = 0, res = INT_MAX, start = -1;
    for (int high = 0; high < n; high++) {
        have[s[high]]++;
        while (isValid(have, need)) {
            int len = high - low + 1;
            if (res > len) { res = len; start = low; }
            have[s[low]]--;
            low++;
        }
    }
    return (res == INT_MAX) ? "" : s.substr(start, res);
}
```

---

## 8. Interview Revision Sheet

### Pattern identification (10-second check)
1. Array or String (not Linked List)?
2. Talks about a **subarray/substring** (continuous) — not a subsequence?
3. Asks for max / min / longest / shortest / sum / count / average / at-most-K / at-least-K / exactly-K?

→ All three yes = **Sliding Window.**

### Window-type decision
- Size `K` explicitly given → **Fixed**
- No size given, condition is `≤` / "at most" / "no duplicates" → **Variable Maximum**
- No size given, condition is `≥` / "at least" / "must contain" → **Variable Minimum**

### Compact templates

**Fixed:**
```cpp
low=0, high=k-1; build first window's sum;
while (high < n) {
    res = max(res, sum);
    low++; high++;
    if (high == n) break;
    sum += arr[high] - arr[low-1];
}
```

**Variable Maximum:**
```cpp
for (high = 0; high < n; high++) {
    include high;
    while (invalid) shrink low;          // shrink WHILE invalid
    res = max(res, high-low+1);          // record AFTER shrink loop
    // (wrap in `if exact-match` for "exactly K" problems)
}
```

**Variable Minimum:**
```cpp
for (high = 0; high < n; high++) {
    include high;
    while (valid) {                      // shrink WHILE valid
        res = min(res, high-low+1);      // record INSIDE shrink loop
        shrink low;
    }
}
return (res == INT_MAX) ? 0 : res;
```

### Most important tricks
- Update info **incrementally** (`new = old − leaving + entering`) — never recompute from scratch.
- Use a **256-size array** for character frequency instead of a hashmap when you need fast max-frequency lookups.
- **Erase zero-frequency keys** from hashmaps, or `map.size()` lies to you.
- `res = INT_MAX` for minimum problems, `res = INT_MIN`/`0` for maximum problems.
- Max ⇔ condition is `≤`. Min ⇔ condition is `≥`. (The opposite direction is never a meaningful question for non-negative inputs.)

### Common mistakes to avoid
- Confusing subsequence (non-continuous) with subarray/substring (continuous) — SW only applies to the latter.
- Using "shrink while invalid" logic on a **Minimum** problem (it should be "shrink while valid").
- Forgetting the `high == n` boundary check after `high++` in a Fixed window.
- Recomputing sum/frequency from scratch every slide (kills the O(N) benefit).
- Leaking `INT_MAX`/`INT_MIN` into the final answer when no valid window exists.

### Interview tips
- State the 3-check flowchart out loud — it signals you're pattern-matching, not guessing, and is usually enough to make an interviewer relax.
- Explicitly say "Fixed or Variable?" and "Max-type or Min-type?" before writing code — this sequencing itself demonstrates structured thinking.
- For story-style questions (no literal "subarray" wording), translate the question into your own words first ("what continuous segment property am I really finding?") before deciding the pattern doesn't fit.
- Trace 2–3 windows by hand on paper/whiteboard before coding — it almost always reveals the correct shrink condition faster than reasoning in the abstract.

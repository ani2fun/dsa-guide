## Brute

### Intuition

**The simple idea**
Think of a class election where you count paper ballots by hand. To check whether "Maya" won, you pick up her name, walk down the *entire* stack of ballots, and make a tick every time you see "Maya". To be fair, you repeat this for **every** candidate. The first candidate with more ticks than half the total ballots is the winner.

**The engineer's view**
This is the naive frequency scan: `for each candidate → one O(N) scan` ⇒ **O(N²)**. Two observations shape everything that follows:

1. **Redundant recounting.** If a value occurs `k` times, the outer loop counts it `k` separate times. We never reuse a count.
2. **Early exit is safe.** Since at most one majority can exist (pigeonhole), the *first* value crossing `n/2` is *the* answer.

Note the check is strict — `cnt > n // 2`. For `n = 7` you need ≥ 4 occurrences; an element occurring exactly `n/2` times (possible only for even `n`) is *not* a majority.

### Approach

1. Loop over every index `i` — treat `nums[i]` as a candidate.
2. Reset `cnt = 0`, then scan the *entire* array with `j`, incrementing `cnt` whenever `nums[j] == nums[i]`.
3. If `cnt > n // 2`, return `nums[i]` immediately.
4. If no candidate crosses the threshold, return `-1`.

### Dry Run

`arr = [2, 2, 1, 1, 1, 2, 2]`, `n = 7` → need strictly more than `7 // 2 = 3`. (✔ = matches candidate, ✘ = doesn't)

| `i` | Candidate | Inner scan over the array | `cnt` | `cnt > 3`? |
|---|---|---|---|---|
| 0 | `2` | 2✔ 2✔ 1✘ 1✘ 1✘ 2✔ 2✔ | **4** | ✅ **return 2** |

The early return fires at `i = 0`, so we never check the remaining candidates. But that's luck of the draw — if the majority first appeared at the *end* of the array, or if there were **no** majority at all (we'd have to exhaust every candidate before returning `-1`), we'd pay the full `N × N` price. That quadratic worst case is what "Better" eliminates.

### Solution

```python solution time=O(N²) space=O(1)
from typing import List

class Solution:
    # Function to find the majority element in an array
    def majorityElement(self, nums: List[int]) -> int:

        # Size of the given array
        n = len(nums)

        # Pick each element as a "candidate" one at a time
        for i in range(n):

            # Tally of the current candidate nums[i]
            cnt = 0

            # Inner pass: rescan the WHOLE array to count every
            # occurrence of nums[i]  <- this is the O(N²) hotspot
            for j in range(n):
                if nums[j] == nums[i]:
                    cnt += 1

            # Majority = STRICTLY more than half
            # (n = 7 -> need 4+; exactly n/2 is NOT enough)
            if cnt > (n // 2):
                # Pigeonhole: at most ONE majority element can exist,
                # so the first candidate that crosses the line is THE
                # answer — no need to check anyone else
                return nums[i]

        # Every candidate counted, none crossed n/2 -> no majority
        return -1


# Reads the test case's nums, e.g. [2, 2, 1, 1, 1, 2, 2]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().majorityElement(nums))
```

```java solution time=O(N²) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the majority element in an array
        int majorityElement(int[] nums) {

            // Size of the given array
            int n = nums.length;

            // Pick each element as a "candidate" one at a time
            for (int i = 0; i < n; i++) {

                // Tally of the current candidate nums[i]
                int cnt = 0;

                // Inner pass: rescan the WHOLE array to count every
                // occurrence of nums[i]  <- this is the O(N²) hotspot
                for (int j = 0; j < n; j++) {
                    if (nums[j] == nums[i]) {
                        cnt++;
                    }
                }

                // Majority = STRICTLY more than half
                // (n = 7 -> need 4+; exactly n/2 is NOT enough)
                if (cnt > (n / 2)) {
                    // Pigeonhole: at most ONE majority element can exist,
                    // so the first candidate that crosses the line is THE
                    // answer — no need to check anyone else
                    return nums[i];
                }
            }

            // Every candidate counted, none crossed n/2 -> no majority
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [2, 2, 1, 1, 1, 2, 2]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().majorityElement(nums));
    }

    // "[1, 2, 3]" -> {1, 2, 3}
    static int[] parseIntArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new int[0];
        String[] parts = inner.split(",");
        int[] out = new int[parts.length];
        for (int i = 0; i < parts.length; i++) out[i] = Integer.parseInt(parts[i].trim());
        return out;
    }
}
```

### Complexity Analysis

**Time: O(N²)** — the outer loop runs up to N times, and each iteration rescans all N elements. Best case is O(N) (majority at index 0 → early return), but the honest worst case — a late majority, or no majority at all — is quadratic. Concretely: with `N = 10⁵`, that's up to ~10¹⁰ comparisons, far beyond a typical 1-second limit.

**Space: O(1)** — one loop index and one counter, no matter how large the input.

## Better 1

### Intuition

**The simple idea**
Brute force kept re-answering the same question — *"how many times does X appear?"* — once for **every single occurrence** of X. That's like re-reading the whole ballot stack for every vote you count. Instead, keep a **tally sheet**: walk the stack once, and for each ballot add one tick next to that candidate's name. Every question gets answered exactly once. Then glance at the sheet — whoever has more than half the ticks wins.

**The engineer's view**
The textbook **space-for-time trade**: replace the O(N) "rescan to count" with an **O(1) average-case hash-map update**, collapsing O(N²) → O(N) at the cost of O(N) auxiliary memory. The map acts like a database index — it turns "search the whole table" into "one keyed lookup." (Per-op cost is amortized O(1) with a sane hash function; adversarial collision chains are a theoretical footnote in modern runtimes.) Idiomatic shortcuts, same algorithm: `collections.Counter(nums)` in Python, `map.merge(num, 1, Integer::sum)` in Java.

### Approach

1. Create an empty hash map `mp` mapping `element → count so far`.
2. **Pass 1 (count):** for each `num`, increment `mp[num]`.
3. **Pass 2 (read the sheet):** return the first key whose value is `> n // 2`.
4. No key qualifies → return `-1`.

*(Production shortcut: check `mp[num] > n/2` inside Pass 1 and return early — kept as two passes here for clarity.)*

### Dry Run

`arr = [2, 2, 1, 1, 1, 2, 2]`, threshold `> 3`.

Pass 1 — build the tally sheet:

| Step | See | Sheet after update |
|---|---|---|
| 1 | `2` | `{2: 1}` |
| 2 | `2` | `{2: 2}` |
| 3 | `1` | `{2: 2, 1: 1}` |
| 4 | `1` | `{2: 2, 1: 2}` |
| 5 | `1` | `{2: 2, 1: 3}` |
| 6 | `2` | `{2: 3, 1: 3}` |
| 7 | `2` | `{2: 4, 1: 3}` |

Pass 2 — read the sheet: `2 → 4` votes, and `4 > 3` → **return 2**.

Compare with brute force: 7 map updates + 1 sheet read ≈ a single linear sweep, versus up to 49 comparisons in the nested-loop version.

### Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    # Function to find the majority element in an array
    def majorityElement(self, nums: List[int]) -> int:

        # Size of the given array
        n = len(nums)

        # Hash map = our "tally sheet": element -> count so far
        mp = {}

        # Pass 1: one sweep. Each distinct element's question
        # ("how many times does it appear?") gets answered exactly
        # once — brute force re-asked it once per occurrence
        for num in nums:
            if num in mp:
                mp[num] += 1
            else:
                mp[num] = 1

        """ Pass 2: read the tally sheet.
        Pigeonhole: at most ONE element can cross n/2,
        so the first qualifying key is THE answer """
        for num, count in mp.items():
            if count > n // 2:
                return num

        # No element crossed the threshold -> no majority
        return -1


# Reads the test case's nums, e.g. [2, 2, 1, 1, 1, 2, 2]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().majorityElement(nums))
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the majority element in an array
        int majorityElement(int[] nums) {

            // Size of the given array
            int n = nums.length;

            // Hash map = our "tally sheet": element -> count so far
            HashMap<Integer, Integer> map = new HashMap<>();

            // Pass 1: count every element in one sweep.
            // getOrDefault: current count, or 0 on first sight — then +1
            for (int num : nums) {
                map.put(num, map.getOrDefault(num, 0) + 1);
            }

            /* Pass 2: read the tally sheet.
            Pigeonhole: at most ONE element can cross n/2,
            so the first qualifying key is THE answer */
            for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
                if (entry.getValue() > n / 2) {
                    return entry.getKey();
                }
            }

            // No element crossed the threshold -> no majority
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [2, 2, 1, 1, 1, 2, 2]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().majorityElement(nums));
    }

    // "[1, 2, 3]" -> {1, 2, 3}
    static int[] parseIntArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new int[0];
        String[] parts = inner.split(",");
        int[] out = new int[parts.length];
        for (int i = 0; i < parts.length; i++) out[i] = Integer.parseInt(parts[i].trim());
        return out;
    }
}
```

### Complexity Analysis

**Time: O(N)** — Pass 1 performs N hash updates; Pass 2 reads at most U ≤ N distinct keys. Two sequential linear passes ⇒ O(N). For `N = 10⁵`: ~2×10⁵ operations instead of ~10¹⁰.

**Space: O(N)** — worst case (all elements distinct) the map stores N entries. That's the rent we pay for the speedup — exactly what the Optimal approach eliminates.

## Better 2

### Intuition

**The simple idea**
Line up all the ballots in one long row, sorted by name — every vote for "Maya" standing together, then every vote for "Leo", and so on. Now the magic: if some name owns **more than half** of all ballots, its block of voters is too long to fit entirely on one side of the row. **It must be standing on the exact middle spot.** No counting needed — sort, look at whoever stands in the middle, done.

**The engineer's view**
A clean application of the **pigeonhole principle**: if `x` occurs `k > N/2` times, its block of `k` consecutive sorted positions cannot avoid covering index `n/2` — a block longer than half the array can't squeeze entirely left of or right of the middle without falling off the end. One indexing operation replaces all counting. Cost: O(N log N) — *worse* than hashing's O(N) — but with **O(1) auxiliary state** and great cache locality. Two production caveats worth saying out loud in an interview: (1) in-place sorting **mutates the caller's array** — copy first if that matters; (2) if existence isn't guaranteed, the middle element is only a *candidate* and needs one O(N) verification pass.

### Approach

1. Sort the array so equal values become adjacent.
2. Take `nums[n // 2]` as the **only possible** majority candidate.
3. Verify by counting its occurrences (skip this pass if the problem guarantees a majority exists, e.g. LeetCode 169).
4. Return the candidate if `count > n // 2`, else `-1`.

### Dry Run

`arr = [2, 2, 1, 1, 1, 2, 2]`.

Sorted: `[1, 1, 1, 2, 2, 2, 2]` — the block of `2`s spans indices 3–6 and covers the middle index `7 // 2 = 3`.

Candidate = `arr[3] = 2`. Verify: `2` occurs 4 times, `4 > 3` → **return 2**.

Why the middle can't lie: a block longer than half the row is too big to fit on either side — start it after the middle, or end it before the middle, and it runs off the end of the array. Only one block can be that big, and it must cover the middle seat.

### Solution

```python solution time=O(N log N) space=O(1)
from typing import List

class Solution:
    # Function to find the majority element in an array
    def majorityElement(self, nums: List[int]) -> int:

        # Size of the given array
        n = len(nums)

        # Sort so equal values sit next to each other.
        # NOTE: sorts IN PLACE (mutates the caller's array) —
        # use `nums = sorted(nums)` if the input must stay untouched
        nums.sort()

        # Pigeonhole: a block of > n/2 equal values is too long to fit
        # on either side of the row — it MUST cover the middle index.
        # So nums[n//2] is the only possible majority
        candidate = nums[n // 2]

        # Verify: count the candidate's occurrences.
        # (Needed only because this problem allows "no majority";
        # skip this pass if existence is guaranteed, e.g. LeetCode 169)
        cnt = nums.count(candidate)

        # Accept only a TRUE majority — strictly more than half
        if cnt > (n // 2):
            return candidate

        # Middle element didn't cross n/2 -> no majority exists
        return -1


# Reads the test case's nums, e.g. [2, 2, 1, 1, 1, 2, 2]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().majorityElement(nums))
```

```java solution time=O(N log N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the majority element in an array
        int majorityElement(int[] nums) {

            // Size of the given array
            int n = nums.length;

            // Sort so equal values sit next to each other.
            // NOTE: sorts IN PLACE (mutates the caller's array)
            Arrays.sort(nums);

            // Pigeonhole: a block of > n/2 equal values is too long to fit
            // on either side of the row — it MUST cover the middle index.
            // So nums[n/2] is the only possible majority
            int candidate = nums[n / 2];

            // Verify: count the candidate's occurrences.
            // (Needed only because this problem allows "no majority";
            // skip this pass if existence is guaranteed, e.g. LeetCode 169)
            int cnt = 0;
            for (int num : nums) {
                if (num == candidate) {
                    cnt++;
                }
            }

            // Accept only a TRUE majority — strictly more than half
            if (cnt > (n / 2)) {
                return candidate;
            }

            // Middle element didn't cross n/2 -> no majority exists
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [2, 2, 1, 1, 1, 2, 2]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().majorityElement(nums));
    }

    // "[1, 2, 3]" -> {1, 2, 3}
    static int[] parseIntArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new int[0];
        String[] parts = inner.split(",");
        int[] out = new int[parts.length];
        for (int i = 0; i < parts.length; i++) out[i] = Integer.parseInt(parts[i].trim());
        return out;
    }
}
```

### Complexity Analysis

**Time: O(N log N)** — dominated by the sort. Picking the middle is O(1); verification is O(N). Trades a `log N` factor against hashing in exchange for (nearly) free memory.

**Space: O(1) auxiliary** for the algorithm itself — one candidate variable and one counter. Fine print on sort internals: Python's Timsort may allocate an O(N) merge buffer in the worst case; Java's `Arrays.sort(int[])` (dual-pivot quicksort) uses O(log N) stack. Both are conventionally called "in-place" in interviews — but a memory-tight code review should flag the Timsort buffer.

## Optimal

### Intuition

**The simple idea — the cancellation duel**
Back to the party: every guest shouts the dish they brought. Instead of a full tally sheet, keep just **one champion dish and a score**:

- No champion yet? The dish you just heard becomes champion, score 1.
- Someone shouts the champion's dish? Score +1.
- Someone shouts a *different* dish? Score −1 — **one opposing voice cancels one supporter**.
- Score hits 0? The champion is dethroned; the next dish takes over.

Why must the true majority dish survive this carnage? Because it owns **more than half** of all voices. Even in the worst case where *every* non-majority voice cancels one majority voice, the majority still has voices left over — "more than half" minus "less than half" is still more than zero. Every other dish can be canceled *completely*.

**The engineer's view**
This is the **Boyer–Moore majority vote algorithm** (Boyer & Moore, 1980; the `k = 2` case of Misra–Gries, 1982). Maintain `(candidate, count)` where `count` is the **net surplus** of the candidate over non-candidates within the current segment: `count = (#candidate) − (#non-candidate)` since the last reset. Correctness is a pairing/discarding argument:

- Every completed segment (one that ends with `count = 0`) has its candidate appearing **exactly half** the time — so the true majority `x` occupies at most half of it, whether `x` was that segment's candidate or one of its cancelers.
- Discarding such segments removes at most half as many copies of `x` as elements discarded. If the discarded prefix has length D, the remaining suffix (length N − D) still holds `> (N − D)/2` copies of `x` — **x stays a majority of whatever is left**.
- The final segment's surviving candidate is a *strict* majority within that segment, and two different values can't both be strict in-segment majorities — so the final candidate must be `x`. ∎

Properties that matter in practice: single pass, O(1) state, sequential memory access (cache-friendly), no hashing, deterministic — and unlike the hashmap approach it's a true **streaming algorithm**, usable when the data doesn't fit in memory. Generalizes via Misra–Gries: keep `k − 1` counters to find all elements occurring more than `N/k` times. One honest caveat: Boyer–Moore guarantees the majority element *is* the candidate **if one exists** — it does *not* certify existence (feed it `[1, 2, 3]` and it confidently hands you `3`). Hence the verification pass below, skippable when existence is guaranteed.

### Approach

1. Keep two variables: `cnt` (net score) and `el` (current candidate).
2. Single pass over `nums`:
   - `cnt == 0` → adopt the current element: `el = num`, `cnt = 1`.
   - `num == el` → `cnt += 1` (a supporter joins).
   - `num != el` → `cnt -= 1` (one cancelation).
3. After the pass, `el` is the **candidate** — the only value that *could* be the majority.
4. Verify by recounting `el` (this problem must return `-1` when no majority exists — skip if existence is guaranteed).
5. Return `el` if `count > n // 2`, else `-1`.

### Dry Run

`arr = [2, 2, 1, 1, 1, 2, 2]`, threshold `> 3`.

| `num` | Rule fired | `el` | `cnt` | What it means |
|---|---|---|---|---|
| `2` | `cnt == 0` → adopt | 2 | 1 | 2 leads by 1 |
| `2` | match → +1 | 2 | 2 | 2 leads by 2 |
| `1` | mismatch → −1 | 2 | 1 | one vote of 2 canceled |
| `1` | mismatch → −1 | 2 | 0 | 2 fully canceled → dethroned |
| `1` | `cnt == 0` → adopt | 1 | 1 | 1 takes over |
| `2` | mismatch → −1 | 1 | 0 | 1 canceled → dethroned |
| `2` | `cnt == 0` → adopt | 2 | 1 | 2 leads by 1 at the end |

Final candidate `el = 2`. Verification: `2` occurs 4 times, `4 > 3` → **return 2**. ✅

Watch the tug-of-war in the middle rows: the block `1, 1` exactly cancels the lead `2, 2` had built — a microcosm of why any non-majority value can never outlast the true majority.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    # Function to find the majority element in an array
    def majorityElement(self, nums: List[int]) -> int:

        # Size of the given array
        n = len(nums)

        # Net score of the candidate:
        # +1 for every matching element, -1 for every opposing one
        cnt = 0

        # Current candidate for majority element
        el = 0

        # Boyer–Moore voting pass: opposing elements cancel each
        # other, so a strict majority can never be fully canceled
        for num in nums:
            if cnt == 0:
                # No live candidate -> current element takes over
                cnt = 1
                el = num
            elif el == num:
                # Another supporter joins the candidate
                cnt += 1
            else:
                # One opposing vote cancels one supporter
                cnt -= 1

        """ Boyer–Moore promises: IF a majority exists, it is `el`.
        It does NOT promise `el` IS a majority (try [1, 2, 3] ->
        candidate 3), so verify before answering. """
        cnt1 = nums.count(el)

        # Accept only a TRUE majority — strictly more than half
        if cnt1 > (n // 2):
            return el

        # Verification failed -> no majority element
        return -1


# Reads the test case's nums, e.g. [2, 2, 1, 1, 1, 2, 2]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().majorityElement(nums))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the majority element in an array
        int majorityElement(int[] nums) {
            // Size of the given array
            int n = nums.length;

            // Net score of the candidate:
            // +1 for every matching element, -1 for every opposing one
            int cnt = 0;

            // Current candidate for majority element
            int el = 0;

            // Boyer–Moore voting pass: opposing elements cancel each
            // other, so a strict majority can never be fully canceled
            for (int i = 0; i < n; i++) {
                if (cnt == 0) {
                    // No live candidate -> current element takes over
                    cnt = 1;
                    el = nums[i];
                } else if (el == nums[i]) {
                    // Another supporter joins the candidate
                    cnt++;
                } else {
                    // One opposing vote cancels one supporter
                    cnt--;
                }
            }

            /* Boyer–Moore promises: IF a majority exists, it is `el`.
            It does NOT promise `el` IS a majority (try [1, 2, 3] ->
            candidate 3), so verify before answering. */
            int cnt1 = 0;
            for (int i = 0; i < n; i++) {
                if (nums[i] == el) {
                    cnt1++;
                }
            }

            // Accept only a TRUE majority — strictly more than half
            if (cnt1 > (n / 2)) {
                return el;
            }

            // Verification failed -> no majority element
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [2, 2, 1, 1, 1, 2, 2]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().majorityElement(nums));
    }

    // "[1, 2, 3]" -> {1, 2, 3}
    static int[] parseIntArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new int[0];
        String[] parts = inner.split(",");
        int[] out = new int[parts.length];
        for (int i = 0; i < parts.length; i++) out[i] = Integer.parseInt(parts[i].trim());
        return out;
    }
}
```

### Complexity Analysis

**Time: O(N) + O(N) = O(N)** — the first pass runs the voting duel; the second verifies the candidate. Verification exists only because this problem allows "no majority"; when existence is guaranteed (LeetCode 169), drop it for a true single-pass solution.

**Space: O(1)** — two integers. This is the entire selling point over the hashmap: state that doesn't grow with input, which is what makes Boyer–Moore usable as a **streaming algorithm** on data too big to store.

## Quick Recap

| Approach | Core idea | Time | Space |
|---|---|---|---|
| Brute | Recount each element with a fresh scan | O(N²) | O(1) |
| Better 1 | Hash-map tally sheet | O(N) | O(N) |
| Better 2 | Sort → majority must sit at the middle index | O(N log N) | O(1)* |
| Optimal | Boyer–Moore: opposing votes cancel out | O(N) | O(1) |

`* modulo sort internals and input mutation.`

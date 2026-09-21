## Brute

### Intuition

Imagine two guest lists for two events, where **each entry on the second list is a physical RSVP card**. You want to build a list of guests attending both events.

You walk through the first list name by name. For each name, you flip through the second list looking for that name on a card. When you find one, you write the name down and **tick off that card** so it can never be matched again. And since the second list is **alphabetical (sorted)**, you stop flipping the moment you hit a name that comes *after* the one you're searching for — nobody further down can possibly match.

This maps directly to the two key mechanisms in the code:

- **The `visited` array = the ticked-off RSVP cards.** Without it, if `nums2 = [2]` and `nums1 = [2, 2]`, the single `2` in `nums2` would be matched twice, wrongly producing `[2, 2]`. With it, we get the correct `[2]`.
- **The early `break` = the alphabetical shortcut.** It only works because the problem assumes both arrays are sorted — this assumption is worth stating explicitly in the explanation.

Net effect: a value appears in the answer exactly `min(count in nums1, count in nums2)` times (intersection with multiplicity).

### Approach

**Assumption:** both arrays are sorted in non-decreasing order (required for the early exit).

1. Create `visited` of size `len(nums2)`, all zeros — every element of `nums2` starts as "free."
2. For each element `nums1[i]`, scan `nums2` left to right with index `j`:
   - **Match found** (`nums1[i] == nums2[j]`) **and `visited[j] == 0`** → mark `visited[j] = 1`, append `nums1[i]` to `ans`, and `break` (this copy of `nums1[i]` is satisfied).
   - **`nums2[j] > nums1[i]`** → since `nums2` is sorted, no later element can equal `nums1[i]`; `break` to skip wasted comparisons.
   - Otherwise (`nums2[j] < nums1[i]`) → simply continue scanning.
3. Duplicates in `nums1` are handled automatically: each copy independently searches for its own *unused* copy in `nums2`.
4. Return `ans`.

### Dry Run

`nums1 = [2, 2, 3]`, `nums2 = [2, 3, 5]`

| `i` | `nums1[i]` | Inner loop behavior | `ans` |
|---|---|---|---|
| 0 | 2 | `j=0`: `2==2`, free → match, `visited=[1,0,0]`, break | `[2]` |
| 1 | 2 | `j=0`: `2==2` but `visited[0]=1` → skip; `j=1`: `3>2` → break | `[2]` |
| 2 | 3 | `j=0`: `2<3` continue; `j=1`: `3==3`, free → match, break | `[2, 3]` |

### Solution

```python solution time=O(N1×N2) space=O(N2)
from typing import List

class Solution:
    # 'visited' acts as a checkbox for every element of nums2:
    #   visited[j] = 0  ->  nums2[j] is still "free" (not matched yet)
    #   visited[j] = 1  ->  nums2[j] has already been used in a match
    # This guarantees each element of nums2 is consumed at most once,
    # so duplicates are handled correctly.
    def intersectionArray(self, nums1: List[int], nums2: List[int]) -> List[int]:
        visited = [0] * len(nums2)

        # Collects the common elements (the final intersection).
        ans = []

        # Outer loop: pick each element of nums1 one by one.
        for i in range(len(nums1)):
            # Inner loop: scan nums2 to search for a match for nums1[i].
            for j in range(len(nums2)):
                # Case 1: exact match found AND this nums2 element is unused.
                if nums1[i] == nums2[j] and visited[j] == 0:
                    visited[j] = 1         # mark this nums2 element as "used"
                    ans.append(nums1[i])   # record the common element
                    break                  # one nums1[i] consumes only one match

                # Case 2: early exit optimization.
                # nums2 is sorted, so the moment we see a value LARGER than
                # nums1[i], every element after it is also larger ->
                # no match is possible further right. Stop scanning.
                if nums2[j] > nums1[i]:
                    break

        return ans


# Reads the test case's nums1 and nums2, one per line
inner1 = input().strip()[1:-1].strip()
nums1 = [int(t) for t in inner1.split(",")] if inner1 else []
inner2 = input().strip()[1:-1].strip()
nums2 = [int(t) for t in inner2.split(",")] if inner2 else []
result = Solution().intersectionArray(nums1, nums2)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N1×N2) space=O(N2)
import java.util.*;

public class Main {
    static class Solution {
        int[] intersectionArray(int[] nums1, int[] nums2) {

            // 'visited' acts as a checkbox for every element of nums2:
            //   visited[j] = 0  ->  nums2[j] is still "free" (not matched yet)
            //   visited[j] = 1  ->  nums2[j] has already been used in a match
            // This guarantees each element of nums2 is consumed at most once,
            // so duplicates are handled correctly.
            // Note: new int[...] in Java is auto-initialized to all zeros,
            // just like [0] * len(nums2) in Python.
            int[] visited = new int[nums2.length];

            // Dynamic list to collect common elements. Java arrays have a fixed
            // size, so we use an ArrayList since the intersection size is
            // unknown upfront (Python's list.append has no direct array equivalent).
            List<Integer> ansList = new ArrayList<>();

            // Outer loop: pick each element of nums1 one by one.
            for (int i = 0; i < nums1.length; i++) {

                // Inner loop: scan nums2 to search for a match for nums1[i].
                for (int j = 0; j < nums2.length; j++) {

                    // Case 1: exact match found AND this nums2 element is unused.
                    if (nums1[i] == nums2[j] && visited[j] == 0) {
                        visited[j] = 1;          // mark this nums2 element as "used"
                        ansList.add(nums1[i]);   // record the common element
                        break;                   // one nums1[i] consumes only one match
                    }

                    // Case 2: early exit optimization.
                    // nums2 is sorted, so the moment we see a value LARGER than
                    // nums1[i], every element after it is also larger ->
                    // no match is possible further right. Stop scanning.
                    if (nums2[j] > nums1[i]) {
                        break;
                    }
                }
            }

            // Convert the List<Integer> into a primitive int[] to return,
            // since most judges expect int[] as the return type.
            int[] ans = new int[ansList.size()];
            for (int k = 0; k < ansList.size(); k++) {
                ans[k] = ansList.get(k);
            }

            return ans;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums1 and nums2, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums1 = parseIntArray(sc.nextLine());
        int[] nums2 = parseIntArray(sc.nextLine());
        System.out.println(Arrays.toString(new Solution().intersectionArray(nums1, nums2)));
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

- **Time Complexity:** `O(N1 × N2)` worst case — e.g., when every element of `nums2` is smaller than `nums1[i]`, the early `break` never triggers. The sorted-array shortcut just makes it faster *in practice*.
- **Space Complexity:** `O(N2)` for the `visited` array (plus the output).

## Optimal

### Intuition

Two party organizers stand side by side, each holding their event's guest list — both lists are alphabetical. Instead of one organizer re-reading the whole second list for every single name (that's the brute force), they walk down their lists **together, in lockstep**, comparing whoever is currently on top:

- **Organizer A's name comes earlier alphabetically** than Organizer B's? Then that guest can't be attending both — every remaining name on B comes later. Skip A's guest; that person is eliminated forever.
- **Organizer B's name comes earlier?** Same logic, mirrored — skip B's guest.
- **Same name?** That guest attends both parties. Write it down, and both organizers move forward together.

Every comparison permanently **eliminates** at least one candidate, and no matching pair is ever skipped. When either organizer runs out of names, they're done.

**Why no `visited` array is needed:** pointers only ever move forward, and on a match both copies are consumed simultaneously. If `nums1` has two 2s but `nums2` has only one 2, the first match eats `nums2`'s copy (`j` moves past it); the second 2 in `nums1` is then compared against something strictly larger — or against nothing — and correctly fails. Duplicates come out exactly `min(count in nums1, count in nums2)` times, for free.

**The connection to brute force:** the early `break` there was a hint. Once you've passed position `j` in sorted `nums2`, you never need to look before it again — but the brute force *forgets* this and restarts the `j`-scan from 0 for every `nums1[i]`. The two-pointer version simply **remembers where it left off**: `j` never resets. That's the entire optimization.

### Approach

**Assumption:** both arrays are sorted in non-decreasing order — here it's not an optional speedup, it's what makes the algorithm correct.

1. Initialize `i = 0`, `j = 0`, and an empty result list `ans`.
2. Loop while both pointers are in bounds (`i < n and j < m`), comparing the current elements:
   - **`nums1[i] < nums2[j]`** → `nums1[i]` is smaller than *everything* remaining in `nums2`, so it can't be common. Advance `i`.
   - **`nums1[i] > nums2[j]`** → mirror case. Advance `j`.
   - **Equal** → common element: append it, advance **both** pointers.
3. Each iteration advances at least one pointer, so the loop always terminates. When one array is exhausted, the other's leftovers can't match anything. Return `ans`.

**Why it never misses a match:** each step compares the *smallest unconsumed* element of each array. If they differ, the smaller one provably can't equal anything still remaining in the other array — discarding it is safe. If they're equal, that's the earliest available match on both sides — consuming it is safe. Nothing is skipped, nothing is double-counted.

### Dry Run

`nums1 = [2, 2, 3]`, `nums2 = [2, 3, 5]`

| Step | `i` | `j` | `nums1[i]` | `nums2[j]` | Comparison | Action | `ans` |
|---|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 2 | 2 | equal | append 2, `i→1`, `j→1` | `[2]` |
| 2 | 1 | 1 | 2 | 3 | `2 < 3` | discard 2, `i→2` | `[2]` |
| 3 | 2 | 1 | 3 | 3 | equal | append 3, `i→3`, `j→2` | `[2, 3]` |
| 4 | 3 | 2 | — | — | `i == n` → stop | | `[2, 3]` |

Result: `[2, 3]`. Step 2 shows elimination in action, and notice the second `2` was correctly *not* matched — no `visited` array required, unlike the brute force.

### Solution

```python solution time=O(N1+N2) space=O(1)
from typing import List

class Solution:
    def intersectionArray(self, nums1: List[int], nums2: List[int]) -> List[int]:
        n = len(nums1)   # size of nums1
        m = len(nums2)   # size of nums2

        # Collects the common elements (the final intersection).
        ans = []

        # Two pointers, one per array:
        #   i -> current position in nums1
        #   j -> current position in nums2
        # Unlike the brute force, j NEVER resets — it only moves forward.
        i = 0
        j = 0

        # Keep walking while both pointers are inside their arrays.
        # The moment one pointer runs off the end, no more matches exist.
        while i < n and j < m:
            if nums1[i] < nums2[j]:
                # nums1[i] is smaller than everything remaining in nums2
                # (nums2 is sorted). It can never match -> discard it.
                i += 1
            elif nums1[i] > nums2[j]:
                # Mirror case: nums2[j] can never match -> discard it.
                j += 1
            else:
                # nums1[i] == nums2[j] -> common element found.
                ans.append(nums1[i])
                # Advance BOTH pointers: this value is now consumed on
                # both sides. This is what replaces the 'visited' array —
                # duplicates are handled automatically.
                i += 1
                j += 1

        return ans


# Reads the test case's nums1 and nums2, one per line
inner1 = input().strip()[1:-1].strip()
nums1 = [int(t) for t in inner1.split(",")] if inner1 else []
inner2 = input().strip()[1:-1].strip()
nums2 = [int(t) for t in inner2.split(",")] if inner2 else []
result = Solution().intersectionArray(nums1, nums2)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N1+N2) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        int[] intersectionArray(int[] nums1, int[] nums2) {

            // Two pointers, one per array. Neither ever moves backward.
            int i = 0, j = 0;

            // Dynamic result list (intersection size unknown upfront).
            List<Integer> ansList = new ArrayList<>();

            // Walk both sorted arrays in lockstep while both are in bounds.
            while (i < nums1.length && j < nums2.length) {
                if (nums1[i] < nums2[j]) {
                    i++;                     // nums1[i] too small -> discard
                } else if (nums1[i] > nums2[j]) {
                    j++;                     // nums2[j] too small -> discard
                } else {
                    ansList.add(nums1[i]);   // common element found
                    i++;                     // consume it on BOTH sides
                    j++;                     // (no 'visited' array needed)
                }
            }

            // Convert List<Integer> -> int[] for the return type.
            int[] ans = new int[ansList.size()];
            for (int k = 0; k < ansList.size(); k++) {
                ans[k] = ansList.get(k);
            }
            return ans;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums1 and nums2, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums1 = parseIntArray(sc.nextLine());
        int[] nums2 = parseIntArray(sc.nextLine());
        System.out.println(Arrays.toString(new Solution().intersectionArray(nums1, nums2)));
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

- **Time Complexity:** `O(N1 + N2)` — every iteration advances `i`, `j`, or both, so the loop runs at most `N1 + N2` times total. Compare with `O(N1 × N2)` for brute force.
- **Space Complexity:** `O(1)` auxiliary — just two integer pointers. The `visited` array is gone entirely.

| | Brute Force | Two Pointers |
|---|---|---|
| Time | `O(N1 × N2)` | `O(N1 + N2)` |
| Extra space | `O(N2)` (`visited`) | `O(1)` |
| Needs sorted input? | No (sorted only enables the early `break`) | **Yes, essential** |

## Going Further

Both approaches above lean on the sorted-input guarantee. If the arrays were **unsorted**, you'd have two options:

1. **Sort first, then two pointers:** `O(N1 log N1 + N2 log N2)` time, keeps the `O(1)` extra space.
2. **Hash map counting:** count frequencies of `nums2` in a `Counter`, then scan `nums1` and consume counts — `O(N1 + N2)` time but `O(N2)` extra space, and the result wouldn't come out sorted unless you sort it afterward.

For sorted input, the two-pointer walk is optimal: you must at least *look* at every element, and this approach looks at each exactly once.

---
title: "Union Of Two Sorted Arrays"
summary: "Merge two sorted arrays into their sorted, duplicate-free union."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Union Of Two Sorted Arrays

Given two sorted arrays nums1 and nums2, return an array that contains the union of these two arrays. The elements in the union must be in ascending order.

The union of two arrays is an array where all values are distinct and are present in either the first array, the second array, or both.

### Example 1

> - **Input :** nums1 = [1, 2, 3, 4, 5], nums2 = [1, 2, 7]
> - **Output :** [1, 2, 3, 4, 5, 7]
> - **Explanation :**
> The elements 1, 2 are common to both, 3, 4, 5 are from nums1 and 7 is from nums2.

### Example 2

> - **Input :** nums1 = [3, 4, 6, 7, 9, 9], nums2 = [1, 5, 7, 8, 8]
> - **Output :** [1, 3, 4, 5, 6, 7, 8, 9]
> - **Explanation :**
> The element 7 is common to both, 3, 4, 6, 9 are from nums1 and 1, 5, 8 is from nums2.

## Constraints

> - `1 <= nums1.length, nums2.length <= 1000`
> - `-10⁴ <= nums1[i], nums2[i] <= 10⁴`
> - `Both nums1 and nums2 are sorted in non-decreasing order.`

```python run
from typing import List

class Solution:
    # Function to return the sorted union of nums1 and nums2
    def unionArray(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # Your code goes here.
        return []


# Reads the test case's nums1 and nums2, one per line
inner1 = input().strip()[1:-1].strip()
nums1 = [int(t) for t in inner1.split(",")] if inner1 else []
inner2 = input().strip()[1:-1].strip()
nums2 = [int(t) for t in inner2.split(",")] if inner2 else []
result = Solution().unionArray(nums1, nums2)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the sorted union of nums1 and nums2
        int[] unionArray(int[] nums1, int[] nums2) {
            // Your code goes here.
            return new int[0];
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums1 and nums2, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums1 = parseIntArray(sc.nextLine());
        int[] nums2 = parseIntArray(sc.nextLine());
        System.out.println(Arrays.toString(new Solution().unionArray(nums1, nums2)));
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

## Frequently Occurring Doubts

### Why do we need both merging and deduplication?

Merging ensures that elements from both arrays are included in the result in sorted order. Deduplication ensures that repeated elements (either within a single array or across both arrays) appear only once in the final result.

### What if the arrays are very large?

For very large arrays: If they fit in memory, use the two-pointer approach to merge them efficiently. If they don't fit in memory, use external sorting techniques or divide the arrays into manageable chunks, process each chunk separately, and merge the results.

## Follow-ups

### How would you handle unsorted input arrays?

If the input arrays are unsorted: Sort each array first (O(M log M) and O(N log N)). Apply the two-pointer approach or merge logic. This approach would have an overall time complexity of O(M log M + N log N + M + N).

### How would you extend this to handle k sorted arrays?

To handle k sorted arrays: Use a min-heap to merge the arrays. Push the smallest element of each array into the heap. Extract the minimum element, add it to the result, and push the next element from the same array into the heap. This has a time complexity of O(N log k), where N is the total number of elements.

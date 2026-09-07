---
title: "Intersection Of Two Sorted Arrays"
summary: "Return the multiset intersection of two sorted arrays."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Intersection Of Two Sorted Arrays

Given two sorted arrays, nums1 and nums2, return an array containing the intersection of these two arrays. Each element in the result must appear as many times as it appears in both arrays; that is, if an element appears x times in nums1 and y times in nums2, it should appear min(x, y) times in the result.

The intersection of two arrays is an array where all values are present in both arrays.

### Example 1

> - **Input :** nums1 = [1, 2, 2, 3, 5], nums2 = [1, 2, 7]
> - **Output :** [1, 2]
> - **Explanation :**
> The elements 1, 2 are the only elements present in both nums1 and nums2.

### Example 2

> - **Input :** nums1 = [1, 2, 2, 3, 3, 3], nums2 = [2, 3, 3, 4, 5, 7]
> - **Output :** [2, 3, 3]
> - **Explanation :**
> The element 2 appears in both arrays only one time. The element 3 appears in both arrays two times so we add element 3 equal to its number of occurrences.

### Example 3

> - **Input :** nums1 = [-45, -45, 0, 0, 2], nums2 = [-50, -45, 0, 0, 5, 7]
> - **Output :** [-45, 0, 0]

## Constraints

> - `1 <= nums1.length, nums2.length <= 1000`
> - `-10⁴ <= nums1[i], nums2[i] <= 10⁴`
> - `Both nums1 and nums2 are sorted in non-decreasing order.`

```python run
from typing import List

class Solution:
    # Function to return the intersection (with multiplicity) of nums1 and nums2
    def intersectionArray(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # Your code goes here.
        return []


# Reads the test case's nums1 and nums2, one per line
inner1 = input().strip()[1:-1].strip()
nums1 = [int(t) for t in inner1.split(",")] if inner1 else []
inner2 = input().strip()[1:-1].strip()
nums2 = [int(t) for t in inner2.split(",")] if inner2 else []
result = Solution().intersectionArray(nums1, nums2)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the intersection (with multiplicity) of nums1 and nums2
        int[] intersectionArray(int[] nums1, int[] nums2) {
            // Your code goes here.
            return new int[0];
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

## Frequently Occurring Doubts

### What happens if one or both arrays are empty?

If either array is empty, the intersection is empty since there are no common elements.

### How does the algorithm handle duplicates within the arrays?

If duplicates are allowed in the intersection: Include the common element as many times as it appears in both arrays. If duplicates are not allowed: Skip consecutive duplicates in both arrays while processing.

## Follow-ups

### How would you handle unsorted arrays?

For unsorted arrays: Sort both arrays first (O(M log M + N log N)). Apply the two-pointer technique to find the intersection.

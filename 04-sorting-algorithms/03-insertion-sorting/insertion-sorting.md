---
title: "Insertion Sorting"
summary: "Sort an array in non-decreasing order using the insertion sort algorithm."
essential: true
kind: problem
difficulty: easy
topics: [sorting, arrays]
---

# Insertion Sorting

Given an array of integers called nums, sort the array in non-decreasing order using the insertion sort algorithm and return the sorted array.

A sorted array in non-decreasing order is an array where each element is greater than or equal to all preceding elements in the array.

### Example 1

> - **Input :** nums = [7, 4, 1, 5, 3]
> - **Output :** [1, 3, 4, 5, 7]
> - **Explanation :**
> 1 <= 3 <= 4 <= 5 <= 7. Thus the array is sorted in non-decreasing order.

### Example 2

> - **Input :** nums = [5, 4, 4, 1, 1]
> - **Output :** [1, 1, 4, 4, 5]
> - **Explanation :**
> 1 <= 1 <= 4 <= 4 <= 5. Thus the array is sorted in non-decreasing order.

## Constraints

> - `1 <= nums.length <= 1000`
> - `-10⁴ <= nums[i] <= 10⁴`
> - `nums[i] may contain duplicate values.`

```python run
from typing import List

class Solution:
    # Function to sort the array using insertion sort
    def insertionSort(self, nums: List[int]) -> List[int]:
        # Your code goes here.
        return nums


# Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().insertionSort(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to sort the array using insertion sort
        int[] insertionSort(int[] nums) {
            // Your code goes here.
            return nums;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().insertionSort(nums)));
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

### What happens when the array is reversed?

In the worst case (reverse order), each element needs to be compared with all previous elements and shifted to the beginning of the array, leading to O(N²) time complexity.

### When is insertion sort efficient?

Insertion sort is efficient for small or nearly sorted datasets because fewer shifts are needed, and it avoids unnecessary comparisons. Example: Input: [1, 2, 3, 4, 5] (Sorted) The algorithm completes in O(N) as no shifting is required.

## Follow-ups

### How can insertion sort be optimized?

Use binary search to find the correct position for the key in the sorted portion. While this reduces comparisons to O(log N), the shifting operation still takes O(N), so the overall complexity remains O(N²).

### Is insertion sort practical for real-world applications?

Insertion sort is rarely used for large datasets but is practical for Online Sorting, It is effective for dynamic datasets where elements are added incrementally, as it can quickly re-sort the array. Example: Sorting a deck of cards, where new cards are added one at a time.

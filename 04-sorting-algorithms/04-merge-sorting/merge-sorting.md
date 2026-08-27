---
title: "Merge Sorting"
summary: "Sort an array in non-decreasing order using the divide-and-conquer merge sort algorithm."
essential: true
kind: problem
difficulty: medium
topics: [sorting, arrays, recursion]
---

# Merge Sorting

Given an array of integers, nums, sort the array in non-decreasing order using the merge sort algorithm. Return the sorted array.

A sorted array in non-decreasing order is one in which each element is either greater than or equal to all the elements to its left in the array.

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

### Example 3

> - **Input :** nums = [3, 2, 3, 4, 5]
> - **Output :** [2, 3, 3, 4, 5]

## Constraints

> - `1 <= nums.length <= 10⁶`
> - `-10⁴ <= nums[i] <= 10⁴`
> - `nums[i] may contain duplicate values.`

```python run
from typing import List

class Solution:
    # Function to sort the array using merge sort
    def mergeSort(self, nums: List[int]) -> List[int]:
        # Your code goes here.
        return nums


# Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().mergeSort(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to sort the array using merge sort
        int[] mergeSort(int[] nums) {
            // Your code goes here.
            return nums;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().mergeSort(nums)));
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

### Why does merge sort require extra space, and how much?

Merge sort requires extra space to store temporary arrays during the merge process. At each step, two halves are merged into a temporary array before copying back into the original array. The space complexity is O(N), where N is the size of the input array. Example: Input: [4, 3, 2, 1] Merge process uses temporary arrays to combine [4, 3] and [2, 1] into sorted halves, and finally merges them into [1, 2, 3, 4].

### Can merge sort handle duplicate elements?

Yes, merge sort naturally handles duplicates by preserving their relative order during the merging process. This makes it a stable sorting algorithm.

## Follow-ups

### Can merge sort be implemented in-place? If not, why?

Standard merge sort is not in-place because merging two sorted arrays requires additional memory to combine them. However, there are in-place variations of merge sort, but they are complex and trade simplicity and performance for reduced memory usage.

### Why is merge sort preferred for linked lists?

Linked lists do not support random access, making quicksort inefficient. Merge sort efficiently splits linked lists into halves using pointers without needing extra space for copying. Merging two sorted linked lists can be done in O(N) without additional memory overhead. Example: Input: 4 → 2 → 9 → 1 Process: Split into 4 → 2 and 9 → 1. Sort each half: 2 → 4 and 1 → 9. Merge: 1 → 2 → 4 → 9.

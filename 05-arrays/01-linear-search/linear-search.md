---
title: "Linear Search"
summary: "Find the smallest index at which a target appears in an array, or -1 if absent."
essential: true
kind: problem
difficulty: easy
topics: [arrays, searching]
---

# Linear Search

Given an array of integers nums and an integer target, find the smallest index (0 based indexing) where the target appears in the array. If the target is not found in the array, return -1.

### Example 1

> - **Input :** nums = [2, 3, 4, 5, 3], target = 3
> - **Output :** 1
> - **Explanation :**
> The first occurence of 3 in nums is at index 1.

### Example 2

> - **Input :** nums = [2, -4, 4, 0, 10], target = 6
> - **Output :** -1
> - **Explanation :**
> The value 6 does not occur in the array, hence output is -1.

### Example 3

> - **Input :** nums = [1, 3, 5, -4, 1], target = 1
> - **Output :** 0

## Constraints

> - `1 <= nums.length <= 10⁵`
> - `-10⁴ <= nums[i] <= 10⁴`
> - `-10⁴ <= target <= 10⁴`

```python run
from typing import List

class Solution:
    # Linear Search Function
    def linearSearch(self, nums: List[int], target: int) -> int:
        # Your code goes here.
        return -1


# Reads the test case's nums and target, one per line
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
target = int(input())
print(Solution().linearSearch(nums, target))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Linear Search Function
        int linearSearch(int[] nums, int target) {
            // Your code goes here.
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums and target, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums = parseIntArray(sc.nextLine());
        int target = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().linearSearch(nums, target));
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

### What happens if the target is not found in the array?

If the target is not present, the function should return -1. This indicates that no index contains the target value. Example: Input: nums = [1, 2, 3, 4], target = 5 Output: -1

### Is linear search suitable for very large arrays?

Linear search is not ideal for large datasets because of its O(N) time complexity. For unsorted arrays, it's often the only choice. However, for sorted arrays, use binary search (O(log N)) to improve efficiency. Alternatively, hash-based methods (O(1) average case) can be used if the data structure supports it.

## Follow-ups

### How would you modify the function to return all indices of the target instead of just the smallest?

To return all indices: Traverse the array completely, even after finding the first occurrence. Use a list to store indices of all occurrences of the target. Example: Input: nums = [1, 2, 3, 2, 4], target = 2 Output: [1, 3]

### How can linear search be optimized for specific scenarios?

Linear search can be optimized for: If a specific target appears frequently, keep track of its last found index to start the search from there in subsequent searches. If the array is partially sorted or has a specific pattern, consider stopping early when certain conditions are met.

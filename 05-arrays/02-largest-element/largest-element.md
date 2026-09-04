---
title: "Largest Element"
summary: "Return the value of the largest element in an array."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Largest Element

Given an array of integers nums, return the value of the largest element in the array.

### Example 1

> - **Input :** nums = [3, 3, 6, 1]
> - **Output :** 6
> - **Explanation :**
> The largest element in array is 6.

### Example 2

> - **Input :** nums = [3, 3, 0, 99, -40]
> - **Output :** 99
> - **Explanation :**
> The largest element in array is 99.

## Constraints

> - `1 <= nums.length <= 10⁵`
> - `-10⁴ <= nums[i] <= 10⁴`
> - `nums may contain duplicate elements.`

```python run
from typing import List

class Solution:
    # Function to find the largest element in the array
    def largestElement(self, nums: List[int]) -> int:
        # Your code goes here.
        return 0


# Reads the test case's nums, e.g. [3, 3, 6, 1]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().largestElement(nums))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the largest element in the array
        int largestElement(int[] nums) {
            // Your code goes here.
            return 0;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [3, 3, 6, 1]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().largestElement(nums));
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

### How does the algorithm behave if there are multiple occurrences of the largest element?

The algorithm still works correctly. It will identify the first occurrence of the largest element, but since the value remains the same, it doesn't matter which occurrence is tracked. Example: Input: nums = [3, 5, 2, 5, 1] Output: 5

### How does the algorithm handle arrays with all negative numbers?

The algorithm works the same way with negative numbers. It starts with the first element as the largest and updates it whenever a larger (less negative) number is found. Example: Input: nums = [-3, -1, -7, -2] Output: -1

## Follow-ups

### How would you handle an empty array or invalid input?

Check if the array is empty at the beginning. If it is, return a specific value (e.g., None) or raise an error. Example: Input: nums = [] Output: None or raise a "ValueError: Array is empty"

### How would you modify the algorithm to return both the largest element and its index?

Use a loop to track both the value and the index of the largest element. Update the index whenever the largest value is updated. Example: Input: nums = [1, 3, 5, 2] Output: (5, 2) (Value = 5, Index = 2)

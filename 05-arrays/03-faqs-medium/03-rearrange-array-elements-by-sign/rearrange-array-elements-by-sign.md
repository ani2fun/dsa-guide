---
title: "Rearrange Array Elements By Sign"
summary: "Rearrange an array of equal positive and negative counts so signs alternate, starting positive."
essential: true
kind: problem
difficulty: medium
topics: [arrays]
---

# Rearrange Array Elements By Sign

Given an integer array nums of even length consisting of an equal number of positive and negative integers. Return the answer array in such a way that the given conditions are met:

- Every consecutive pair of integers have opposite signs.
- For all integers with the same sign, the order in which they were present in nums is preserved.
- The rearranged array begins with a positive integer.

### Example 1

> - **Input :** nums = [2, 4, 5, -1, -3, -4]
> - **Output :** [2, -1, 4, -3, 5, -4]
> - **Explanation :**
> The positive number 2, 4, 5 maintain their relative positions and -1, -3, -4 maintain their relative positions.

### Example 2

> - **Input :** nums = [1, -1, -3, -4, 2, 3]
> - **Output :** [1, -1, 2, -3, 3, -4]
> - **Explanation :**
> The positive number 1, 2, 3 maintain their relative positions and -1, -3, -4 maintain their relative positions.

## Constraints

> - `2 <= nums.length <= 10⁵`
> - `1 <= |nums[i]| <= 10⁴`
> - `nums.length is an even number.`
> - `Number of positive and negative numbers are equal.`

```python run
from typing import List

class Solution:
    # Function to rearrange the given array by signs
    def rearrangeArray(self, nums: List[int]) -> List[int]:
        # Your code goes here.
        return []


# Reads the test case's nums, e.g. [2, 4, 5, -1, -3, -4]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().rearrangeArray(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to rearrange the given array by signs
        int[] rearrangeArray(int[] nums) {
            // Your code goes here.
            return new int[0];
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [2, 4, 5, -1, -3, -4]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().rearrangeArray(nums)));
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

### How does the algorithm ensure the order of positives and negatives is preserved?

The algorithm processes positives and negatives in the order they appear in the original array by iterating over the separated positive and negative arrays without modifying their relative order.

### How does the algorithm handle edge cases like duplicates?

The algorithm treats duplicate integers the same as other integers, preserving their order during separation and merging. Duplicates do not affect the correctness of the alternation.

## Follow-ups

### How would you modify the algorithm to handle uneven counts of positives and negatives?

If the counts are uneven: Fill the result array with as many alternating pairs as possible. Append the remaining elements (all positives or all negatives) to the end of the result array while preserving their order.

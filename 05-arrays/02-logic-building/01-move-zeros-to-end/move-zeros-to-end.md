---
title: "Move Zeros to End"
summary: "Push all zeros in an array to the end in place, keeping the other elements' relative order."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Move Zeros to End

Given an integer array nums, move all the 0's to the end of the array. The relative order of the other elements must remain the same.

This must be done in place, without making a copy of the array.

### Example 1

> - **Input :** nums = [0, 1, 4, 0, 5, 2]
> - **Output :** [1, 4, 5, 2, 0, 0]
> - **Explanation :**
> Both the zeroes are moved to the end and the order of the other elements stay the same.

### Example 2

> - **Input :** nums = [0, 0, 0, 1, 3, -2]
> - **Output :** [1, 3, -2, 0, 0, 0]
> - **Explanation :**
> All 3 zeroes are moved to the end and the order of the other elements stay the same.

### Example 3

> - **Input :** nums = [0, 20, 0, -20, 0, 20]
> - **Output :** [20, -20, 20, 0, 0, 0]

## Constraints

> - `1 <= nums.length <= 10⁵`
> - `-10⁴ <= nums[i] <= 10⁴`

```python run
from typing import List

class Solution:
    # Function to move all zeroes to the end, in place
    def moveZeroes(self, nums: List[int]) -> None:
        # Your code goes here.
        pass


# Reads the test case's nums, e.g. [0, 1, 4, 0, 5, 2]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
Solution().moveZeroes(nums)
print("[" + ", ".join(str(x) for x in nums) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to move all zeroes to the end, in place
        void moveZeroes(int[] nums) {
            // Your code goes here.
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 1, 4, 0, 5, 2]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        new Solution().moveZeroes(nums);
        System.out.println(Arrays.toString(nums));
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

### What ensures the relative order of non-zero elements is preserved?

By iterating from left to right and moving each non-zero element to the next available position, the algorithm keeps their original sequence intact. Zeros are moved to the end only after all non-zero elements are correctly positioned, ensuring relative order remains unchanged.

### Can this logic be generalized for multi-dimensional arrays?

The same principle can be extended to multi-dimensional arrays, but it must be applied consistently row-wise or column-wise depending on the problem's definition of "end." Preserving relative order in higher dimensions requires careful handling, usually with nested loops or recursion, to ensure elements maintain their intended sequence within each sub-structure.

## Follow-ups

### How would you modify the algorithm to move all zeros to the beginning instead?

To move zeros to the beginning: Iterate through the array from right to left. Shift non-zero elements to the rightmost available position, and place zeros at the beginning. This maintains the relative order of non-zero elements.

### How can you adapt this algorithm for other conditions, like moving all negative numbers to the end?

Instead of checking for zeros, modify the condition to identify negative numbers. Use the same two-pointer approach to shift non-negative numbers to the front while maintaining their order.

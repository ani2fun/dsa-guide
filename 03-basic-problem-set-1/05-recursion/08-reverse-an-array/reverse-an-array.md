---
title: "Reverse An Array"
summary: "Reverse an array of integers in place, using recursion."
essential: true
kind: problem
difficulty: easy
topics: [recursion, arrays]
---

# Reverse An Array

Given an array nums of n integers, return reverse of the array.

### Example 1

> - **Input :** nums = [1, 2, 3, 4, 5]
> - **Output :** [5, 4, 3, 2, 1]

### Example 2

> - **Input :** nums = [1, 3, 3, 3, 5]
> - **Output :** [5, 3, 3, 3, 1]

### Example 3

> - **Input :** nums = [1, 2, 1]
> - **Output :** [1, 2, 1]

## Constraints

> - `1 <= n <= 100`
> - `1 <= nums[i] <= 100`

```python run
from typing import List

class Solution:
    # Function to reverse the given array in place, using recursion
    def reverseArray(self, nums: List[int]) -> List[int]:
        # Your code goes here.
        return nums


# Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().reverseArray(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to reverse the given array in place, using recursion
        int[] reverseArray(int[] nums) {
            // Your code goes here.
            return nums;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().reverseArray(nums)));
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

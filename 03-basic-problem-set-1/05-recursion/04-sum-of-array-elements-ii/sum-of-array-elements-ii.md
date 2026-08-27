---
title: "Sum Of Array Elements II"
summary: "Return the sum of an array's elements using recursion."
essential: true
kind: problem
difficulty: easy
topics: [recursion, arrays]
---

# Sum Of Array Elements II

Given an array nums, find the sum of elements of array using recursion.

### Example 1

> - **Input :** nums = [1, 2, 3]
> - **Output :** 6
> - **Explanation :**
> The sum of elements of array is 1 + 2 + 3 => 6.

### Example 2

> - **Input :** nums = [5, 8, 1]
> - **Output :** 14
> - **Explanation :**
> The sum of elements of array is 5 + 8 + 1 => 14.

### Example 3

> - **Input :** nums = [12, 9, 17]
> - **Output :** 38

## Constraints

> - `1 <= n <= 100`
> - `1 <= nums[i] <= 100`

```python run
from typing import List

class Solution:
    # Function to find the sum of the array's elements using recursion
    def arraySum(self, nums: List[int]) -> int:
        # Your code goes here.
        pass


# Reads the test case's nums, e.g. [1, 2, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().arraySum(nums))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the sum of the array's elements using recursion
        int arraySum(int[] nums) {
            // Your code goes here.
            return 0;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [1, 2, 3]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().arraySum(nums));
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

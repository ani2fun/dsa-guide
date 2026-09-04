---
title: "Find Missing Number"
summary: "Find the one number missing from an array holding n distinct values in the range 0 to n."
essential: true
kind: problem
difficulty: easy
topics: [arrays, maths]
---

# Find Missing Number

Given an integer array of size n containing distinct values in the range from 0 to n (inclusive), return the only number missing from the array within this range.

### Example 1

> - **Input :** nums = [0, 2, 3, 1, 4]
> - **Output :** 5
> - **Explanation :**
> nums contains 0, 1, 2, 3, 4 thus leaving 5 as the only missing number in the range [0, 5].

### Example 2

> - **Input :** nums = [0, 1, 2, 4, 5, 6]
> - **Output :** 3
> - **Explanation :**
> nums contains 0, 1, 2, 4, 5, 6 thus leaving 3 as the only missing number in the range [0, 6].

### Example 3

> - **Input :** nums = [1, 3, 6, 4, 2, 5]
> - **Output :** 0

## Constraints

> - `n == nums.length`
> - `1 <= n <= 10⁴`
> - `0 <= nums[i] <= n`
> - `All the numbers of nums are unique.`

```python run
from typing import List

class Solution:
    # Function to find the missing number
    def missingNumber(self, nums: List[int]) -> int:
        # Your code goes here.
        return -1


# Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().missingNumber(nums))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the missing number
        int missingNumber(int[] nums) {
            // Your code goes here.
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().missingNumber(nums));
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

### Why use the sum formula instead of iterative checks?

The sum formula is faster (O(N)) compared to iterative checks (O(N²)) because the sum formula requires only a single pass to compute the sum of array elements and one subtraction. Iterative checks require comparing each number in the range to the array, which is inefficient.

### What happens if the missing number is 0 or n?

If 0 is missing, the sum formula still works because the expected sum includes 0 by definition. If n is missing, the sum formula accounts for n since it calculates the sum of the entire range, and subtracting the array sum leaves n.

## Follow-ups

### How would you handle the problem if duplicates are allowed in the array?

If duplicates are allowed: Use a hash set to track numbers present in the array. Iterate through 0 to n, checking if each number exists in the set. This approach requires O(N) time and O(N) space.

### How does the performance compare between the sum formula and XOR methods?

Both methods have O(N) time complexity and O(1) space complexity. The sum formula involves addition and subtraction, while the XOR method uses bitwise operations. XOR is slightly faster in practice due to the lower computational cost of bitwise operations.

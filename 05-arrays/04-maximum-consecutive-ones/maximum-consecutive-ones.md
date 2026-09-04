---
title: "Maximum Consecutive Ones"
summary: "Return the length of the longest run of consecutive 1s in a binary array."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Maximum Consecutive Ones

Given a binary array nums, return the maximum number of consecutive 1s in the array.

A binary array is an array that contains only 0s and 1s.

### Example 1

> - **Input :** nums = [1, 1, 0, 0, 1, 1, 1, 0]
> - **Output :** 3
> - **Explanation :**
> The maximum consecutive 1s are present from index 4 to index 6, amounting to 3 1s.

### Example 2

> - **Input :** nums = [0, 0, 0, 0, 0, 0, 0, 0]
> - **Output :** 0
> - **Explanation :**
> No 1s are present in nums, thus we return 0.

### Example 3

> - **Input :** nums = [1, 0, 1, 1, 1, 0, 1, 1, 1]
> - **Output :** 3

## Constraints

> - `1 <= nums.length <= 10⁵`
> - `nums[i] is either 0 or 1.`

```python run
from typing import List

class Solution:
    # Function to find the length of the longest run of 1s
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        # Your code goes here.
        return 0


# Reads the test case's nums, e.g. [1, 1, 0, 0, 1, 1, 1, 0]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().findMaxConsecutiveOnes(nums))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the length of the longest run of 1s
        int findMaxConsecutiveOnes(int[] nums) {
            // Your code goes here.
            return 0;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [1, 1, 0, 0, 1, 1, 1, 0]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().findMaxConsecutiveOnes(nums));
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

### What is the time complexity, and can it be optimized further?

The time complexity of the solution is O(N), where N is the length of the array. This is optimal as each element must be inspected at least once to determine the number of consecutive 1s. It cannot be optimized further without additional assumptions about the input.

## Follow-ups

### How would you modify the algorithm to return the indices of the maximum segment of consecutive 1s?

Track the starting index of each segment of consecutive 1s. Update the start and end indices whenever a new maximum is found. Example: Input: nums = [1, 1, 0, 1, 1, 1, 0] Output: Indices (3, 5)

### How would you handle a streaming input (data arriving one bit at a time)?

For streaming data, maintain a running count of consecutive 1s and update the maximum whenever a 0 is encountered. Use a single variable to track the current count. Update the maximum count dynamically without storing the full array. Example: Stream: [1, 1, 0, 1, 1, 1, 0] Output after processing: 3

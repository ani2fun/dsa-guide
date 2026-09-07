---
title: "Majority Element I"
summary: "Find the array element that appears more than n/2 times."
essential: true
kind: problem
difficulty: medium
topics: [arrays]
---

# Majority Element I

Given an integer array nums of size n, return the majority element of the array.

The majority element of an array is an element that appears more than n/2 times in the array. The array is guaranteed to have a majority element.

### Example 1

> - **Input :** nums = [7, 0, 0, 1, 7, 7, 2, 7, 7]
> - **Output :** 7
> - **Explanation :**
> The number 7 appears 5 times in the 9 sized array.

### Example 2

> - **Input :** nums = [1, 1, 1, 2, 1, 2]
> - **Output :** 1
> - **Explanation :**
> The number 1 appears 4 times in the 6 sized array.

### Example 3

> - **Input :** nums = [-1, -1, -1, -1]
> - **Output :** -1

## Constraints

> - `n == nums.length.`
> - `1 <= n <= 10⁵`
> - `-10⁴ <= nums[i] <= 10⁴`
> - `One value appears more than n/2 times.`

```python run
from typing import List

class Solution:
    # Function to find the majority element in an array
    def majorityElement(self, nums: List[int]) -> int:
        # Your code goes here.
        return -1


# Reads the test case's nums, e.g. [7, 0, 0, 1, 7, 7, 2, 7, 7]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().majorityElement(nums))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the majority element in an array
        int majorityElement(int[] nums) {
            // Your code goes here.
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [7, 0, 0, 1, 7, 7, 2, 7, 7]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().majorityElement(nums));
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

### Why does the Boyer-Moore algorithm work?

The majority element always dominates other numbers, so it cancels out non-majority elements when counting. Even if count resets, the majority element eventually overtakes.

### Why does sorting work?

Since the majority element appears more than n/2 times, it will always be at nums[n/2] in a sorted array.

## Follow-ups

### How would you modify this to find all elements appearing more than n/3 times?

Boyer-Moore extended approach: Use two candidates instead of one. Each valid candidate must appear more than n/3 times.

### Can this problem be solved using bitwise operations?

Yes, count each bit position and reconstruct the majority element.

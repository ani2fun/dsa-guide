---
title: "Remove Duplicates From Sorted Array"
summary: "Remove duplicates from a sorted array in place and return the count of unique elements."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Remove Duplicates From Sorted Array

Given an integer array nums sorted in non-decreasing order, remove all duplicates in-place so that each unique element appears only once.

Return the number of unique elements in the array.

If the number of unique elements be k, then, change the array nums such that the first k elements of nums contain the unique values in the order that they were present originally. The remaining elements, as well as the size of the array does not matter in terms of correctness — only the value you return is checked.

An array sorted in non-decreasing order is an array where every element to the right of an element is either equal to or greater in value than that element.

### Example 1

> - **Input :** nums = [0, 0, 3, 3, 5, 6]
> - **Output :** 4
> - **Explanation :**
> Resulting array = [0, 3, 5, 6, _, _]. There are 4 distinct elements in nums and the elements marked as _ can have any value.

### Example 2

> - **Input :** nums = [-2, 2, 4, 4, 4, 4, 5, 5]
> - **Output :** 4
> - **Explanation :**
> Resulting array = [-2, 2, 4, 5, _, _, _, _]. There are 4 distinct elements in nums and the elements marked as _ can have any value.

### Example 3

> - **Input :** nums = [-30, -30, 0, 0, 10, 20, 30, 30]
> - **Output :** 5
> - **Explanation :**
> Resulting array = [-30, 0, 10, 20, 30, _, _, _]. There are 5 distinct elements in nums and the elements marked as _ can have any value.

## Constraints

> - `1 <= nums.length <= 10⁵`
> - `-10⁴ <= nums[i] <= 10⁴`
> - `nums is sorted in non-decreasing order.`

```python run
from typing import List

class Solution:
    # Function to remove duplicates in place and return the count of unique elements
    def removeDuplicates(self, nums: List[int]) -> int:
        # Your code goes here.
        return 0


# Reads the test case's nums, e.g. [0, 0, 3, 3, 5, 6]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().removeDuplicates(nums))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to remove duplicates in place and return the count of unique elements
        int removeDuplicates(int[] nums) {
            // Your code goes here.
            return 0;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 0, 3, 3, 5, 6]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().removeDuplicates(nums));
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

### What happens to the remaining elements after placing the unique elements?

The problem specifies that the elements after the first k unique values (where k is the number of unique elements) are irrelevant. They do not need to be in any particular order or have specific values, as only the first k elements are considered part of the result.

## Follow-ups

### How would the solution change if the array was not sorted?

If the array was unsorted, the sorted property could not be used to identify duplicates in one pass. Instead: Sort the array first (O(N log N)), then apply the two-pointer technique. Alternatively, use a hash set to track seen elements, but this would require O(N) extra space.

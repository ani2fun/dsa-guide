---
title: "Check If The Array Is Sorted II"
summary: "Decide whether an array is sorted in non-decreasing order, using recursion."
essential: true
kind: problem
difficulty: easy
topics: [recursion, arrays]
---

# Check If The Array Is Sorted II

Given an array nums of n integers, return true if the array nums is sorted in non-decreasing order or else false.

### Example 1

> - **Input :** nums = [1, 2, 3, 4, 5]
> - **Output :** true
> - **Explanation :**
> For all i (1 <= i <= 4) it holds nums[i] <= nums[i+1], hence it is sorted and we return true.

### Example 2

> - **Input :** nums = [1, 2, 1, 4, 5]
> - **Output :** false
> - **Explanation :**
> For i == 2 it does not hold nums[i] <= nums[i+1], hence it is not sorted and we return false.

### Example 3

> - **Input :** nums = [1, 9, 6, 8, 5, 4, 0]
> - **Output :** false

## Constraints

> - `1 <= n <= 100`
> - `1 <= nums[i] <= 100`

```python run
from typing import List

class Solution:
    # Function to check if the array is sorted in non-decreasing order, using recursion
    def isSorted(self, nums: List[int]) -> bool:
        # Your code goes here.
        pass


# Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print("true" if Solution().isSorted(nums) else "false")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to check if the array is sorted in non-decreasing order, using recursion
        boolean isSorted(ArrayList<Integer> nums) {
            // Your code goes here.
            return false;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
        ArrayList<Integer> nums = parseIntList(new Scanner(System.in).nextLine());
        System.out.println(new Solution().isSorted(nums));
    }

    // "[1, 2, 3]" -> [1, 2, 3]
    static ArrayList<Integer> parseIntList(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        ArrayList<Integer> out = new ArrayList<>();
        if (inner.isEmpty()) return out;
        for (String part : inner.split(",")) out.add(Integer.parseInt(part.trim()));
        return out;
    }
}
```

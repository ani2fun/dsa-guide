---
title: "Selection Sort"
summary: "Sort an array in non-decreasing order using the selection sort algorithm."
essential: true
kind: problem
difficulty: easy
topics: [sorting, arrays]
---

# Selection Sort

Given an array of integers nums, sort the array in non-decreasing order using the selection sort algorithm and return the sorted array.

A sorted array in non-decreasing order is an array where each element is greater than or equal to all previous elements in the array.

### Example 1

> - **Input :** nums = [7, 4, 1, 5, 3]
> - **Output :** [1, 3, 4, 5, 7]
> - **Explanation :**
> 1 <= 3 <= 4 <= 5 <= 7. Thus the array is sorted in non-decreasing order.

### Example 2

> - **Input :** nums = [5, 4, 4, 1, 1]
> - **Output :** [1, 1, 4, 4, 5]
> - **Explanation :**
> 1 <= 1 <= 4 <= 4 <= 5. Thus the array is sorted in non-decreasing order.

### Example 3

> - **Input :** nums = [3, 2, 3, 4, 5]
> - **Output :** [2, 3, 3, 4, 5]

## Constraints

> - `1 <= nums.length <= 1000`
> - `-10⁴ <= nums[i] <= 10⁴`
> - `nums[i] may contain duplicate values.`

```python run
from typing import List

class Solution:
    # Function to sort the array using selection sort
    def selectionSort(self, nums: List[int]) -> List[int]:
        # Your code goes here.
        return nums


# Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().selectionSort(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to sort the array using selection sort
        int[] selectionSort(int[] nums) {
            // Your code goes here.
            return nums;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().selectionSort(nums)));
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

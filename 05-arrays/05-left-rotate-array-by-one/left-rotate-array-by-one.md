---
title: "Left Rotate Array by One"
summary: "Rotate an array one step to the left, in place."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Left Rotate Array by One

Given an integer array nums, rotate the array to the left by one.

Note: There is no need to return anything, just modify the given array.

### Example 1

> - **Input :** nums = [1, 2, 3, 4, 5]
> - **Output :** [2, 3, 4, 5, 1]
> - **Explanation :**
> Initially, nums = [1, 2, 3, 4, 5]. Rotating once to left -> nums = [2, 3, 4, 5, 1].

### Example 2

> - **Input :** nums = [-1, 0, 3, 6]
> - **Output :** [0, 3, 6, -1]
> - **Explanation :**
> Initially, nums = [-1, 0, 3, 6]. Rotating once to left -> nums = [0, 3, 6, -1].

### Example 3

> - **Input :** nums = [7, 6, 5, 4]
> - **Output :** [6, 5, 4, 7]

## Constraints

> - `1 <= nums.length <= 10⁵`
> - `-10⁴ <= nums[i] <= 10⁴`

```python run
from typing import List

class Solution:
    # Function to rotate the array one step to the left, in place
    def rotateArrayByOne(self, nums: List[int]) -> None:
        # Your code goes here.
        pass


# Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
Solution().rotateArrayByOne(nums)
print("[" + ", ".join(str(x) for x in nums) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to rotate the array one step to the left, in place
        void rotateArrayByOne(int[] nums) {
            // Your code goes here.
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        new Solution().rotateArrayByOne(nums);
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

### Can this logic handle nested arrays or complex objects?

Yes, the logic applies to arrays of any type. For complex objects, ensure that only references are moved and no deep copying is unintentionally triggered.

### How can you validate correctness across various test cases?

Validation involves testing:
- Empty arrays: Output should remain empty.
- Single-element arrays: Output should remain unchanged.
- Arrays with duplicates: Check that all duplicates are correctly preserved and shifted.
- Arrays with mixed values: Ensure the logic handles all types of elements consistently.

## Follow-ups

### How would the algorithm handle multidimensional arrays?

For multidimensional arrays (e.g., matrices), rotation involves more complex transformations:
- Left Rotation: Shifting rows or columns depending on the axis of rotation.
- Right Rotation: Similar logic but reversed.

### What is the difference between in-place rotation and using extra space?

In-Place Rotation: Rearranges elements directly in the original array without using additional memory. It is more space-efficient but often requires more careful handling of indices. Using Extra Space: Creates a temporary array to hold shifted elements, simplifying the process but increasing memory usage.

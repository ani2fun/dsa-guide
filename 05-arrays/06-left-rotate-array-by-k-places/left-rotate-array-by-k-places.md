---
title: "Left Rotate Array by K Places"
summary: "Rotate an array k steps to the left, in place."
essential: true
kind: problem
difficulty: medium
topics: [arrays]
---

# Left Rotate Array by K Places

Given an integer array nums and a non-negative integer k, rotate the array to the left by k steps.

### Example 1

> - **Input :** nums = [1, 2, 3, 4, 5, 6], k = 2
> - **Output :** [3, 4, 5, 6, 1, 2]
> - **Explanation :**
> rotate 1 step to the left: [2, 3, 4, 5, 6, 1]. rotate 2 steps to the left: [3, 4, 5, 6, 1, 2].

### Example 2

> - **Input :** nums = [3, 4, 1, 5, 3, -5], k = 8
> - **Output :** [1, 5, 3, -5, 3, 4]
> - **Explanation :**
> rotate 1 step to the left: [4, 1, 5, 3, -5, 3]
> rotate 2 steps to the left: [1, 5, 3, -5, 3, 4]
> rotate 3 steps to the left: [5, 3, -5, 3, 4, 1]
> rotate 4 steps to the left: [3, -5, 3, 4, 1, 5]
> rotate 5 steps to the left: [-5, 3, 4, 1, 5, 3]
> rotate 6 steps to the left: [3, 4, 1, 5, 3, -5]
> rotate 7 steps to the left: [4, 1, 5, 3, -5, 3]
> rotate 8 steps to the left: [1, 5, 3, -5, 3, 4]

## Constraints

> - `1 <= nums.length <= 10⁵`
> - `-10⁴ <= nums[i] <= 10⁴`
> - `0 <= k <= 10⁵`

```python run
from typing import List

class Solution:
    # Function to rotate the array k steps to the left, in place
    def rotateArray(self, nums: List[int], k: int) -> None:
        # Your code goes here.
        pass


# Reads the test case's nums and k, one per line
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
k = int(input())
Solution().rotateArray(nums, k)
print("[" + ", ".join(str(x) for x in nums) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to rotate the array k steps to the left, in place
        void rotateArray(int[] nums, int k) {
            // Your code goes here.
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums and k, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums = parseIntArray(sc.nextLine());
        int k = Integer.parseInt(sc.nextLine().trim());
        new Solution().rotateArray(nums, k);
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

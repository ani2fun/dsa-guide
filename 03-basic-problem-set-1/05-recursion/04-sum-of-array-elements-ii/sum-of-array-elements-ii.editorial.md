## Intuition

Computing the sum of an array's elements through recursion involves thinking about adding the first element to the sum of the rest. This process continues by recursively considering one element at a time, gradually reducing the array until reaching the point where no elements are left to add.

## Approach

1. Define a recursive helper function sum(nums, left) where nums is the array and left is the current index.
2. In the helper function — base case: if the left index is out of bounds (i.e., left >= nums.length), return 0 because there are no more elements to add. Recursive case: add the current element nums[left] to the sum of the remaining elements, obtained by recursively calling the function with the next index left + 1.
3. The initial call to the helper function is made from the main function with the starting index 0.

## Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    # Function to find the sum of the array's elements using recursion
    def arraySum(self, nums: List[int]) -> int:
        # Start from index 0
        return self.sum(nums, 0)

    def sum(self, nums: List[int], left: int) -> int:
        # Base case: out of bounds
        if left >= len(nums):
            return 0
        # Add current element and recurse
        return nums[left] + self.sum(nums, left + 1)


# Reads the test case's nums, e.g. [1, 2, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().arraySum(nums))
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the sum of the array's elements using recursion
        public int arraySum(int[] nums) {
            // Start from index 0
            return sum(nums, 0);
        }

        private int sum(int[] nums, int left) {
            // Base case: out of bounds
            if (left >= nums.length) {
                return 0;
            }
            // Add current element and recurse
            return nums[left] + sum(nums, left + 1);
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

## Complexity Analysis

- **Time Complexity:** O(N) — each element in the array is processed exactly once.
- **Space Complexity:** O(N) — due to the recursion stack, which can grow up to the size of the array.

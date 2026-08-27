## Intuition

The concept of reversing an array involves swapping elements from both ends, moving towards the center. Recursion facilitates this by initially swapping the first and last elements, then progressively moving inward until the pointers converge at the center.

## Approach

1. Start with two pointers p1 and p2, for example: one at the beginning of the array and one at the end. Swap the elements at these two pointers.
2. Move the left pointer one step to the right and the right pointer one step to the left. Repeat the swap operation until the two pointers meet or cross each other.
3. Post swapping, call the recursion to perform the same operations again on the next pair of elements.
4. Return the reversed array.

## Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    def reverseArray(self, nums: List[int]) -> List[int]:
        # Call the helper function to reverse the array
        self.reverse(nums, 0, len(nums) - 1)
        # Return the reversed array
        return nums

    def reverse(self, nums: List[int], left: int, right: int) -> None:
        if left >= right:
            return
        # Swap the elements
        nums[left], nums[right] = nums[right], nums[left]
        # Recursive call with updated pointers
        self.reverse(nums, left + 1, right - 1)


# Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().reverseArray(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        public int[] reverseArray(int[] nums) {
            // Call the helper function to reverse the array
            reverse(nums, 0, nums.length - 1);
            // Return the reversed array
            return nums;
        }

        private void reverse(int[] nums, int left, int right) {
            // Base case: pointers have crossed, the array is reversed
            if (left >= right) {
                return;
            }
            // Swap the elements
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            // Recursive call with updated pointers
            reverse(nums, left + 1, right - 1);
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().reverseArray(nums)));
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

- **Time Complexity:** O(N) — a constant-time swap is performed for each element pair, so the recursion makes N/2 calls for an array of N elements.
- **Space Complexity:** O(N) — the swaps happen in place, but the recursion stack grows to a depth of N/2 before the base case unwinds it.

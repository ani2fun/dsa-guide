## Intuition

To determine if an array is sorted in non-decreasing order using recursion, consider comparing each element with the one following it. If an element exceeds the next one, the array is not sorted. This comparison is then repeated for the entire array.

## Approach

1. If the array has 0 or 1 elements, it is already sorted. So, return true.
2. Use a helper function sort that takes the array and two pointers, left and right, to compare elements.
3. In the helper function, check if the array is sorted by comparing elements at the left and right pointers; if right reaches the end of the array, the array is sorted, so return true; if the element at left is greater than the element at right, return false because the array is not sorted; otherwise, move both pointers to the next elements and call the helper function recursively.

## Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    def isSorted(self, nums: List[int]) -> bool:
        # Ensure nums is a list to use len() function
        nums = list(nums)
        # An array with 0 or 1 element is always considered sorted
        if len(nums) <= 1:
            return True
        # Check if the array is sorted starting from index 0 to 1
        return self.sort(nums, 0, 1)

    def sort(self, nums: List[int], left: int, right: int) -> bool:
        # If we reach the end of the array
        # it means the array is sorted
        if right >= len(nums):
            return True
        # If we find a pair where the left element is greater than the right
        # the array is not sorted
        if nums[left] > nums[right]:
            return False
        # Move to the next pair of elements
        return self.sort(nums, left + 1, right + 1)


# Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print("true" if Solution().isSorted(nums) else "false")
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        public boolean isSorted(ArrayList<Integer> nums) {
            // An array with 0 or 1 element is always considered sorted
            if (nums.size() <= 1) {
                return true;
            }
            // Check if the array is sorted starting from index 0 to 1
            return sort(nums, 0, 1);
        }

        private boolean sort(ArrayList<Integer> nums, int left, int right) {
            // If we reach the end of the array
            // it means the array is sorted
            if (right >= nums.size()) {
                return true;
            }
            // If we find a pair where the left element is greater than the right
            // the array is not sorted
            if (nums.get(left) > nums.get(right)) {
                return false;
            }
            // Move to the next pair of elements
            return sort(nums, left + 1, right + 1);
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

## Complexity Analysis

- **Time Complexity:** O(N) — the helper function makes a recursive call for each element in the array, moving from the beginning to the end of the array.
- **Space Complexity:** O(N) — due to the recursion stack. Each recursive call adds a new frame to the call stack, and in the worst case, there will be N frames on the stack (one for each call).

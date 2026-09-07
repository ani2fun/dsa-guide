## Intuition

- Sorts an array by repeatedly finding the minimum element from the unsorted part and putting it at the beginning.
- The largest element will end up at the last index of the array.

## Approach

1. **Select the starting index** of the unsorted part using an outer loop with `i` from `0` to `n-2` (since the final element will automatically be in its correct sorted position).
2. **Assume the current element is the minimum** by setting `min_index = i`.
3. **Find the actual smallest element** in the remaining unsorted portion by using an inner loop with `j` from `i + 1` to `n - 1`. If a smaller element is found, update the `min_index`.
4. **Swap the elements** at index `i` and `min_index`, but *only if* the `min_index` has changed from `i` (this avoids unnecessary swaps).
5. **Repeat the process** for the next starting index until the entire array is sorted.

## Solution

```python solution time=O(N²) space=O(1)
from typing import List

class Solution:
    def selectionSort(self, nums: List[int]) -> List[int]:
        # Loop through unsorted part
        # of the array (0 to n-2)
        for i in range(len(nums) - 1):
            # Assume current element is minimum hence we can take the current index and assign it to variable to track minimum index of an element.
            min_index = i

            # Find minimum element in unsorted part (i+1 to n-1) and take it's index.
            # `j` begin with next index of `i` and traverse backwards to reach until 0 to find the minimum element and store mini_index
            for j in range(i + 1, len(nums)):
                if nums[j] < nums[min_index]:
                    min_index = j

            # Swap only if minIndex changed (optimization)
            # Skipping the swap when min_index == i avoids a wasted no-op write. This pays off most
            # when the array is already sorted, since every pass would otherwise perform a needless
            # self-swap. It does not reduce comparisons or enable early exit — the minimum-search
            # still scans the full unsorted portion on every pass, regardless of order.
            if min_index != i:
                nums[i], nums[min_index] = nums[min_index], nums[i]

        return nums

# -- Driver Code
# Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().selectionSort(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N²) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        public int[] selectionSort(int[] nums) {
            // Loop through unsorted part of the array (0 to n-2)
            for (int i = 0; i < nums.length - 1; i++) {
                /*Assume current element
                is the minimum*/
                int minIndex = i;

                // Find actual minimum in unsorted part (i+1 to n-1)
                for (int j = i + 1; j < nums.length; j++) {
                    if (nums[j] < nums[minIndex]) {
                        minIndex = j;
                    }
                }

                // Swap only if minIndex changed
                if (minIndex != i) {
                    int temp = nums[i];
                    nums[i] = nums[minIndex];
                    nums[minIndex] = temp;
                }
            }

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

## Complexity Analysis

- **Time Complexity:** O(N²) — where N is the length of the input array. The outer loop runs through each element, and the inner loop finds the smallest element in the unsorted portion of the array.
- **Space Complexity:** O(1) — as it is an in-place sorting algorithm and does not require additional storage proportional to the input size.

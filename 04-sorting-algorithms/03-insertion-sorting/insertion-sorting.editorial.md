## Intuition

Sorts an array one element at a time by repeatedly picking the next element and inserting it at its correct position within the already sorted part of the array.

## Approach

1. In each iteration, select an element from the unsorted part of the array using an outer loop.
2. Place this element in its correct position within the sorted part of the array.
3. Use an inner loop to shift the remaining elements as necessary to accommodate the selected element. This involves shifting the elements by one place until the selected element can be placed at its correct position.
4. Continue this process until the entire array is sorted.

## Solution

```python solution time=O(N²) space=O(1)
from typing import List

class Solution:
    # Function to sort the array using insertion sort
    def insertionSort(self, nums: List[int]) -> List[int]:
        n = len(nums) # Size of the array

        # For every element in the array
        for i in range(1, n):
            key = nums[i] # Current element as key
            j = i - 1

            # Shift elements that are greater than key by one position
            while j >= 0 and nums[j] > key:
                nums[j + 1] = nums[j]
                j -= 1

            nums[j + 1] = key # Insert key at correct position

        return nums


# Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().insertionSort(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N²) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        public int[] insertionSort(int[] nums) {
            int n = nums.length; // Size of the array

            // For every element in the array
            for (int i = 1; i < n; i++) {
                int key = nums[i]; // Current element as key
                int j = i - 1;

                // Shift elements that are greater than key by one position
                while (j >= 0 && nums[j] > key) {
                    nums[j + 1] = nums[j];
                    j--;
                }

                nums[j + 1] = key; // Insert key at correct position
            }

            return nums;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().insertionSort(nums)));
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

- **Time Complexity:** O(N²) — for the worst and average cases, where N is the size of the array. This is because the outer loop runs N times, and for each pass, the inner loop runs up to N times as well, resulting in approximately N × N operations, hence O(N²). The best-case time complexity occurs when the array is already sorted, in which case the inner loop doesn't run at all, leading to a time complexity of O(N).
- **Space Complexity:** O(1) — because Insertion Sort is an in-place sorting algorithm, meaning it sorts the array by modifying the original array without using additional data structures that grow with the size of the input.

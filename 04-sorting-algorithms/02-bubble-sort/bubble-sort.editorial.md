## Intuition

- Sorts an array by repeatedly swapping adjacent elements if they are in the wrong order.
- The largest elements "bubble" to the end of the array with each pass.

## Approach

1. Run a loop i from n-1 to 0.
2. Run a nested loop from j from 0 to i-1.
3. If arr[j] > arr[j+1], swap them.
4. Continue until the array is sorted.

<div style="border-left:4px solid #15448e;background:rgba(21,68,142,0.08);padding:0.6rem 1rem;border-radius:0 0.5rem 0.5rem 0;margin:1.25rem 0">

📘 **Definition.** Here, after each iteration, the array becomes sorted up to the last index of the range. That is why the last index of the range decreases by 1 after each iteration. This decrement is managed by the outer loop, where the last index is represented by the variable i. The inner loop (variable j) helps to push the maximum element of the range [0...i] to the last index (i.e., index i).

</div>

## Solution

```python solution time=O(N²) space=O(1)
from typing import List

class Solution:
    # Bubble Sort Function
    def bubbleSort(self, nums: List[int]) -> List[int]:
        n = len(nums)
        # Traverse through the array
        for i in range(n - 1, -1, -1):
            # Track if swaps are made
            isSwapped = False
            for j in range(i):
                # Swap if next element is smaller
                if nums[j] > nums[j + 1]:
                    nums[j], nums[j + 1] = nums[j + 1], nums[j]
                    isSwapped = True
            ''' Break out of loop
             if no swaps done'''
            if not isSwapped:
                break
        return nums


# Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().bubbleSort(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N²) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Bubble Sort Function
        public int[] bubbleSort(int[] nums) {
            int n = nums.length;
            // Traverse through the array
            for (int i = n - 1; i >= 0; i--) {
                // Track if swaps are made
                boolean isSwapped = false;
                for (int j = 0; j <= i - 1; j++) {
                    // Swap if next element is smaller
                    if (nums[j] > nums[j + 1]) {
                        int temp = nums[j];
                        nums[j] = nums[j + 1];
                        nums[j + 1] = temp;
                        isSwapped = true;
                    }
                }
                /** Break out of loop
              if no swaps done*/
                if (!isSwapped) {
                    break;
                }
            }
            return nums;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().bubbleSort(nums)));
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

- **Time Complexity:** O(N²) — for the worst and average cases, and O(N) for the best case. Here, N is the size of the array.
- **Space Complexity:** O(1) — because Bubble Sort is an in-place sorting algorithm, meaning it only requires a constant amount of extra space for its operations, regardless of the size of the input array.

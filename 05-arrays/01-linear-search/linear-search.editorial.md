## Intuition

Let's break the problem statement into an example to understand it better. Imagine having a long shelf filled with books, and each book has a unique number written on its spine. The ask is to look for the first book with a specific number, let's say 2.

To achieve this we will simply start scanning each book and once a book with number 2 is got, stop the scan procedure.

## Approach

1. Traverse through the array, similar to the idea of scanning each book serially.
2. Check if the current element of array is equal to the target element. If so, return the index and stop scanning further.
3. In case target value is not found, return -1 marking that the target element missing.

## Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    # Linear Search Function
    def linearSearch(self, nums: List[int], target: int) -> int:
        # Traverse the entire array
        for i in range(len(nums)):

            # Check if current element is target
            if nums[i] == target:

                # Return index if target found
                return i

        # If target not found
        return -1


# Reads the test case's nums and target, one per line
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
target = int(input())
print(Solution().linearSearch(nums, target))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Linear Search Function
        public int linearSearch(int[] nums, int target) {
            // Traverse the entire array
            for (int i = 0; i < nums.length; i++) {

                // Check if current element is target
                if (nums[i] == target) {

                    // Return if target found
                    return i;

                }
            }
            // If target not found
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums and target, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums = parseIntArray(sc.nextLine());
        int target = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().linearSearch(nums, target));
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

- **Time Complexity:** O(N) — in worst case entire array will be traversed, taking a time of N where N is size of the array.
- **Space Complexity:** O(1) — as no additional space is used apart from the input array, the space complexity stays constant.

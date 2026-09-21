## Intuition

To rotate an array by one position to the left, consider that the first element of the array will move to the last position, while all other elements shift one position to the left.

The thought process involves first capturing the value of the first element in a temporary variable. Next, iterate through the array starting from the second element and shift each element to the position of its predecessor (previous element). Finally, place the initially captured value into the last position of the array. This approach ensures that the array is rotated by one position to the left effectively.

## Approach

1. Store the value of the first element of the array in a temporary variable.
2. Iterate through the array starting from the second element.
3. Shift each element one position to the left by assigning the current element to the position of its predecessor.
4. After completing the iteration, place the value from the temporary variable into the last position of the array.

## Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    def rotateArrayByOne(self, nums: List[int]) -> None:
        # Store the first element in a temporary variable
        temp = nums[0]

        # Shift elements to the left
        for i in range(1, len(nums)):
            nums[i - 1] = nums[i]

        # Place the first element at the end
        nums[-1] = temp


# Reads the test case's nums, e.g. [1, 2, 3, 4, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
Solution().rotateArrayByOne(nums)
print("[" + ", ".join(str(x) for x in nums) + "]")
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        void rotateArrayByOne(int[] nums) {
            // Store the first element in a temporary variable
            int temp = nums[0];

            // Shift elements to the left
            for (int i = 1; i < nums.length; i++) {
                nums[i - 1] = nums[i];
            }

            // Place the first element at the end
            nums[nums.length - 1] = temp;
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

## Complexity Analysis

- **Time Complexity:** O(N) — where N is the number of elements in the array. Each element is visited once during the iteration.
- **Space Complexity:** O(1). The space used does not depend on the size of the input array and remains constant.

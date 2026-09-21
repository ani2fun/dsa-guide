## Intuition

To find the number of maximum consecutive 1s, the idea is to count the number of 1s each time we encounter them and update the maximum number of 1s. On encountering any 0, reset the count to 0 again so as to count the next consecutive 1s.

## Approach

1. Initialize two variables, count and max_count to 0. Traverse the array and if the current element is 1, increment the count by 1.
2. Update max_count if count is greater than max_count.
3. If the current element is 0, reset the count variable to 0 and at last return max_count.

## Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        ''' Initialize count and max_count
              to track current and maximum consecutive 1s '''
        cnt = 0
        maxi = 0

        # Traverse the array
        for num in nums:
            # If the current element is 1, increment the count
            if num == 1:
                cnt += 1

                # Update maxi if current count is greater than maxi
                maxi = max(maxi, cnt)

            else:
                # If the current element is 0, reset the count
                cnt = 0

        # Return the maximum count of consecutive 1s
        return maxi


# Reads the test case's nums, e.g. [1, 1, 0, 0, 1, 1, 1, 0]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().findMaxConsecutiveOnes(nums))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        public int findMaxConsecutiveOnes(int[] nums) {
            /* Initialize count and max_count
                   to track current and maximum consecutive 1s */
            int cnt = 0;
            int maxi = 0;

            // Traverse the array
            for (int i = 0; i < nums.length; i++) {

                // If the current element is 1, increment the count
                if (nums[i] == 1) {
                    cnt++;

                    // Update maxi if current count is greater than maxi
                    maxi = Math.max(maxi, cnt);

                } else {
                    // If the current element is 0, reset the count
                    cnt = 0;
                }
            }
            // Return the maximum count of consecutive 1s
            return maxi;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [1, 1, 0, 0, 1, 1, 1, 0]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().findMaxConsecutiveOnes(nums));
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

- **Time Complexity:** O(N) — as there is single traversal of the array. Here N is the number of elements in the array.
- **Space Complexity:** O(1) — as no additional space is used.

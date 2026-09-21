## Intuition

A naive approach repeatedly applies the row/column formula from Pascal's Triangle I to find each element in the row — that costs O(n²) since it recomputes a value for every element in the nth row.

There's a pattern instead: each element in the row is derived from the one before it, `curr = (prev × (r−i)) / i`, where `prev` is the previous element in the row and `i` is the index of the element being computed. Using this formula, the whole row can be generated in O(n) time.

## Approach

1. Initialize a list sized to the given row number.
2. Set the first element of the row to 1 — the first element in every row of Pascal's Triangle is always 1.
3. Iterate through the row, computing each value from the previous one with the formula above.
4. Return the computed row.

## Solution

```python solution time=O(R) space=O(1)
from typing import List

class Solution:
    # Function to return the rth row of Pascal's Triangle
    def pascalTriangleII(self, r: int) -> List[int]:
        ans = [0] * r  # To store the answer

        # The first element of every row is 1
        ans[0] = 1

        # Compute each element from the one before it
        for i in range(1, r):
            ans[i] = (ans[i - 1] * (r - i)) // i

        return ans  # Return the result


# Reads the test case's r
r = int(input())
print(Solution().pascalTriangleII(r))
```

```java solution time=O(R) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the rth row of Pascal's Triangle
        int[] pascalTriangleII(int r) {
            int[] ans = new int[r]; // To store the answer

            // The first element of every row is 1
            ans[0] = 1;

            // Compute each element from the one before it
            for (int i = 1; i < r; i++) {
                ans[i] = (ans[i - 1] * (r - i)) / i;
            }

            return ans; // Return the result
        }
    }

    public static void main(String[] args) {
        // Reads the test case's r
        int r = Integer.parseInt(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().pascalTriangleII(r)));
    }
}
```

## Complexity Analysis

**Time Complexity:** O(R), where R is the given row number — a single loop runs R times doing constant-time work per iteration.

**Space Complexity:** O(1), as no extra space is used beyond the output. Counting the output itself, the space complexity is O(R), since the row stored is proportional to the row number.

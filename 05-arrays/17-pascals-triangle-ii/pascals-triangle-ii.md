---
title: "Pascal's Triangle II"
summary: "Return the full rth row (1-indexed) of Pascal's Triangle, in order."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Pascal's Triangle II

Given an integer r, return all the values in the rth row (1-indexed) of Pascal's Triangle, in order.

In Pascal's Triangle:

- The first row has one element, with a value of 1.
- Each row has one more element than the previous row.
- The value of each element is the sum of the elements directly above it.

### Example 1

> - **Input :** r = 4
> - **Output :** [1, 3, 3, 1]
> - **Explanation :**
> Row 4 of Pascal's Triangle is `1 3 3 1`, built as `1` → `1 1` → `1 2 1` → `1 3 3 1`.

### Example 2

> - **Input :** r = 5
> - **Output :** [1, 4, 6, 4, 1]
> - **Explanation :**
> Row 5 of Pascal's Triangle is `1 4 6 4 1`, built as `1` → `1 1` → `1 2 1` → `1 3 3 1` → `1 4 6 4 1`.

## Constraints

> - `1 <= r <= 30`
> - `All values will fit inside a 32-bit integer.`

```python run
from typing import List

class Solution:
    # Function to return the rth row of Pascal's Triangle
    def pascalTriangleII(self, r: int) -> List[int]:
        # Your code goes here.
        return []


# Reads the test case's r
r = int(input())
print(Solution().pascalTriangleII(r))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the rth row of Pascal's Triangle
        int[] pascalTriangleII(int r) {
            // Your code goes here.
            return new int[0];
        }
    }

    public static void main(String[] args) {
        // Reads the test case's r
        int r = Integer.parseInt(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().pascalTriangleII(r)));
    }
}
```

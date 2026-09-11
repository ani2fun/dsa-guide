---
title: "Pascal's Triangle I"
summary: "Return the value at a given row and column (1-indexed) in Pascal's Triangle."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Pascal's Triangle I

Given two integers r and c, return the value at the rth row and cth column (1-indexed) in Pascal's Triangle.

In Pascal's Triangle:

- The first row contains a single element, 1.
- Each row has one more element than the previous row.
- Every row starts and ends with 1.
- For all interior elements (not at the ends), the value at position (r, c) is the sum of the two elements directly above it from the previous row:

  `Pascal[r][c] = Pascal[r−1][c−1] + Pascal[r−1][c]`

  where indexing is 1-based.

### Example 1

> - **Input :** r = 4, c = 2
> - **Output :** 3
> - **Explanation :**
> Row 4 of Pascal's Triangle is `1 3 3 1` (built as `1` → `1 1` → `1 2 1` → `1 3 3 1`), so the value at row 4, column 2 is 3.

### Example 2

> - **Input :** r = 5, c = 3
> - **Output :** 6
> - **Explanation :**
> Row 5 of Pascal's Triangle is `1 4 6 4 1` (built as `1` → `1 1` → `1 2 1` → `1 3 3 1` → `1 4 6 4 1`), so the value at row 5, column 3 is 6.

## Constraints

> - `1 <= r, c <= 30`
> - `c <= r`
> - `All values will fit inside a 32-bit integer.`

```python run
class Solution:
    # Function to find the value at row r and column c in Pascal's Triangle
    def pascalTriangleI(self, r: int, c: int) -> int:
        # Your code goes here.
        return -1


# Reads the test case's r, then c
r = int(input())
c = int(input())
print(Solution().pascalTriangleI(r, c))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the value at row r and column c in Pascal's Triangle
        int pascalTriangleI(int r, int c) {
            // Your code goes here.
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's r, then c
        Scanner sc = new Scanner(System.in);
        int r = Integer.parseInt(sc.nextLine());
        int c = Integer.parseInt(sc.nextLine());
        System.out.println(new Solution().pascalTriangleI(r, c));
    }
}
```

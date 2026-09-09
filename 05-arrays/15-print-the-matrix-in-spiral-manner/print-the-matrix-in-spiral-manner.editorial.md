## Intuition

Use four boundary pointers — `top`, `bottom`, `left`, `right` — and shrink them inward one edge at a time: traverse the top row left to right, the right column top to bottom, the bottom row right to left, and the left column bottom to top, repeating until the boundaries cross.

## Approach

1. Initialize four variables: `top` as 0, `left` as 0, `bottom` as `totalRows - 1`, `right` as `totalColumns - 1`.
2. Iterate while `top <= bottom` and `left <= right`.
3. Move left to right along the top row, appending each element, then increment `top`.
4. Move top to bottom along the right column, appending each element, then decrement `right`.
5. If `top <= bottom`, move right to left along the bottom row, appending each element, then decrement `bottom`.
6. If `left <= right`, move bottom to top along the left column, appending each element, then increment `left`.
7. Return the collected answer.

## Solution

```python solution time=O(N×M) space=O(1)
from typing import List

class Solution:
    # Function to print matrix in spiral manner
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        ans = []

        # Number of rows
        n = len(matrix)

        # Number of columns
        m = len(matrix[0])

        # Initialize pointers for traversal
        top, left = 0, 0
        bottom, right = n - 1, m - 1

        # Traverse the matrix in spiral order
        while top <= bottom and left <= right:
            # Traverse from left to right
            for i in range(left, right + 1):
                ans.append(matrix[top][i])
            top += 1

            # Traverse from top to bottom
            for i in range(top, bottom + 1):
                ans.append(matrix[i][right])
            right -= 1

            # Traverse from right to left
            if top <= bottom:
                for i in range(right, left - 1, -1):
                    ans.append(matrix[bottom][i])
                bottom -= 1

            # Traverse from bottom to top
            if left <= right:
                for i in range(bottom, top - 1, -1):
                    ans.append(matrix[i][left])
                left += 1

        return ans


# Reads the test case's matrix, e.g. [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
inner = input().strip()[1:-1].strip()
rows = inner.split("], [") if inner else []
matrix = [[int(t) for t in r.strip("[]").split(",")] for r in rows]
print(Solution().spiralOrder(matrix))
```

```java solution time=O(N×M) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to print matrix in spiral manner
        List<Integer> spiralOrder(int[][] matrix) {
            List<Integer> ans = new ArrayList<>();

            // Number of rows
            int n = matrix.length;

            // Number of columns
            int m = matrix[0].length;

            // Initialize pointers for traversal
            int top = 0, left = 0;
            int bottom = n - 1, right = m - 1;

            // Traverse the matrix in spiral order
            while (top <= bottom && left <= right) {
                // Traverse from left to right
                for (int i = left; i <= right; ++i) {
                    ans.add(matrix[top][i]);
                }
                top++;

                // Traverse from top to bottom
                for (int i = top; i <= bottom; ++i) {
                    ans.add(matrix[i][right]);
                }
                right--;

                // Traverse from right to left
                if (top <= bottom) {
                    for (int i = right; i >= left; --i) {
                        ans.add(matrix[bottom][i]);
                    }
                    bottom--;
                }

                // Traverse from bottom to top
                if (left <= right) {
                    for (int i = bottom; i >= top; --i) {
                        ans.add(matrix[i][left]);
                    }
                    left++;
                }
            }

            return ans;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's matrix, e.g. [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
        int[][] matrix = parseIntMatrix(new Scanner(System.in).nextLine());
        System.out.println(new Solution().spiralOrder(matrix));
    }

    // "[[1, 2, 3], [4, 5, 6]]" -> {{1, 2, 3}, {4, 5, 6}}
    static int[][] parseIntMatrix(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new int[0][0];
        String[] rows = inner.split("\\], \\[");
        int[][] out = new int[rows.length][];
        for (int i = 0; i < rows.length; i++) {
            String r = rows[i].replaceAll("^\\[|\\]$", "");
            String[] parts = r.split(",");
            int[] row = new int[parts.length];
            for (int j = 0; j < parts.length; j++) row[j] = Integer.parseInt(parts[j].trim());
            out[i] = row;
        }
        return out;
    }
}
```

## Complexity Analysis

**Time Complexity:** O(N×M), as every element is traversed exactly once and the matrix holds a total of N×M elements (M elements in each of N rows).

**Space Complexity:** O(1), as the extra space used to store the answer is not considered.

---
title: "Print the Matrix in Spiral Manner"
summary: "Traverse an M × N matrix and return its elements in clockwise spiral order."
essential: true
kind: problem
difficulty: medium
topics: [arrays]
---

# Print the Matrix in Spiral Manner

Given an M × N matrix, print the elements in a clockwise spiral manner.

Return an array with the elements in the order of their appearance when printed in a spiral manner.

### Example 1

> - **Input :** matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
> - **Output :** [1, 2, 3, 6, 9, 8, 7, 4, 5]
> - **Explanation :**
> The elements in the spiral order are 1, 2, 3 → 6, 9 → 8, 7 → 4, 5

### Example 2

> - **Input :** matrix = [[1, 2, 3, 4], [5, 6, 7, 8]]
> - **Output :** [1, 2, 3, 4, 8, 7, 6, 5]
> - **Explanation :**
> The elements in the spiral order are 1, 2, 3, 4 → 8, 7, 6, 5

## Constraints

> - `m == matrix.length`
> - `n == matrix[i].length`
> - `1 <= m, n <= 100`
> - `-100 <= matrix[i][j] <= 100`

```python run
from typing import List

class Solution:
    # Function to print matrix in spiral manner
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        # Your code goes here.
        return []


# Reads the test case's matrix, e.g. [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
inner = input().strip()[1:-1].strip()
rows = inner.split("], [") if inner else []
matrix = [[int(t) for t in r.strip("[]").split(",")] for r in rows]
print(Solution().spiralOrder(matrix))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to print matrix in spiral manner
        List<Integer> spiralOrder(int[][] matrix) {
            // Your code goes here.
            return new ArrayList<>();
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

## Frequently Occurring Doubts

### How does the algorithm avoid revisiting elements?

After traversing a boundary, adjust it inward: increment `top` after the top row, decrement `right` after the right column, decrement `bottom` after the bottom row, and increment `left` after the left column.

### How do I handle the center element in an odd-dimensional matrix?

In an odd-dimensional square matrix, the center element is visited during the last iteration. No special handling is needed, as the shrinking boundaries naturally include it in the traversal.

## Follow-ups

### How would you handle a sparse matrix?

For sparse matrices, use a coordinate-based approach that tracks only non-zero elements, performing the traversal using the coordinates of active elements instead of iterating through every cell.

### How would you modify the algorithm for counterclockwise spiral traversal?

To traverse counterclockwise, start with the left column (top to bottom), then the bottom row (left to right), then the right column (bottom to top), and finally the top row (right to left).

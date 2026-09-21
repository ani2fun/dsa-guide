---
title: "Rotate Matrix by 90 Degrees"
summary: "Rotate an N × N matrix clockwise by 90 degrees, in place."
essential: true
kind: problem
difficulty: medium
topics: [arrays]
---

# Rotate Matrix by 90 Degrees

Given an N × N 2D integer matrix, rotate the matrix by 90 degrees clockwise.

The rotation must be done in place, meaning the input 2D matrix must be modified directly. Do not allocate another 2D matrix and do the rotation.

### Example 1

> - **Input :** matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
> - **Output :** [[7, 4, 1], [8, 5, 2], [9, 6, 3]]
> - **Explanation :**
> Rotating the matrix clockwise by 90 degrees turns the first column `7, 4, 1` (read bottom to top) into the first row, the second column `8, 5, 2` into the second row, and the third column `9, 6, 3` into the third row.

### Example 2

> - **Input :** matrix = [[0, 1, 1, 2], [2, 0, 3, 1], [4, 5, 0, 5], [5, 6, 7, 0]]
> - **Output :** [[5, 4, 2, 0], [6, 5, 0, 1], [7, 0, 3, 1], [0, 5, 1, 2]]
> - **Explanation :**
> Each column, read from the bottom up, becomes a row: `5, 4, 2, 0` → row 1, `6, 5, 0, 1` → row 2, `7, 0, 3, 1` → row 3, `0, 5, 1, 2` → row 4.

## Constraints

> - `n == matrix.length == matrix[i].length`
> - `1 <= n <= 100`
> - `-10⁴ <= matrix[i][j] <= 10⁴`

```python run
from typing import List

class Solution:
    # Function to rotate the matrix by 90 degrees clockwise, in place
    def rotateMatrix(self, matrix: List[List[int]]) -> None:
        # Your code goes here.
        pass


# Reads the test case's matrix, e.g. [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
inner = input().strip()[1:-1].strip()
rows = inner.split("], [") if inner else []
matrix = [[int(t) for t in r.strip("[]").split(",")] for r in rows]
Solution().rotateMatrix(matrix)
print(matrix)
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to rotate the matrix by 90 degrees clockwise, in place
        void rotateMatrix(int[][] matrix) {
            // Your code goes here.
        }
    }

    public static void main(String[] args) {
        // Reads the test case's matrix, e.g. [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
        int[][] matrix = parseIntMatrix(new Scanner(System.in).nextLine());
        new Solution().rotateMatrix(matrix);
        System.out.println(Arrays.deepToString(matrix));
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

### Where does each element end up after the rotation?

The element at row `i`, column `j` moves to row `j`, column `n - 1 - i`. The first row becomes the last column, read top to bottom; the last row becomes the first column.

### Why does transposing and then reversing each row give a clockwise rotation?

Transposing swaps rows and columns, so `matrix[i][j]` lands at `matrix[j][i]` — the first row is now the first column. Reversing each row then flips that column so it reads top to bottom, which is exactly where a clockwise rotation puts it.

## Follow-ups

### How would you rotate the matrix counterclockwise instead?

Transpose, then reverse each column instead of each row. Equivalently, reverse each row first and then transpose.

### How would you rotate by 180 degrees?

Reverse the order of the rows, then reverse each row — or apply the 90-degree rotation twice.

### Can a non-square M × N matrix be rotated in place?

No. Rotating an M × N matrix produces an N × M matrix, so unless M == N the result has a different shape and needs a new array.

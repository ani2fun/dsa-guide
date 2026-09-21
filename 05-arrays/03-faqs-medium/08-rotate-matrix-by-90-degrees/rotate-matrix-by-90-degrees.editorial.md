## Brute

### Intuition

Work out where each element lands and copy it there. After a clockwise rotation the first row becomes the last column, the second row becomes the second-to-last column, and so on — so the element at row `i`, column `j` ends up at row `j`, column `n - 1 - i`. Build the rotated matrix in a fresh array from that rule and copy it back.

### Approach

1. Let `n` be the size of the matrix and create an `n × n` array `rotated` filled with zeros.
2. For every row `i` and column `j`, set `rotated[j][n - 1 - i] = matrix[i][j]`.
3. Copy `rotated` back into `matrix` row by row so the input is modified.

### Solution

```python solution time=O(N²) space=O(N²)
from typing import List

class Solution:
    # Function to rotate the matrix by 90 degrees clockwise
    def rotateMatrix(self, matrix: List[List[int]]) -> None:
        n = len(matrix)

        # Build the rotated matrix in a separate array
        rotated = [[0] * n for _ in range(n)]

        # The element at (i, j) moves to (j, n - 1 - i)
        for i in range(n):
            for j in range(n):
                rotated[j][n - 1 - i] = matrix[i][j]

        # Copy the result back so the input is modified
        for i in range(n):
            matrix[i] = rotated[i]


# Reads the test case's matrix, e.g. [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
inner = input().strip()[1:-1].strip()
rows = inner.split("], [") if inner else []
matrix = [[int(t) for t in r.strip("[]").split(",")] for r in rows]
Solution().rotateMatrix(matrix)
print(matrix)
```

```java solution time=O(N²) space=O(N²)
import java.util.*;

public class Main {
    static class Solution {
        // Function to rotate the matrix by 90 degrees clockwise
        void rotateMatrix(int[][] matrix) {
            int n = matrix.length;

            // Build the rotated matrix in a separate array
            int[][] rotated = new int[n][n];

            // The element at (i, j) moves to (j, n - 1 - i)
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    rotated[j][n - 1 - i] = matrix[i][j];
                }
            }

            // Copy the result back so the input is modified
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    matrix[i][j] = rotated[i][j];
                }
            }
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

### Complexity Analysis

**Time Complexity:** O(N²) — every one of the N² elements is visited once to build the rotated matrix and once to copy it back.

**Space Complexity:** O(N²) — the rotated matrix is a second N × N array.

## Optimal

### Intuition

A clockwise rotation is two simpler reflections in a row. Transposing the matrix (swapping `matrix[i][j]` with `matrix[j][i]`) turns every row into a column, so the first row now stands as the first column — but read top to bottom it is in the wrong order. Reversing each row of the transposed matrix flips that order, and the result is exactly the rotated matrix. Both steps swap elements in place, so no extra matrix is needed.

### Approach

1. Transpose the matrix: for every `i` and every `j > i`, swap `matrix[i][j]` with `matrix[j][i]`. Only the upper triangle is visited so no pair is swapped twice.
2. Reverse each row of the matrix.

### Solution

```python solution time=O(N²) space=O(1)
from typing import List

class Solution:
    # Function to rotate the matrix by 90 degrees clockwise, in place
    def rotateMatrix(self, matrix: List[List[int]]) -> None:
        n = len(matrix)

        # Step 1: transpose — swap matrix[i][j] with matrix[j][i] above the diagonal
        for i in range(n):
            for j in range(i + 1, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        # Step 2: reverse every row
        for row in matrix:
            row.reverse()


# Reads the test case's matrix, e.g. [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
inner = input().strip()[1:-1].strip()
rows = inner.split("], [") if inner else []
matrix = [[int(t) for t in r.strip("[]").split(",")] for r in rows]
Solution().rotateMatrix(matrix)
print(matrix)
```

```java solution time=O(N²) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to rotate the matrix by 90 degrees clockwise, in place
        void rotateMatrix(int[][] matrix) {
            int n = matrix.length;

            // Step 1: transpose — swap matrix[i][j] with matrix[j][i] above the diagonal
            for (int i = 0; i < n; i++) {
                for (int j = i + 1; j < n; j++) {
                    int temp = matrix[i][j];
                    matrix[i][j] = matrix[j][i];
                    matrix[j][i] = temp;
                }
            }

            // Step 2: reverse every row
            for (int i = 0; i < n; i++) {
                int left = 0, right = n - 1;
                while (left < right) {
                    int temp = matrix[i][left];
                    matrix[i][left] = matrix[i][right];
                    matrix[i][right] = temp;
                    left++;
                    right--;
                }
            }
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

### Complexity Analysis

**Time Complexity:** O(N²) — the transpose touches each element above the diagonal once (about N²/2 swaps) and reversing the rows touches every element once more.

**Space Complexity:** O(1) — every swap happens inside the input matrix; no second matrix is allocated.

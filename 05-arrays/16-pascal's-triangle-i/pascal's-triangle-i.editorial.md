## Intuition

A brute-force way to solve this is to generate the entire Pascal's Triangle up to the given row and then read off the element at the given position — but that does far more work than needed for a single value.

We can instead calculate the value directly with the combination formula (nCr), avoiding the generation of the entire triangle: the element at row r, column c equals `(r−1)C(c−1)`. Since `nCr = n! / (r! × (n−r)!)` and `nCr = nC(n−r)`, we only need to iterate `min(r, n−r)` times, computing the product and division together at each step to avoid overflow.

## Approach

1. Identify the given row and column position in Pascal's Triangle.
2. Compute the binomial coefficient nCr using `nCr = n! / (r! × (n−r)!)`.
3. Choose the smaller value between r and (n−r) to minimize the number of iterations.
4. Initialize the result as 1, then iterate through the range, updating the result with multiplication and division together to prevent overflow.
5. Return the computed nCr, the value at the specified position in Pascal's Triangle.

## Solution

```python solution time=O(C) space=O(1)
class Solution:
    # Function to find the value at row r and column c in Pascal's Triangle
    def pascalTriangleI(self, r: int, c: int) -> int:
        return self.nCr(r - 1, c - 1)

    # Function to calculate nCr
    def nCr(self, n: int, r: int) -> int:
        # Choose the smaller value for fewer iterations
        if r > n - r:
            r = n - r

        # Base case
        if r == 1:
            return n

        res = 1  # To store the result

        # Calculate nCr using an iterative method that avoids overflow
        for i in range(r):
            res = res * (n - i)
            res = res // (i + 1)

        return res  # Return the result


# Reads the test case's r, then c
r = int(input())
c = int(input())
print(Solution().pascalTriangleI(r, c))
```

```java solution time=O(C) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the value at row r and column c in Pascal's Triangle
        int pascalTriangleI(int r, int c) {
            return nCr(r - 1, c - 1);
        }

        // Function to calculate nCr
        private int nCr(int n, int r) {
            // Choose the smaller value for fewer iterations
            if (r > n - r) r = n - r;

            // Base case
            if (r == 1) return n;

            int res = 1; // To store the result

            // Calculate nCr using an iterative method that avoids overflow
            for (int i = 0; i < r; i++) {
                res = res * (n - i);
                res = res / (i + 1);
            }

            return res; // Return the result
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

## Complexity Analysis

**Time Complexity:** O(C), where C is the column number — the loop in `nCr` runs C times, and C can be as large as R/2.

**Space Complexity:** O(1), as no extra space is used.

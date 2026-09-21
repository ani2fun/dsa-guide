---
title: "Pascal's Triangle III"
summary: "Return the first n rows (1-indexed) of Pascal's Triangle."
essential: true
kind: problem
difficulty: medium
topics: [arrays]
---

# Pascal's Triangle III

Given an integer n, return the first n rows (1-indexed) of Pascal's Triangle.

In Pascal's Triangle:

- The first row has one element, with a value of 1.
- Each row has one more element than the previous row.
- The value of each element is the sum of the elements directly above it.

### Example 1

> - **Input :** n = 4
> - **Output :** [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1]]
> - **Explanation :**
> The first 4 rows of Pascal's Triangle are `1`, `1 1`, `1 2 1`, `1 3 3 1` — each row starts and ends with 1, and every interior value is the sum of the two values above it.

### Example 2

> - **Input :** n = 5
> - **Output :** [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1]]
> - **Explanation :**
> The first 5 rows of Pascal's Triangle are `1`, `1 1`, `1 2 1`, `1 3 3 1`, `1 4 6 4 1` — each row starts and ends with 1, and every interior value is the sum of the two values above it.

## Constraints

> - `1 <= n <= 30`
> - `All values will fit inside a 32-bit integer.`

```python run
from typing import List

class Solution:
    # Function to generate the first n rows of Pascal's Triangle
    def pascalTriangleIII(self, n: int) -> List[List[int]]:
        # Your code goes here.
        return []


# Reads the test case's n
n = int(input())
print(Solution().pascalTriangleIII(n))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to generate the first n rows of Pascal's Triangle
        List<List<Integer>> pascalTriangleIII(int n) {
            // Your code goes here.
            return new ArrayList<>();
        }
    }

    public static void main(String[] args) {
        // Reads the test case's n
        int n = Integer.parseInt(new Scanner(System.in).nextLine());
        System.out.println(new Solution().pascalTriangleIII(n));
    }
}
```

## Frequently Occurring Doubts

### How do we calculate elements in the middle of a row?

Each middle element is the sum of the two elements directly above it: if the previous row is `prevRow`, then `currRow[i] = prevRow[i - 1] + prevRow[i]`.

### How can Pascal's Triangle be used to compute Fibonacci numbers?

The sum of the elements along the diagonals of Pascal's Triangle gives the Fibonacci numbers.

## Follow-ups

### How would you compute a specific element without generating the entire triangle?

To compute the value at row r and column c (0-indexed), use the combination formula: `C(r, c) = r! / (c! × (r−c)!)`.

### How can Pascal's Triangle be used in binomial expansion?

The nth row of Pascal's Triangle gives the coefficients of the terms in the expansion of (a+b)ⁿ.

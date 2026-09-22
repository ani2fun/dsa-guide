---
title: "Fibonacci Number - I"
summary: "Compute the nth Fibonacci number with a loop that carries only the last two values."
essential: true
kind: problem
difficulty: easy
topics: [basics, loops]
---

# Fibonacci Number - I

The Fibonacci sequence starts `0, 1` and every later term is the sum of the two before it: `0, 1, 1, 2, 3, 5, 8, 13, …`. Using 0-based positions, `F(0) = 0`, `F(1) = 1` and `F(n) = F(n - 1) + F(n - 2)` for `n >= 2`.

Complete the function `fibonacci` which takes a non-negative integer `n` and returns `F(n)`.

## Example 1

> **Input :** n = 5  
> **Output :** 5  
> **Explanation :** The sequence is 0, 1, 1, 2, 3, 5 — position 5 holds 5.

## Example 2

> **Input :** n = 0  
> **Output :** 0  
> **Explanation :** F(0) is defined as 0.

## Example 3

> **Input :** n = 10  
> **Output :** 55  
> **Explanation :** 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55 — position 10 holds 55.

## Constraints

`0 <= n <= 40`

```python run
class Solution:
    # Function to return the nth Fibonacci number, with F(0) = 0 and F(1) = 1
    def fibonacci(self, n: int) -> int:
        return 0


# Reads the test case's n, e.g. 5
n = int(input())
print(Solution().fibonacci(n))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the nth Fibonacci number, with F(0) = 0 and F(1) = 1
        int fibonacci(int n) {
            return 0;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's n, e.g. 5
        int n = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().fibonacci(n));
    }
}
```

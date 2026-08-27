---
title: "Fibonacci Number"
summary: "Compute the nth Fibonacci number using recursion."
essential: true
kind: problem
difficulty: easy
topics: [recursion, maths]
---

# Fibonacci Number

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,

> ```text
> F(0) = 0, F(1) = 1
> F(n) = F(n - 1) + F(n - 2), for n > 1.
> ```

Given n, calculate F(n).

### Example 1

> - **Input :** n = 2
> - **Output :** 1
> - **Explanation :**
> F(2) = F(1) + F(0) => 1 + 0 => 1.

### Example 2

> - **Input :** n = 3
> - **Output :** 2
> - **Explanation :**
> F(3) = F(2) + F(1) => 1 + 1 => 2.

## Constraints

> - `0 <= n <= 30`

```python run
class Solution:
    # Function to compute the nth Fibonacci number, using recursion
    def fib(self, n: int) -> int:
        # Your code goes here.
        pass


# Reads the test case's n
n = int(input())
print(Solution().fib(n))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to compute the nth Fibonacci number, using recursion
        int fib(int n) {
            // Your code goes here.
            return 0;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's n
        int n = new Scanner(System.in).nextInt();
        System.out.println(new Solution().fib(n));
    }
}
```

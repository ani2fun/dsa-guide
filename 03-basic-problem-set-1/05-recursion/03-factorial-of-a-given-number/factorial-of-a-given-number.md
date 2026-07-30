---
title: "Factorial Of A Given Number"
summary: "Compute n! recursively, returning a 64-bit result."
essential: true
kind: problem
difficulty: easy
topics: [recursion]
---

# Factorial Of A Given Number

Given an integer n, return the factorial of n.

Factorial of a non-negative integer, is the multiplication of all integers smaller than or equal to n (use 64-bits to return answer).

## Example 1

> **Input :** n = 3  
> **Output :** 6  
> **Explanation :**  
> Factorial = 1 * 2 * 3 => 6

## Example 2

> **Input :** n = 5  
> **Output :** 120  
> **Explanation :**  
> Factorial = 1 * 2 * 3 * 4 * 5 => 120

## Example 3

> **Input :** n = 4  
> **Output :** 24

## Constraints

- `0 <= n <= 15`

```python run
class Solution:
    # Function to find the factorial of n
    def factorial(self, n: int) -> int:
        # Your code goes here.
        pass


# Reads the test case's n
n = int(input())
print(Solution().factorial(n))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the factorial of n
        long factorial(int n) {
            // Your code goes here.
            return 0;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's n
        int n = new Scanner(System.in).nextInt();
        System.out.println(new Solution().factorial(n));
    }
}
```

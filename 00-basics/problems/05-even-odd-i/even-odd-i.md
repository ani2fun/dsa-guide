---
title: "Even Odd - I"
summary: "Print Even or Odd for an integer using the remainder operator."
essential: true
kind: problem
difficulty: easy
topics: [basics, conditionals]
---

# Even Odd - I

Complete the function `evenOrOdd` which takes an integer `n` and prints `Even` if `n` is even and `Odd` if it is odd.

Zero is even, and the rule applies to negative numbers too. Ensure only the first letter of the answer is capitalised.

## Example 1

> **Input :** n = 4  
> **Output :** Even  
> **Explanation :** 4 divided by 2 leaves no remainder.

## Example 2

> **Input :** n = 7  
> **Output :** Odd  
> **Explanation :** 7 divided by 2 leaves a remainder of 1.

## Example 3

> **Input :** n = -3  
> **Output :** Odd  
> **Explanation :** -3 is odd: its remainder on division by 2 is not zero.

## Constraints

`-10⁴ <= n <= 10⁴`

```python run
class Solution:
    # Function to print whether a number is even or odd
    def evenOrOdd(self, n: int) -> None:
        # Your code goes here — print "Even" or "Odd".
        pass


# Reads the test case's n, e.g. 4
n = int(input())
Solution().evenOrOdd(n)
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to print whether a number is even or odd
        void evenOrOdd(int n) {
            // Your code goes here — print "Even" or "Odd".
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's n, e.g. 4
        int n = Integer.parseInt(sc.nextLine().trim());
        new Solution().evenOrOdd(n);
    }
}
```

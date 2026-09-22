---
title: "Sum of Digits of a Number - I"
summary: "Add up the digits of a non-negative integer by peeling one digit per loop iteration."
essential: true
kind: problem
difficulty: easy
topics: [basics, loops]
---

# Sum of Digits of a Number - I

Complete the function `sumOfDigits` which takes a non-negative integer `n` and returns the sum of its digits.

## Example 1

> **Input :** n = 123  
> **Output :** 6  
> **Explanation :** 1 + 2 + 3 = 6

## Example 2

> **Input :** n = 9  
> **Output :** 9  
> **Explanation :** A single digit is its own sum.

## Example 3

> **Input :** n = 1000  
> **Output :** 1  
> **Explanation :** 1 + 0 + 0 + 0 = 1

## Constraints

`0 <= n <= 10⁹`

```python run
class Solution:
    # Function to return the sum of the digits of n
    def sumOfDigits(self, n: int) -> int:
        return 0


# Reads the test case's n, e.g. 123
n = int(input())
print(Solution().sumOfDigits(n))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the sum of the digits of n
        int sumOfDigits(int n) {
            return 0;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's n, e.g. 123
        int n = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().sumOfDigits(n));
    }
}
```

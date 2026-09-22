---
title: "Multiple Inputs"
summary: "Read three integers, one per line, and print their sum — the first program with more than one input."
essential: true
kind: problem
difficulty: easy
topics: [basics, io]
---

# Multiple Inputs

Complete the function `sumOfThree` which takes three integers `a`, `b` and `c` and returns their sum.

The three values arrive one per line, in that order. The exercise is in the reading: three separate reads, each converted to an integer, before any arithmetic happens.

## Example 1

> **Input :** a = 1, b = 2, c = 3  
> **Output :** 6  
> **Explanation :** 1 + 2 + 3 = 6

## Example 2

> **Input :** a = 10, b = -4, c = 7  
> **Output :** 13  
> **Explanation :** 10 + (-4) + 7 = 13

## Example 3

> **Input :** a = 0, b = 0, c = 0  
> **Output :** 0

## Constraints

`-1000 <= a, b, c <= 1000`

```python run
class Solution:
    # Function to add three integers read from the user
    def sumOfThree(self, a: int, b: int, c: int) -> int:
        return 0


# Reads the test case's a, e.g. 1
a = int(input())
# Reads the test case's b, e.g. 2
b = int(input())
# Reads the test case's c, e.g. 3
c = int(input())
print(Solution().sumOfThree(a, b, c))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to add three integers read from the user
        int sumOfThree(int a, int b, int c) {
            return 0;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's a, e.g. 1
        int a = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's b, e.g. 2
        int b = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's c, e.g. 3
        int c = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().sumOfThree(a, b, c));
    }
}
```

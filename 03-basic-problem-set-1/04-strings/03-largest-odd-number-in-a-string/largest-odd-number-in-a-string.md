---
title: "Largest Odd Number In A String"
summary: "Return the largest odd-valued substring of a numeric string, without leading zeroes."
essential: true
kind: problem
difficulty: easy
topics: [strings, greedy]
---

# Largest Odd Number In A String

Given a string s, representing a large integer, the task is to return the largest-valued odd integer (as a string) that is a substring of the given string s.

The number returned should not have leading zero's. But the given input string may have leading zero. (If no odd number is found, then return empty string.)

## Example 1

> **Input :** s = "5347"  
> **Output :** 5347  
> **Explanation :**  
> The odd numbers formed by given strings are --> 5, 3, 53, 347, 5347. So the largest among all the possible odd numbers for given string is 5347.

## Example 2

> **Input :** s = "0214638"  
> **Output :** 21463  
> **Explanation :**  
> The different odd numbers that can be formed by the given string are --> 1, 3, 21, 63, 463, 1463, 21463. We cannot include 021463 as the number contains leading zero. So largest odd number in given string is 21463.

## Example 3

> **Input :** s = "0032579"  
> **Output :** 32579

## Constraints

- `1 <= s.length <= 10³`
- `'0' <= s[i] <= '9'`

```python run
class Solution:
    # Function to find the largest odd number
    # that is a substring of given string
    def largeOddNum(self, s: str) -> str:
        # Your code goes here.
        pass


# Reads the test case's s
s = input()
print(Solution().largeOddNum(s))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        /* Function to find the largest odd number
        that is a substring of given string */
        String largeOddNum(String s) {
            // Your code goes here.
            return "";
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s
        String s = new Scanner(System.in).nextLine();
        System.out.println(new Solution().largeOddNum(s));
    }
}
```

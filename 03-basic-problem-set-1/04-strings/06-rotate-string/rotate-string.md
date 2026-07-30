---
title: "Rotate String"
summary: "Decide whether one string becomes another after some number of left shifts."
essential: true
kind: problem
difficulty: easy
topics: [strings]
---

# Rotate String

Given two strings s and goal, return true if and only if s can become goal after some number of shifts on s.

A shift on s consists of moving the leftmost character of s to the rightmost position.

For example, if s = "abcde", then it will be "bcdea" after one shift.

## Example 1

> **Input :** s = "abcde", goal = "cdeab"  
> **Output :** true  
> **Explanation :**  
> After performing 2 shifts we can achieve the goal string from string s. After the first shift the string s is => bcdea. After the second shift the string s is => cdeab.

## Example 2

> **Input :** s = "abcde", goal = "adeac"  
> **Output :** false  
> **Explanation :**  
> Any number of shift operations cannot convert string s to string goal.

## Example 3

> **Input :** s = "abcde", goal = "abcde"  
> **Output :** true

## Constraints

- `1 <= s.length <= 100`
- `1 <= goal.length <= 100`
- `s and goal consist of only lowercase English letters.`

```python run
class Solution:
    # Function to check if s becomes goal after some number of shifts
    def rotateString(self, s: str, goal: str) -> bool:
        # Your code goes here.
        pass


# Reads the test case's s and goal, one per line
s = input()
goal = input()
print("true" if Solution().rotateString(s, goal) else "false")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to check if s becomes goal after some number of shifts
        boolean rotateString(String s, String goal) {
            // Your code goes here.
            return false;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s and goal, one per line
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        String goal = sc.nextLine();
        System.out.println(new Solution().rotateString(s, goal));
    }
}
```

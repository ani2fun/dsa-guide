---
title: "Isomorphic String"
summary: "Decide whether two strings share a consistent one-to-one character mapping."
essential: true
kind: problem
difficulty: easy
topics: [strings, hashing]
---

# Isomorphic String

Given two strings s and t, determine if they are isomorphic. Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

## Example 1

> **Input :** s = "egg", t = "add"  
> **Output :** true  
> **Explanation :**  
> The 'e' in string s can be replaced with 'a' of string t, and the 'g' in s can be replaced with 'd' of t. Hence all characters in s can be replaced to get t.

## Example 2

> **Input :** s = "apple", t = "bbnbm"  
> **Output :** false  
> **Explanation :**  
> Strings are matched index by index. At index 0, 'a' maps to 'b'; at index 1, 'p' also maps to 'b'. This is invalid because **two different characters (a and p) cannot map to the same character (b)** in a one-to-one mapping. Therefore, no valid mapping exists and the output is false.

## Example 3

> **Input :** s = "paper", t = "title"  
> **Output :** true

## Constraints

- `1 <= s.length <= 10³`
- `s.length == t.length`
- `s and t consist of only lowercase English letters.`

```python run
class Solution:
    # Function to check if s and t are isomorphic
    def isomorphicString(self, s: str, t: str) -> bool:
        # Your code goes here.
        pass


# Reads the test case's s and t, one per line
s = input()
t = input()
print("true" if Solution().isomorphicString(s, t) else "false")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to check if s and t are isomorphic
        boolean isomorphicString(String s, String t) {
            // Your code goes here.
            return false;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s and t, one per line
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        String t = sc.nextLine();
        System.out.println(new Solution().isomorphicString(s, t));
    }
}
```

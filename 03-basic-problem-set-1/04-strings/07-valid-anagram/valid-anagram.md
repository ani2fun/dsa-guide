---
title: "Valid Anagram"
summary: "Decide whether one string is a rearrangement of another."
essential: true
kind: problem
difficulty: easy
topics: [strings, hashing]
---

# Valid Anagram

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Example 1

> **Input :** s = "anagram", t = "nagaram"  
> **Output :** true  
> **Explanation :**  
> We can rearrange the characters of string s to get string t as frequency of all characters from both strings is same.

## Example 2

> **Input :** s = "dog", t = "cat"  
> **Output :** false  
> **Explanation :**  
> We cannot rearrange the characters of string s to get string t as frequency of all characters from both strings is not same.

## Example 3

> **Input :** s = "eat", t = "tea"  
> **Output :** true

## Constraints

- `1 <= s.length, t.length <= 5*10⁴`
- `s and t consist of only lowercase English letters`

```python run
class Solution:
    # Function to check if t is an anagram of s
    def anagramStrings(self, s: str, t: str) -> bool:
        # Your code goes here.
        pass


# Reads the test case's s and t, one per line
s = input()
t = input()
print("true" if Solution().anagramStrings(s, t) else "false")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to check if t is an anagram of s
        boolean anagramStrings(String s, String t) {
            // Your code goes here.
            return false;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s and t, one per line
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        String t = sc.nextLine();
        System.out.println(new Solution().anagramStrings(s, t));
    }
}
```

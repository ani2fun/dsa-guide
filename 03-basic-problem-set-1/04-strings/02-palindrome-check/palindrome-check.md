---
title: "Palindrome Check"
summary: "Return true if a string reads the same forward and backward."
essential: true
kind: problem
difficulty: easy
topics: [strings, two-pointers]
---

# Palindrome Check

You are given a string s. Return true if the string is palindrome, otherwise false.

A string is called palindrome if it reads the same forward and backward.

## Example 1

> **Input :** s = "hannah"  
> **Output :** true  
> **Explanation :**  
> The given string when read backward is -> "hannah", which is same as when read forward. Hence answer is true.

## Example 2

> **Input :** s = "aabbaaa"  
> **Output :** false  
> **Explanation :**  
> The given string when read backward is -> "aaabbaa", which is not same as when read forward. Hence answer is false.

## Constraints

- `1 <= s.length <= 10⁵`
- `s consist of only uppercase and lowercase English characters.`

```python run
class Solution:
    # Function to check if a given string is a palindrome
    def palindromeCheck(self, s: str) -> bool:
        # Your code goes here.
        pass


# Reads the test case's s
s = input()
print("true" if Solution().palindromeCheck(s) else "false")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to check if a given string is a palindrome
        boolean palindromeCheck(String s) {
            // Your code goes here.
            return false;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s
        String s = new Scanner(System.in).nextLine();
        System.out.println(new Solution().palindromeCheck(s));
    }
}
```

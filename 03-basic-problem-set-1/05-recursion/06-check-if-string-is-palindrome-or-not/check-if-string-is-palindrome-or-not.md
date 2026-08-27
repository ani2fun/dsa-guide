---
title: "Check If String Is Palindrome Or Not"
summary: "Decide whether a string reads the same forward and backward, using recursion."
essential: true
kind: problem
difficulty: easy
topics: [recursion, strings]
---

# Check If String Is Palindrome Or Not

Given a string s, return true if the string is palindrome, otherwise false.

A string is called palindrome if it reads the same forward and backward.

### Example 1

> - **Input :** s = "hannah"
> - **Output :** true
> - **Explanation :**
> The string when reversed is --> "hannah", which is same as original string , so we return true.

### Example 2

> - **Input :** s = "aabbaA"
> - **Output :** false
> - **Explanation :**
> The string when reversed is --> "Aabbaa", which is not same as original string, So we return false.

### Example 3

> - **Input :** s = "aabbcccdbbaa"
> - **Output :** false

## Constraints

> - `1 <= s.length <= 10³`
> - `s consist of only uppercase and lowercase English characters.`

```python run
class Solution:
    # Function to check if the given string is a palindrome, using recursion
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
        // Function to check if the given string is a palindrome, using recursion
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

---
title: "Reverse A String I"
summary: "Reverse a string given as an array of characters, using recursion."
essential: true
kind: problem
difficulty: easy
topics: [recursion, strings]
---

# Reverse A String I

Given an input string as an array of characters, write a function that reverses the string.

### Example 1

> - **Input :** s = [h, e, l, l, o]
> - **Output :** [o, l, l, e, h]
> - **Explanation :**
> The given string is s = "hello" and after reversing it becomes s = "olleh".

### Example 2

> - **Input :** s = [b, y, e]
> - **Output :** [e, y, b]
> - **Explanation :**
> The given string is s = "bye" and after reversing it becomes s = "eyb".

### Example 3

> - **Input :** s = [h, a, n, n, a, h]
> - **Output :** [h, a, n, n, a, h]

## Constraints

> - `1 <= s.length <= 10³`
> - `s consist of only lowercase and uppercase English characters.`

```python run
from typing import List

class Solution:
    # Function to reverse the given string in place, using recursion
    def reverseString(self, s: List[str]) -> List[str]:
        # Your code goes here.
        return s


# Reads the test case's s, e.g. [h, e, l, l, o]
inner = input().strip()[1:-1].strip()
s = [t.strip() for t in inner.split(",")] if inner else []
result = Solution().reverseString(s)
print("[" + ", ".join(result) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to reverse the given string in place, using recursion
        ArrayList<Character> reverseString(ArrayList<Character> s) {
            // Your code goes here.
            return s;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s, e.g. [h, e, l, l, o]
        ArrayList<Character> s = parseCharArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().reverseString(s));
    }

    // "[h, e, l]" -> ['h', 'e', 'l']
    static ArrayList<Character> parseCharArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        ArrayList<Character> out = new ArrayList<>();
        if (inner.isEmpty()) return out;
        for (String part : inner.split(",")) out.add(part.trim().charAt(0));
        return out;
    }
}
```

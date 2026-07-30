---
title: "Reverse A String II"
summary: "Reverse a character array in place with O(1) extra memory."
essential: true
kind: problem
difficulty: easy
topics: [strings, two-pointers]
---

# Reverse A String II

Given a string, the task is to reverse it. The string is represented by an array of characters s.
Perform the reversal **in place with O(1) extra memory**.

Note: no need to return anything, modify the given list.

## Example 1

> **Input :** s = [h, e, l, l, o]  
> **Output :** [o, l, l, e, h]  
> **Explanation :**  
> The given string is s = "hello" and after reversing it becomes s = "olleh".

## Example 2

> **Input :** s = [b, y, e]  
> **Output :** [e, y, b]  
> **Explanation :**  
> The given string is s = "bye" and after reversing it becomes s = "eyb".

## Example 3

> **Input :** s = [h, a, n, n, a, h]  
> **Output :** [h, a, n, n, a, h]

## Constraints

- `1 <= s.length <= 10⁵`
- `s consist of only lowercase and uppercase English characters.`

```python run
from typing import List

class Solution:
    # Function to reverse the character list in place
    def reverseString(self, s: List[str]) -> None:
        # Your code goes here.
        pass


# Reads the test case's s, e.g. [h, e, l, l, o]
inner = input().strip()[1:-1].strip()
s = [t.strip().strip('"').strip("'") for t in inner.split(",")] if inner else []
Solution().reverseString(s)
print("[" + ", ".join(s) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to reverse the character list in place
        void reverseString(List<Character> s) {
            // Your code goes here.
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s, e.g. [h, e, l, l, o]
        List<Character> s = parseCharList(new Scanner(System.in).nextLine());
        new Solution().reverseString(s);
        System.out.println(s);
    }

    // "[h, e, l, l, o]" -> ['h', 'e', 'l', 'l', 'o']
    static List<Character> parseCharList(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        List<Character> out = new ArrayList<>();
        if (inner.isEmpty()) return out;
        for (String p : inner.split(",")) {
            String tok = p.trim().replaceAll("^[\"']|[\"']$", "");
            if (!tok.isEmpty()) out.add(tok.charAt(0));
        }
        return out;
    }
}
```

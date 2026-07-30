---
title: "Longest Common Prefix"
summary: "Find the longest common prefix shared by every string in an array."
essential: true
kind: problem
difficulty: easy
topics: [strings]
---

# Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.
If there is no common prefix, return an empty string "".

## Example 1

> **Input :** str = ["flowers", "flow", "fly", "flight"]  
> **Output :** fl  
> **Explanation :**  
> All strings given in array contains common prefix "fl".

## Example 2

> **Input :** str = ["dog", "cat", "animal", "monkey"]  
> **Output :**
> ```text
>
> ```
> **Explanation :**  
> There is no common prefix among the given strings in array.

## Example 3

> **Input :** str = ["lady", "lazy"]  
> **Output :** la

## Constraints

- `1 <= str.length <= 200`
- `1 <= str[i].length <= 200`
- `str[i] contains only lowercase English letters.`

```python run
from typing import List

class Solution:
    # Function to find the longest common prefix
    def longestCommonPrefix(self, strs: List[str]) -> str:
        # Your code goes here.
        pass


# Reads the test case's strs, e.g. ["flowers", "flow", "fly", "flight"]
inner = input().strip()[1:-1].strip()
strs = [t.strip().strip('"').strip("'") for t in inner.split(",")] if inner else []
print(Solution().longestCommonPrefix(strs))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the longest common prefix
        String longestCommonPrefix(String[] v) {
            // Your code goes here.
            return "";
        }
    }

    public static void main(String[] args) {
        // Reads the test case's strs, e.g. ["flowers", "flow", "fly", "flight"]
        String[] v = parseStringArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().longestCommonPrefix(v));
    }

    // "[\"flowers\", \"flow\"]" -> {"flowers", "flow"}
    static String[] parseStringArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new String[0];
        String[] parts = inner.split(",");
        String[] out = new String[parts.length];
        for (int i = 0; i < parts.length; i++)
            out[i] = parts[i].trim().replaceAll("^[\"']|[\"']$", "");
        return out;
    }
}
```

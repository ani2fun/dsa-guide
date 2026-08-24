---
title: "Sort Characters by Frequency"
summary: "Return a string's unique characters sorted by frequency, ties broken alphabetically."
essential: true
kind: problem
difficulty: easy
topics: [strings]
---

# Sort Characters by Frequency

You are given a string s. Return the array of **unique** characters, sorted by highest to lowest occurring frequency.

If two or more characters have the same frequency, sort them alphabetically.

## Example 1

> **Input :** s = "tree"  
> **Output :** [e, r, t]  
> **Explanation :**  
> The occurrences of each character are: e --> 2, r --> 1, t --> 1. r and t have the same frequency, so they're ordered alphabetically.

## Example 2

> **Input :** s = "raaaajj"  
> **Output :** [a, j, r]  
> **Explanation :**  
> The occurrences of each character are: a --> 4, j --> 2, r --> 1.

## Example 3

> **Input :** s = "bbccddaaa"  
> **Output :** [a, b, c, d]  
> **Explanation :**  
> a occurs 3 times; b, c and d occur 2 times each and tie, so they're ordered alphabetically.

## Constraints

- `1 <= s.length <= 10⁵`
- `s consists of only lowercase English characters.`

```python run
class Solution:
    # Function to return s's unique characters sorted by frequency, ties broken alphabetically
    def frequencySort(self, s: str) -> list[str]:
        # Your code goes here.
        pass


# Reads the test case's s
s = input()
result = Solution().frequencySort(s)
print("[" + ", ".join(result) + "]")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to return s's unique characters sorted by frequency, ties broken alphabetically
        List<Character> frequencySort(String s) {
            // Your code goes here.
            return new ArrayList<>();
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s
        String s = new Scanner(System.in).nextLine();
        List<Character> result = new Solution().frequencySort(s);
        StringBuilder sb = new StringBuilder("[");
        for (int i = 0; i < result.size(); i++) {
            if (i > 0) sb.append(", ");
            sb.append(result.get(i));
        }
        sb.append("]");
        System.out.println(sb);
    }
}
```

## Fun facts
> - This problem is often encountered when developing data analysis tools or text editors, where understanding the frequency of character usage can be important.
> - Optimizing compression algorithms such as Huffman coding relies on knowing the frequency of each character in the dataset.
> - This problem's concept is also used in SEO analytics, where the frequency of certain words or characters can affect a webpage's visibility in search engine results.

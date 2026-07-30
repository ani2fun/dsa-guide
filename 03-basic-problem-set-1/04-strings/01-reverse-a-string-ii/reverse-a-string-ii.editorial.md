## Brute

### Intuition

- To reverse a string, an auxiliary data structure like a temporary array can be used to store characters in reverse order.
- The thought process involves iterating over the original string and placing each character into the temporary array from the end to the beginning, which naturally builds the reversed sequence.
- Once the reversed order is formed in the temporary array, copying it back to the original string results in the desired reversal.
- This approach leverages extra space to simplify the reversal process.

### Approach

- Create a temporary array/list to store characters. Iterate over the given string from the first character to the last.
- During each iteration, copy the current character to the temporary array in reverse order (that is from the end of the original string to the beginning of the temporary array).
- After completing the iteration, iterate again over the temporary array and copy each character back to the original string to reverse its content.

### Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    # Function to reverse a string
    def reverseString(self, s: List[str]) -> None:
        n = len(s)

        # Create a temporary list to store reversed elements
        temp = [None] * n

        # Copy elements from original list to temp in reverse order
        for i in range(n):
            temp[i] = s[n - i - 1]

        # Copy back the reversed string to original list
        for i in range(n):
            s[i] = temp[i]

        return


# Reads the test case's s, e.g. [h, e, l, l, o]
inner = input().strip()[1:-1].strip()
s = [t.strip().strip('"').strip("'") for t in inner.split(",")] if inner else []
Solution().reverseString(s)
print("[" + ", ".join(s) + "]")
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to reverse the string
        public void reverseString(List<Character> s) {
            int n = s.size();

            // Create a temporary list to store reversed elements
            List<Character> temp = new ArrayList<>(n);

            // Initialize temp with dummy values
            for (int i = 0; i < n; i++) {
                temp.add(' ');
            }

            // Copy elements from original list to temp in reverse order
            for (int i = 0; i < n; i++) {
                temp.set(i, s.get(n - i - 1));
            }

            // Copy back the reversed string to original list
            for (int i = 0; i < n; i++) {
                s.set(i, temp.get(i));
            }
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

### Complexity Analysis

- **Time Complexity:** O(N), where N is the length of the string. The algorithm iterates once over the string to copy characters into the temporary array and then iterates again to copy them back to the original string.
- **Space Complexity:** O(N), due to the usage of the extra data structure (temporary array), which grows linearly with the size of the input string.

## Optimal

### Intuition

- To reverse a string, another method is swapping the characters from the beginning and end simultaneously.
- This can be achieved using two pointers: one positioned at the leftmost character and the other at the rightmost character.
  - Swap these two characters and then move both the pointers toward the center until they meet.
- In this manner, the first character is swapped with the last, the second with the second last, and so forth.

### Approach

- Set up two pointers: `i` and `j`. Initialize the pointer `i` to 0 (the start of the string) and `j` to (length of string - 1) (the end of the string).
- Use a while loop to iterate as long as `i` is less than `j` and in each iteration, swap the characters at positions `i` and `j`.
- After swapping, increment `i` by 1 and decrement `j` by 1. Continue this process until the pointers meet or cross each other.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    # Function to reverse a string
    def reverseString(self, s: List[str]) -> None:
        start, end = 0, len(s) - 1

        # Until the string is reversed
        while start < end:
            # Swap the characters at start and end
            s[start], s[end] = s[end], s[start]

            # Move the pointers towards the center
            start += 1
            end -= 1

        return


# Reads the test case's s, e.g. [h, e, l, l, o]
inner = input().strip()[1:-1].strip()
s = [t.strip().strip('"').strip("'") for t in inner.split(",")] if inner else []
Solution().reverseString(s)
print("[" + ", ".join(s) + "]")
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to reverse the string
        public void reverseString(List<Character> s) {
            int start = 0, end = s.size() - 1;

            // Until the string is reversed
            while (start < end) {
                // Swap the characters at start and end
                char ch = s.get(start);
                s.set(start, s.get(end));
                s.set(end, ch);

                // Move the pointers towards the center
                start++;
                end--;
            }
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

### Complexity Analysis

- **Time Complexity:** O(N), linear time where N is the length of the string. The algorithm iterates through half of the string.
- **Space Complexity:** O(1), constant space. The algorithm only uses a few extra variables regardless of the input size.

<div style="border-left:4px solid #195045;background:rgba(25,80,69,0.08);padding:0.6rem 1rem;border-radius:0 0.5rem 0.5rem 0;margin:1.25rem 0">

💡 **The same idea, recursively.** This can also be done with recursion: swap the characters at the two ends, then call the function again for the substring that excludes those ends, until the two pointers meet.

</div>

## Intuition

Reversing a string through recursion involves conceptualizing the problem in smaller segments. The process identifies a base case where the left index surpasses or equals the right index, signaling completion. Characters at the left and right indices are swapped, and a recursive call is initiated with updated indices (left incremented, right decremented). This sequence of swaps ensures the entire string is reversed.

## Approach

1. **Identify the Base Case:** Determine the condition under which the recursion should stop. For reversing a string, the recursion stops when the left index is greater than or equal to the right index. This indicates that we have reached the middle of the string and all necessary character swaps have been made.
2. **Swap Characters at Indices:** Perform the swap operation between the characters at the current left and right indices. This action exchanges the characters at the ends of the string segment being processed, which moves towards reversing the string.
3. **Make Recursive Calls:** After swapping, call the recursive function again with updated indices: increment the left index and decrement the right index. This step processes the next pair of characters moving inward until the base case is met.

## Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:

    # Function to reverse the given string
    def reverseString(self, s: List[str]) -> List[str]:

        # Recursive function to reverse the
        # string character by character
        def reverse(s, left, right):
            # Base case
            if left >= right:
                return

            # Swap characters at left and right positions
            s[left], s[right] = s[right], s[left]

            # Recursive call with updated indices
            reverse(s, left + 1, right - 1)

        reverse(s, 0, len(s) - 1)
        return s


# Reads the test case's s, e.g. [h, e, l, l, o]
inner = input().strip()[1:-1].strip()
s = [t.strip() for t in inner.split(",")] if inner else []
result = Solution().reverseString(s)
print("[" + ", ".join(result) + "]")
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        /* Recursive function to reverse the
        string character by character */
        private void reverse(ArrayList<Character> s, int left, int right) {

            // Base case
            if (left >= right) return;

            // Swap characters at left and right positions
            char temp = s.get(left);
            s.set(left, s.get(right));
            s.set(right, temp);

            // Recursive call with updated indices
            reverse(s, left + 1, right - 1);
        }

        // Function to reverse the given string
        public ArrayList<Character> reverseString(ArrayList<Character> s) {
            int left = 0;
            int right = s.size() - 1;
            reverse(s, left, right);
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

## Complexity Analysis

- **Time Complexity:** O(N) — each recursive call swaps one pair of characters and moves both indices inward, so the recursion performs N/2 swaps for a string of length N.
- **Space Complexity:** O(N) — the swaps happen in place, but the recursion stack grows to a depth of N/2 before the base case unwinds it.

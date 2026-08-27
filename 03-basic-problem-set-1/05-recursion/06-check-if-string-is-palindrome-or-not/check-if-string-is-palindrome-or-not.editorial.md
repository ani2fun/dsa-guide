## Intuition

Determining whether a string is a palindrome through recursion involves comparing characters from the start and end of the string. If the characters match, the next set of characters is checked recursively, moving inward. This process continues until a mismatch is found, indicating the string is not a palindrome, or until all characters are verified to match, confirming the string reads the same forwards and backwards.

## Approach

1. Start by comparing the first and last characters of the string. If the characters match, move inward by increasing the starting index and decreasing the ending index. Check if the substring between these indices is also a palindrome.
2. Continue this process until the starting index is greater than or equal to the ending index. If at any point the characters do not match, the string is not a palindrome.
3. If all the characters are successfully compared and they all match, the string is a palindrome.

## Solution

```python solution time=O(N) space=O(N)
class Solution:
    def palindromeCheck(self, s: str) -> bool:
        # Call the recursive helper method with initial indices
        return self.isPalindrome(s, 0, len(s) - 1)

    def isPalindrome(self, s: str, left: int, right: int) -> bool:
        # Base Case: If the start index is greater than or equal to the end index
        if left >= right:
            return True
        # Check if characters at the current positions are the same
        if s[left] != s[right]:
            return False  # Characters do not match, so it's not a palindrome
        # Recur for the next set of characters
        return self.isPalindrome(s, left + 1, right - 1)


# Reads the test case's s
s = input()
print("true" if Solution().palindromeCheck(s) else "false")
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Method to check if a string is a palindrome
        public boolean palindromeCheck(String s) {
            // Start recursion with the whole string
            return isPalindrome(s, 0, s.length() - 1);
        }

        // Helper method to perform the recursive check
        private boolean isPalindrome(String s, int left, int right) {
            // Base Case: If the start index is greater than or equal to the end index, it's a palindrome
            if (left >= right) {
                return true;
            }
            // Check if characters at the current positions are the same
            if (s.charAt(left) != s.charAt(right)) {
                return false; // Characters do not match, so it's not a palindrome
            }
            // Recur for the next set of characters
            return isPalindrome(s, left + 1, right - 1);
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s
        String s = new Scanner(System.in).nextLine();
        System.out.println(new Solution().palindromeCheck(s));
    }
}
```

## Complexity Analysis

- **Time Complexity:** O(N) — each recursive call compares one pair of characters and moves both indices inward, so at most N/2 comparisons are made for a string of length N.
- **Space Complexity:** O(N) — no extra data structure is used, but the recursion stack grows to a depth of N/2 before the base case is reached.

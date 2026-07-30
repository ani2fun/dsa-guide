## Intuition

- To determine if a string is a palindrome, that is, reads the same backwards as forwards, begin by comparing the first and last characters.
- If they match, proceed by moving inward from both ends and comparing the subsequent pairs of characters. This process is repeated, gradually converging towards the center of the string.
- If all character pairs match throughout this process, the string is confirmed to be a palindrome.
- This method effectively checks for symmetry by comparing characters from both ends toward the center.

## Approach

1. Initialize two pointers: one at the beginning (`left`) and one at the end (`right`) of the string.
2. Compare the characters at `left` and `right`. If they are not equal, return false.
3. Move both pointers inward (increment `left` and decrement `right`) and continue the comparison. If the loop completes without finding unequal characters, the string is a palindrome and returns true.

## Solution

```python solution time=O(N) space=O(1)
class Solution:
    # Function to check if a given string is a palindrome
    def palindromeCheck(self, s: str) -> bool:
        left = 0
        right = len(s) - 1

        # Iterate while  start pointer is less than end pointer
        while left < right:
            # If characters  don't match, it's not a palindrome
            if s[left] != s[right]:
                return False
            left += 1
            right -= 1
        return True


# Reads the test case's s
s = input()
print("true" if Solution().palindromeCheck(s) else "false")
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to check if a given string is a palindrome
        public boolean palindromeCheck(String s) {
            int left = 0;
            int right = s.length() - 1;

            // Iterate while start pointer is less than end pointer
            while (left < right) {
                // If characters  don't match, it's not a palindrome
                if (s.charAt(left) != s.charAt(right)) {
                    return false;
                }
                left++;
                right--;
            }
            return true;
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

- **Time Complexity:** O(N), where N is the length of the string.
- **Space Complexity:** O(1), as no extra space is required.

<div style="border-left:4px solid #195045;background:rgba(25,80,69,0.08);padding:0.6rem 1rem;border-radius:0 0.5rem 0.5rem 0;margin:1.25rem 0">

💡 **The same idea, recursively.** Compare the letters at the two ends. If they match, call the function again for the next pair (`start + 1`, `end - 1`) until `start >= end`. If any pair differs, return false; once the base case `start >= end` is reached, the string is a palindrome.

</div>

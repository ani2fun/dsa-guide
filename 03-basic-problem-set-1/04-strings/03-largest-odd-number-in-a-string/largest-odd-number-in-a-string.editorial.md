## Intuition

- To determine the largest substring ending with an odd digit, start by iterating backward from the end of the number.
- This approach efficiently finds the rightmost odd digit by examining each character in reverse order.
- Once an odd digit is encountered, the substring from the beginning of the number up to and including this digit represents the largest possible odd-ending substring.
- This process leverages the fact that finding the last occurrence of an odd digit directly provides the longest valid substring.

## Approach

1. Start by iterating through the string from the end towards the beginning to find the first odd digit. This digit marks the potential end of the largest odd number substring.
2. Once an odd digit is found, skip any leading zeroes from the beginning of the string up to this odd digit.
3. Extract and return the substring starting after the leading zeroes and ending at the identified odd digit. This substring represents the largest odd integer without leading zeroes.

## Solution

```python solution time=O(N) space=O(N)
class Solution:
    # Function to find the largest odd number
    # that is a substring of given string
    def largeOddNum(self, s: str) -> str:
        ind = -1

        # Iterate through the string from the end to beginning
        for i in range(len(s) - 1, -1, -1):
            # Break if an odd digit is found
            if (int(s[i]) % 2) == 1:
                ind = i
                break

        # Skipping any leading zeroes
        i = 0
        while i <= ind and s[i] == '0':
            i += 1

        # Return the largest odd number substring
        return s[i:ind + 1]


# Reads the test case's s
s = input()
print(Solution().largeOddNum(s))
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        /* Function to find the largest odd number
        that is a substring of given string */
        public String largeOddNum(String s) {
            int ind = -1;

            // Iterate through the string from the end to beginning
            int i;
            for (i = s.length() - 1; i >= 0; i--) {
                // Break if an odd digit is found
                if ((s.charAt(i) - '0') % 2 == 1) {
                    ind = i;
                    break;
                }
            }

            // If no odd number was found, return an empty string
            if (ind == -1) return "";

            // Skipping any leading zeroes
            i = 0;
            while (i <= ind && s.charAt(i) == '0') i++;

            // Return the largest odd number substring
            return s.substring(i, ind + 1);
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s
        String s = new Scanner(System.in).nextLine();
        System.out.println(new Solution().largeOddNum(s));
    }
}
```

## Complexity Analysis

- **Time Complexity:** O(N), the loop runs once through the string of length N.
- **Space Complexity:** O(N), the auxiliary space used is O(1), but if the space for the returned string is considered (which will be O(N) in the worst case), the overall space complexity comes out to be O(N).

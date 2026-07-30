## Brute

*Using sorting.*

### Intuition

- To determine the longest common prefix among a set of strings, consider the following approach: when a list of strings is sorted lexicographically, the first string and the last string in this sorted list will differ the most.
- The common prefix of these two strings is guaranteed to be the longest common prefix across all strings in the array.
- For example, if the sorted list is ["flight", "flow", "flowers", "fly"], comparing the first and last string in the sorted order gives the longest common prefix shared by all strings in the list.

### Approach

1. Sort the array of strings.
2. Select the first and the last string from the sorted array. These two strings will have the maximum possible common prefix.
3. Initialize an index variable to zero. This index will track the length of the common prefix.
4. Compare characters at the current index of both selected strings. Continue moving the index forward as long as the characters at the current index are equal and the index is within the bounds of both strings.
5. Once characters differ or the end of one of the strings is reached, the index will indicate the length of the common prefix.
6. Return the substring of the first string from the start to the index, which represents the longest common prefix.

### Solution

```python solution time=O(N*M*log N) space=O(M)
from typing import List

class Solution:
    # Function to find the longest common prefix
    def longestCommonPrefix(self, strs: List[str]) -> str:
        # Edge case: empty list
        if not strs:
            return ""

        # Sort the list to get the lexicographically smallest and largest strings
        strs.sort()
        # First string (smallest in sorted order)
        first = strs[0]
        # Last string (largest in sorted order)
        last = strs[-1]

        # Compare characters of the first and last strings
        ans = []
        for i in range(min(len(first), len(last))):
            # If characters don't match, return the current prefix
            if first[i] != last[i]:
                return ''.join(ans)
            # Append the matching character to the result
            ans.append(first[i])

        # Return the longest common prefix found
        return ''.join(ans)


# Reads the test case's strs, e.g. ["flowers", "flow", "fly", "flight"]
inner = input().strip()[1:-1].strip()
strs = [t.strip().strip('"').strip("'") for t in inner.split(",")] if inner else []
print(Solution().longestCommonPrefix(strs))
```

```java solution time=O(N*M*log N) space=O(M)
import java.util.*;

public class Main {
    static class Solution {
        // Method to find the longest common prefix in an array of strings
        public String longestCommonPrefix(String[] v) {
            // Use StringBuilder to build the result
            StringBuilder ans = new StringBuilder();

            // Sort the array to get the lexicographically smallest and largest strings
            Arrays.sort(v);
            // First string (smallest in sorted order)
            String first = v[0];
            // Last string (largest in sorted order)
            String last = v[v.length - 1];

            // Compare characters of the first and last strings
            for (int i = 0; i < Math.min(first.length(), last.length()); i++) {
                // If characters don't match, return the current prefix
                if (first.charAt(i) != last.charAt(i)) {
                    return ans.toString();
                }
                // Append the matching character to the result
                ans.append(first.charAt(i));
            }

            // Return the longest common prefix found
            return ans.toString();
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

### Complexity Analysis

- **Time Complexity:** O(N*M*log N), where N is the number of strings and M is the maximum length of a string. Sorting does O(N*log N) comparisons, and comparing two strings during the sort costs up to O(M), so the sort dominates. Comparing the characters of the first and last strings is a further O(M), which the sorting step absorbs.
- **Space Complexity:** O(M), as the answer can store the length of the prefix, which in the worst case is O(M).

## Optimal

*Using a vertical scan.*

### Intuition

- The vertical scan approach compares the strings column by column instead of comparing whole strings.
- Think of all strings arranged one below another:
  - flower
  - flow
  - flight
- Now compare: the first character of every string, then the second character of every string, then the third, and so on.
- The longest common prefix ends at the first position where any string has a different character or where one string ends.
- So we keep moving left to right across the characters, and for each position we verify that all strings have the same character there.
- If all strings match at index i, then that character belongs to the prefix. If a mismatch is found, we immediately return the prefix collected so far.

### Approach

1. If the array of strings is empty, return "".
2. Take the first string as a reference.
3. Traverse its characters from left to right.
4. For each character position i, compare `strs[0][i]` with `strs[j][i]` for every other string j. If any string ends before i or has a different character at i, stop and return the prefix up to i.
5. If no mismatch is found, the first string itself is the longest common prefix.

### Solution

```python solution time=O(N*M) space=O(1)
from typing import List

class Solution:
    # Function to find the longest common prefix
    def longestCommonPrefix(self, strs: List[str]) -> str:
        # Edge case: empty list
        if not strs:
            return ""

        # Traverse character by character using the first string as reference
        for i in range(len(strs[0])):

            # Current character from the first string
            ch = strs[0][i]

            # Compare this character with the same index in all other strings
            for j in range(1, len(strs)):

                # If the current string ends or characters do not match, return prefix
                if i == len(strs[j]) or strs[j][i] != ch:
                    return strs[0][:i]

        # If all characters match, the first string itself is the longest common prefix
        return strs[0]


# Reads the test case's strs, e.g. ["flowers", "flow", "fly", "flight"]
inner = input().strip()[1:-1].strip()
strs = [t.strip().strip('"').strip("'") for t in inner.split(",")] if inner else []
print(Solution().longestCommonPrefix(strs))
```

```java solution time=O(N*M) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Method to find the longest common prefix in an array of strings
        public String longestCommonPrefix(String[] v) {
            // Edge case: empty array
            if (v.length == 0) return "";

            // Traverse character by character using the first string as reference
            for (int i = 0; i < v[0].length(); i++) {

                // Current character from the first string
                char ch = v[0].charAt(i);

                // Compare this character with the same index in all other strings
                for (int j = 1; j < v.length; j++) {

                    // If the current string ends or characters do not match, return prefix
                    if (i == v[j].length() || v[j].charAt(i) != ch) {
                        return v[0].substring(0, i);
                    }
                }
            }

            // If all characters match, the first string itself is the longest common prefix
            return v[0];
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

### Complexity Analysis

- **Time Complexity:** O(N*M), where N is the number of strings and M is the maximum length of a string. In the worst case, for each character position up to M, we compare that character across all N strings.
- **Space Complexity:** O(1), we only use a few variables for traversal. If the returned answer string is counted, it can be O(M) in the worst case.

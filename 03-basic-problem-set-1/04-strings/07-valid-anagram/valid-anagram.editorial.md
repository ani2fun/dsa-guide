## Brute

### Intuition

The letters of an anagram should form identically sequences if alphabetically sorted. By furthering this thought process a method to check for anagrams would be sorting both strings. By sorting both strings and then comparing them, we can easily determine if they contain the same characters in the same frequencies.

### Approach

1. Sort the characters of both strings using an inbuilt sort function, so that if they are anagrams, the sorted strings will be identical.
2. Compare the sorted versions of both strings. If they match, the original strings are anagrams; otherwise, they are not.
3. Return true if the sorted strings are identical, otherwise return false.

### Solution

```python solution time=O(N log N) space=O(N)
class Solution:
    def anagramStrings(self, s: str, t: str) -> bool:
        # If lengths are not equal, they cannot be anagrams
        if len(s) != len(t):
            return False

        # Sort both strings and compare
        return sorted(s) == sorted(t)


# Reads the test case's s and t, one per line
s = input()
t = input()
print("true" if Solution().anagramStrings(s, t) else "false")
```

```java solution time=O(N log N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        public boolean anagramStrings(String s, String t) {
            // If lengths are not equal, they cannot be anagrams
            if (s.length() != t.length()) return false;

            // Convert strings to char arrays and sort them
            char[] sArray = s.toCharArray();
            char[] tArray = t.toCharArray();
            Arrays.sort(sArray);
            Arrays.sort(tArray);

            // Compare sorted arrays
            return Arrays.equals(sArray, tArray);
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s and t, one per line
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        String t = sc.nextLine();
        System.out.println(new Solution().anagramStrings(s, t));
    }
}
```

### Complexity Analysis

- **Time Complexity:** O(N log N) due to sorting each string.
- **Space Complexity:** O(N). The algorithm itself adds no data structure, but both implementations copy the input to sort it — Java creates two additional character arrays, and Python's `sorted()` builds a new list — so each is O(N) in practice.

## Optimal

### Intuition

An alternative approach to checking anagrams is to check the number of times each character in both strings appears through frequency counting. The frequency counting method for checking if two strings are anagrams is based on the idea that two strings are anagrams if they have the same characters appearing the same number of times. By counting the frequency of each character in the first string and then decreasing the count for each character in the second string, we can ensure that both strings have identical character distributions. If any character count does not return to zero, the strings are not anagrams.

### Approach

1. Initialize a frequency array of size 26 to count the occurrences of each letter in the first string. Each index of the array represents a letter from 'a' to 'z'.
2. Iterate through the second string and decrease the count in the frequency array for each letter found in it. This ensures we are balancing out the counts from the first string.
3. Check the frequency array. If all counts return to zero, both strings have identical character frequencies and are anagrams. If any count is not zero, the strings are not anagrams.

### Solution

```python solution time=O(N) space=O(1)
class Solution:
    def anagramStrings(self, s: str, t: str) -> bool:
        # Edge Cases
        if len(s) != len(t):
            return False

        # To store the count of each character
        count = [0] * 26

        # Count occurrence of each character in first string
        for c in s:
            count[ord(c) - ord('a')] += 1

        # Decrement the count for each character in the second string
        for c in t:
            count[ord(c) - ord('a')] -= 1

        # Check for count of every character
        for i in count:
            # If the count is not zero
            if i != 0:
                return False  # Return false

        # Otherwise strings are anagram
        return True


# Reads the test case's s and t, one per line
s = input()
t = input()
print("true" if Solution().anagramStrings(s, t) else "false")
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        public boolean anagramStrings(String s, String t) {
            // Edge Cases
            if (s.length() != t.length()) return false;

            // To store the count of each character
            int[] count = new int[26];

            // Count occurrence of each character in first string
            for (char c : s.toCharArray()) count[c - 'a']++;

            // Decrement the count for each character in the second string
            for (char c : t.toCharArray()) count[c - 'a']--;

            // Check for count of every character
            for (int i : count) {
                // If the count is not zero
                if (i != 0) return false; // Return false
            }

            // Otherwise strings are anagram
            return true;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's s and t, one per line
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        String t = sc.nextLine();
        System.out.println(new Solution().anagramStrings(s, t));
    }
}
```

### Complexity Analysis

- **Time Complexity:** O(N), where N is the length of the strings — one pass to count, one to decrement, and a fixed 26-step check.
- **Space Complexity:** O(1). The frequency array holds 26 entries whatever the input size.

<div style="border-left:4px solid #da5233;background:rgba(218,82,51,0.08);padding:0.6rem 1rem;border-radius:0 0.5rem 0.5rem 0;margin:1.25rem 0">

⚠️ **The counting approach assumes lowercase letters.** `count[c - 'a']` indexes a 26-entry array, so an uppercase or non-alphabetic character indexes outside it — Java throws, and Python silently wraps to the wrong slot. The constraints guarantee lowercase, which is what makes it safe; widen the alphabet and this needs a hash map instead. The sorting approach has no such limit.

</div>

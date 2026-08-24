## Intuition

The frequency of each character is all that decides the answer, and there are only 26 possible
lowercase letters. So a fixed 26-slot frequency table can hold the full count for any input, and
sorting that small, constant-size table by (frequency descending, letter ascending) directly
produces the answer.

## Approach

1. Create a frequency array of 26 pairs, one per lowercase letter, each pair holding that letter
   and a count starting at 0.
2. Walk the string once, incrementing the count for each character's pair.
3. Sort the 26 pairs by descending frequency, breaking ties by ascending letter.
4. Collect the letters whose count is greater than 0, in that sorted order.

## Solution

```python solution time=O(N) space=O(1)
class Solution:
    # Function to return s's unique characters sorted by frequency, ties broken alphabetically
    def frequencySort(self, s: str) -> list[str]:
        # Frequency table for 'a' to 'z'
        freq = [(0, chr(i + ord('a'))) for i in range(26)]

        # Count the frequency of each character
        for ch in s:
            index = ord(ch) - ord('a')
            freq[index] = (freq[index][0] + 1, ch)

        # Sort by frequency (descending), then alphabetically (ascending)
        freq.sort(key=lambda x: (-x[0], x[1]))

        # Keep only the letters that actually appear
        return [ch for count, ch in freq if count > 0]


# Reads the test case's s
s = input()
result = Solution().frequencySort(s)
print("[" + ", ".join(result) + "]")
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        static class Pair {
            int frequency;
            char character;

            Pair(int frequency, char character) {
                this.frequency = frequency;
                this.character = character;
            }
        }

        // Function to return s's unique characters sorted by frequency, ties broken alphabetically
        List<Character> frequencySort(String s) {
            // Frequency table for 'a' to 'z'
            Pair[] freqPair = new Pair[26];
            for (int i = 0; i < 26; i++) {
                freqPair[i] = new Pair(0, (char) (i + 'a'));
            }

            // Count the frequency of each character
            for (int i = 0; i < s.length(); i++) {
                freqPair[s.charAt(i) - 'a'].frequency++;
            }

            // Sort by frequency (descending), then alphabetically (ascending)
            Arrays.sort(freqPair, (p1, p2) -> {
                if (p1.frequency != p2.frequency) {
                    return p2.frequency - p1.frequency;
                }
                return p1.character - p2.character;
            });

            // Keep only the letters that actually appear
            List<Character> ans = new ArrayList<>();
            for (Pair pair : freqPair) {
                if (pair.frequency > 0) {
                    ans.add(pair.character);
                }
            }
            return ans;
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

## Complexity Analysis

- **Time Complexity:** O(N), where N is the length of s — one pass to count characters, plus
  sorting and scanning the fixed 26-entry table, which is constant work.
- **Space Complexity:** O(1). The frequency table holds 26 entries whatever the input size.

## Intuition

With two candidates there is only one question to ask: is `a` greater than `b`? If yes, `a` is the maximum; if no, `b` is at least as large, which covers the equal case for free.

## Approach

1. **Compare:** test `a > b`.
2. **Return:** `a` when the test holds, otherwise `b` — when they are equal, `b` is returned and it is the same value.

## Solution

```python solution time=O(1) space=O(1)
class Solution:
    # Function to return the larger of two integers
    def maxOfTwo(self, a: int, b: int) -> int:
        if a > b:
            return a
        return b


# Reads the test case's a, e.g. 3
a = int(input())
# Reads the test case's b, e.g. 7
b = int(input())
print(Solution().maxOfTwo(a, b))
```

```java solution time=O(1) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the larger of two integers
        int maxOfTwo(int a, int b) {
            if (a > b) {
                return a;
            }
            return b;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's a, e.g. 3
        int a = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's b, e.g. 7
        int b = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().maxOfTwo(a, b));
    }
}
```

## Complexity Analysis

**Time Complexity:** O(1), one comparison.

**Space Complexity:** O(1), no extra storage.

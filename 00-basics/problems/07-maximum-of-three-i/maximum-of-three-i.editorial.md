## Intuition

Keep a running answer. Start by assuming `a` is the largest, then let `b` and then `c` challenge it: each one replaces the running answer only if it is strictly greater. After two challenges the running answer is the maximum — the same idea scales to any number of values, which is why it beats a tangle of `if a > b and a > c` conditions.

## Approach

1. **Assume:** `largest = a`.
2. **Challenge with `b`:** if `b > largest`, set `largest = b`.
3. **Challenge with `c`:** if `c > largest`, set `largest = c`.
4. **Return `largest`.**

## Solution

```python solution time=O(1) space=O(1)
class Solution:
    # Function to return the largest of three integers
    def maxOfThree(self, a: int, b: int, c: int) -> int:
        largest = a
        if b > largest:
            largest = b
        if c > largest:
            largest = c
        return largest


# Reads the test case's a, e.g. 3
a = int(input())
# Reads the test case's b, e.g. 9
b = int(input())
# Reads the test case's c, e.g. 5
c = int(input())
print(Solution().maxOfThree(a, b, c))
```

```java solution time=O(1) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the largest of three integers
        int maxOfThree(int a, int b, int c) {
            int largest = a;
            if (b > largest) {
                largest = b;
            }
            if (c > largest) {
                largest = c;
            }
            return largest;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's a, e.g. 3
        int a = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's b, e.g. 9
        int b = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's c, e.g. 5
        int c = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().maxOfThree(a, b, c));
    }
}
```

## Complexity Analysis

**Time Complexity:** O(1), two comparisons.

**Space Complexity:** O(1), one extra variable.

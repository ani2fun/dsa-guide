## Intuition

"Both positive" is one condition joined by *and*; "both negative" is another; the answer is one **or** the other. Written out, `(a > 0 and b > 0) or (a < 0 and b < 0)` is the whole solution — the operators compose the two checks without any branching.

## Approach

1. **Both positive:** `a > 0 and b > 0`.
2. **Both negative:** `a < 0 and b < 0`.
3. **Combine:** the pair shares a sign when either check holds, so join them with `or` and return the result. A zero fails both halves on its own.

## Solution

```python solution time=O(1) space=O(1)
class Solution:
    # Function to check whether two integers share a sign
    def sameSign(self, a: int, b: int) -> bool:
        return (a > 0 and b > 0) or (a < 0 and b < 0)


# Reads the test case's a, e.g. 3
a = int(input())
# Reads the test case's b, e.g. 5
b = int(input())
print("true" if Solution().sameSign(a, b) else "false")
```

```java solution time=O(1) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to check whether two integers share a sign
        boolean sameSign(int a, int b) {
            return (a > 0 && b > 0) || (a < 0 && b < 0);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's a, e.g. 3
        int a = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's b, e.g. 5
        int b = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().sameSign(a, b));
    }
}
```

## Complexity Analysis

**Time Complexity:** O(1), four comparisons.

**Space Complexity:** O(1), no extra storage.

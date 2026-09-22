## Intuition

Every term needs only the two before it, so there is no reason to store the whole sequence: keep `prev` and `curr`, and on each step slide the window forward — the new `curr` is their sum, the new `prev` is the old `curr`. After `n - 1` slides from `(F(0), F(1))`, `curr` holds `F(n)`.

## Approach

1. **Handle `n = 0`:** return 0 — the loop below starts from `F(1)`.
2. **Start** with `prev = 0` (`F(0)`) and `curr = 1` (`F(1)`).
3. **Repeat for positions 2 to `n`:** compute `next = prev + curr`, then shift: `prev = curr`, `curr = next`.
4. **Return `curr`.** With `n <= 40`, `F(40) = 102334155` fits comfortably in a 32-bit integer.

## Solution

```python solution time=O(N) space=O(1)
class Solution:
    # Function to return the nth Fibonacci number, with F(0) = 0 and F(1) = 1
    def fibonacci(self, n: int) -> int:
        if n == 0:
            return 0

        prev, curr = 0, 1   # F(0), F(1)
        for _ in range(2, n + 1):
            prev, curr = curr, prev + curr
        return curr


# Reads the test case's n, e.g. 5
n = int(input())
print(Solution().fibonacci(n))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the nth Fibonacci number, with F(0) = 0 and F(1) = 1
        int fibonacci(int n) {
            if (n == 0) {
                return 0;
            }

            int prev = 0, curr = 1;  // F(0), F(1)
            for (int i = 2; i <= n; i++) {
                int next = prev + curr;
                prev = curr;
                curr = next;
            }
            return curr;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's n, e.g. 5
        int n = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().fibonacci(n));
    }
}
```

## Complexity Analysis

**Time Complexity:** O(N), one loop iteration per position from 2 to n.

**Space Complexity:** O(1), two variables regardless of n.

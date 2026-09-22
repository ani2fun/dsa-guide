## Intuition

`n % 10` is always the last digit and `n / 10` (integer division) is the number with that digit removed. Repeating the pair until nothing is left visits every digit exactly once, from the right, so a running total collects the sum without ever turning the number into a string.

## Approach

1. **Start** with `total = 0`.
2. **While `n > 0`:** add `n % 10` to `total`, then replace `n` with `n // 10` (Java: `n / 10`).
3. **Return `total`.** For `n = 0` the loop never runs and the answer is 0, which is correct.

## Solution

```python solution time=O(log₁₀(N)) space=O(1)
class Solution:
    # Function to return the sum of the digits of n
    def sumOfDigits(self, n: int) -> int:
        total = 0
        while n > 0:
            total += n % 10   # the last digit
            n //= 10          # drop it
        return total


# Reads the test case's n, e.g. 123
n = int(input())
print(Solution().sumOfDigits(n))
```

```java solution time=O(log₁₀(N)) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the sum of the digits of n
        int sumOfDigits(int n) {
            int total = 0;
            while (n > 0) {
                total += n % 10;  // the last digit
                n /= 10;          // drop it
            }
            return total;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's n, e.g. 123
        int n = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().sumOfDigits(n));
    }
}
```

## Complexity Analysis

**Time Complexity:** O(log₁₀(N)), one iteration per digit.

**Space Complexity:** O(1), one accumulator.

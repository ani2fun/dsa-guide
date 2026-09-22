## Intuition

An even number is one that 2 divides exactly, and the remainder operator `%` reports exactly that: `n % 2` is 0 for every even `n`. Comparing the remainder with 0 — rather than with 1 — is what makes the test correct for negatives as well, because Java's `-3 % 2` is `-1`, not `1`.

## Approach

1. **Receive input:** capture the integer `n`.
2. **Test the remainder:** `n % 2 == 0` means even.
3. **Print the verdict:** `Even` when the test holds, `Odd` otherwise.

## Solution

```python solution time=O(1) space=O(1)
class Solution:
    # Function to print whether a number is even or odd
    def evenOrOdd(self, n: int) -> None:
        if n % 2 == 0:
            print("Even")
        else:
            print("Odd")


# Reads the test case's n, e.g. 4
n = int(input())
Solution().evenOrOdd(n)
```

```java solution time=O(1) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to print whether a number is even or odd
        void evenOrOdd(int n) {
            if (n % 2 == 0) {
                System.out.println("Even");
            } else {
                System.out.println("Odd");
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's n, e.g. 4
        int n = Integer.parseInt(sc.nextLine().trim());
        new Solution().evenOrOdd(n);
    }
}
```

## Complexity Analysis

**Time Complexity:** O(1), one remainder and one comparison.

**Space Complexity:** O(1), no extra storage.

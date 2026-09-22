## Intuition

The ten lines differ only in the multiplier, so a counter running from 1 to 10 generates them all: each iteration prints `n`, the counter, and their product. The formatting is fixed text around three numbers — build the line, print it, move on.

## Approach

1. **Receive input:** capture the integer `n`.
2. **Loop `i` from 1 to 10** (Python: `range(1, 11)`).
3. **Print each line** as `n x i = n*i`. In Java the product must be parenthesised inside string concatenation — `n + " = " + n * i` would multiply correctly, but writing `(n * i)` keeps the intent obvious.

## Solution

```python solution time=O(1) space=O(1)
class Solution:
    # Function to print the multiplication table of n from 1 to 10
    def printTable(self, n: int) -> None:
        for i in range(1, 11):
            print(f"{n} x {i} = {n * i}")


# Reads the test case's n, e.g. 5
n = int(input())
Solution().printTable(n)
```

```java solution time=O(1) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to print the multiplication table of n from 1 to 10
        void printTable(int n) {
            for (int i = 1; i <= 10; i++) {
                System.out.println(n + " x " + i + " = " + (n * i));
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's n, e.g. 5
        int n = Integer.parseInt(sc.nextLine().trim());
        new Solution().printTable(n);
    }
}
```

## Complexity Analysis

**Time Complexity:** O(1), always exactly ten iterations.

**Space Complexity:** O(1), one loop counter.

## Intuition

Each `input()` / `nextLine()` call consumes exactly one line, so three values on three lines are three calls in order — nothing more. Once the three integers are in variables, the sum is one expression.

## Approach

1. **Read `a`:** read the first line and convert it to an integer.
2. **Read `b` and `c`:** repeat for the second and third lines — the order of the reads is the order of the lines.
3. **Return the sum:** `a + b + c`, and let the driver print it.

## Solution

```python solution time=O(1) space=O(1)
class Solution:
    # Function to add three integers read from the user
    def sumOfThree(self, a: int, b: int, c: int) -> int:
        return a + b + c


# Reads the test case's a, e.g. 1
a = int(input())
# Reads the test case's b, e.g. 2
b = int(input())
# Reads the test case's c, e.g. 3
c = int(input())
print(Solution().sumOfThree(a, b, c))
```

```java solution time=O(1) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to add three integers read from the user
        int sumOfThree(int a, int b, int c) {
            return a + b + c;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's a, e.g. 1
        int a = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's b, e.g. 2
        int b = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's c, e.g. 3
        int c = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().sumOfThree(a, b, c));
    }
}
```

## Complexity Analysis

**Time Complexity:** O(1), three reads and one addition, regardless of the values.

**Space Complexity:** O(1), three integer variables.

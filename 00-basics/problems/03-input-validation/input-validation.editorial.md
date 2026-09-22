## Intuition

A range check is two comparisons joined by *and*: the value must be at least the lower bound **and** at most the upper bound. Either failing makes the input invalid, so one `if` with both conditions answers the question.

## Approach

1. **Receive input:** capture the integer `n`.
2. **Check the range:** `n >= 1 and n <= 100` — Python also allows the chained form `1 <= n <= 100`.
3. **Print the verdict:** `Valid` when the check holds, `Invalid` otherwise.

## Solution

```python solution time=O(1) space=O(1)
class Solution:
    # Function to check whether the input lies in the accepted range
    def validate(self, n: int) -> None:
        if 1 <= n <= 100:
            print("Valid")
        else:
            print("Invalid")


# Reads the test case's n, e.g. 50
n = int(input())
Solution().validate(n)
```

```java solution time=O(1) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to check whether the input lies in the accepted range
        void validate(int n) {
            if (n >= 1 && n <= 100) {
                System.out.println("Valid");
            } else {
                System.out.println("Invalid");
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's n, e.g. 50
        int n = Integer.parseInt(sc.nextLine().trim());
        new Solution().validate(n);
    }
}
```

## Complexity Analysis

**Time Complexity:** O(1), two comparisons.

**Space Complexity:** O(1), no extra storage.

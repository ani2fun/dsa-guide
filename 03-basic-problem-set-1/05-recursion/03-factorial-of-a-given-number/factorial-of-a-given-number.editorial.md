## Intuition

Finding the factorial of a number N using recursion involves visualizing the process of multiplying the number by each smaller positive integer down to 1. The approach is to repeatedly call the function, reducing the number by 1 each time. This continues until reaching the base case of 1. Imagine the factorial as a series of multiplications: starting with N, then multiplying by N-1, then by N-2, and so on, until multiplying by 1.

## Approach

1. Define a function that calculates the factorial of a number.
2. In the function, if the number is 0 or 1, return 1 (base case).
3. Otherwise, return the number multiplied by the factorial of the number minus 1 (recursive case).

## Solution

```python solution time=O(N) space=O(N)
class Solution:
    # Function to find the factorial of n
    def factorial(self, n: int) -> int:
        # Base case: factorial of 0 or 1 is 1
        if n <= 1:
            return 1
        # Recursive case: n * factorial of n-1
        return n * self.factorial(n - 1)


# Reads the test case's n
n = int(input())
print(Solution().factorial(n))
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the factorial of n
        public long factorial(int n) {
            // Base case: factorial of 0 or 1 is 1
            if (n <= 1) return 1;
            // Recursive case: n * factorial of n-1
            return n * factorial(n - 1);
        }
    }

    public static void main(String[] args) {
        // Reads the test case's n
        int n = new Scanner(System.in).nextInt();
        System.out.println(new Solution().factorial(n));
    }
}
```

## Complexity Analysis

- **Time Complexity:** O(N) — the function makes N recursive calls to reach the base case, so the time complexity is proportional to the number of recursive calls.
- **Space Complexity:** O(N) — the call stack grows with each recursive call, using N stack frames, so the space complexity is proportional to the depth of recursion.

<div style="border-left:4px solid #da5233;background:rgba(218,82,51,0.08);padding:0.6rem 1rem;border-radius:0 0.5rem 0.5rem 0;margin:1.25rem 0">

⚠️ **Note.** For very large numbers, recursion can lead to a stack overflow due to too many nested function calls.

</div>

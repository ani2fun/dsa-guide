## Intuition

To solve the problem of finding the sum of digits in a given number using recursion, the approach revolves around breaking down the problem into smaller, manageable parts. The key idea is to isolate the last digit of the number and add it to the result of a recursive call with the remaining digits. This process continues until the number reduces to a single digit. At each step, the last digit can be obtained using the modulus operation, and the rest of the number can be obtained using integer division. This recursive approach ensures that each digit is processed individually and accumulated to form the final sum.

## Approach

1. **Base Case:** If the number is 0, return 0 as there are no more digits to process.
2. **Recursive Case:** Compute the last digit of the number using number % 10. Compute the remaining number by performing integer division number / 10. Make a recursive call with the remaining number and add the last digit to the result of this call.

## Solution

```python solution time=O(log N) space=O(log N)
class Solution:

    # Method to compute the sum of digits of given number
    def addDigits(self, num: int) -> int:
        # Base case: if the number is a single digit, return it
        if num < 10:
            return num

        # Recursive case: sum the digits and continue
        sum_digits = self.sumDigits(num)

        return self.addDigits(sum_digits)

    # Helper function to add the sum of digits recursively
    def sumDigits(self, num: int) -> int:
        # Base case: If the number is 0, return 0
        if num == 0:
            return 0

        # Recursive case
        return self.sumDigits(num // 10) + (num % 10)


# Reads the test case's num
num = int(input())
print(Solution().addDigits(num))
```

```java solution time=O(log N) space=O(log N)
import java.util.*;

public class Main {
    static class Solution {

        // Method to compute the sum of digits of given number
        public int addDigits(int num) {
            // Base case: if the number is a single digit, return it
            if (num < 10) {
                return num;
            }

            // Recursive case: sum the digits and continue
            int sum = sumDigits(num);

            return addDigits(sum);
        }

        // Helper function to add the sum of digits recursively
        private int sumDigits(int num) {
            // Base case: If the number is 0, return 0
            if (num == 0) return 0;

            // Recursive case
            return sumDigits(num / 10) + (num % 10);
        }
    }

    public static void main(String[] args) {
        // Reads the test case's num
        int num = new Scanner(System.in).nextInt();
        System.out.println(new Solution().addDigits(num));
    }
}
```

## Complexity Analysis

- **Time Complexity:** O(log N) — each recursive call processes a number with fewer digits than the previous call, leading to logarithmic time complexity in terms of the number of digits.
- **Space Complexity:** O(log N) — this space is required for the recursion stack, which grows with the number of digits in the number.

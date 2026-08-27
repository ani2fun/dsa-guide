---
title: "Check If A Number Is Prime Or Not"
summary: "Decide whether a number is prime by testing divisors up to its square root."
essential: true
kind: problem
difficulty: easy
topics: [recursion, maths]
---

# Check If A Number Is Prime Or Not

Given an integer num, return true if it is prime otherwise false.

A prime number is a number that is divisible only by 1 and itself.

### Example 1

> - **Input :** num = 5
> - **Output :** true
> - **Explanation :**
> The factors of 5 are 1 and 5 only. So it satisfies the prime number condition.

### Example 2

> - **Input :** num = 15
> - **Output :** false
> - **Explanation :**
> The factors of 15 are 1, 3, 5, 15 only. As the number has factors other than 1 and itself, So it is not a prime number.

### Example 3

> - **Input :** num = 41
> - **Output :** true

## Constraints

> - `1 <= num <= 10⁴`

```python run
class Solution:
    # Function to check if the given number is prime or not
    def checkPrime(self, num: int) -> bool:
        # Your code goes here.
        pass


# Reads the test case's num
num = int(input())
print("true" if Solution().checkPrime(num) else "false")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to check if the given number is prime or not
        boolean checkPrime(int num) {
            // Your code goes here.
            return false;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's num
        int num = new Scanner(System.in).nextInt();
        System.out.println(new Solution().checkPrime(num));
    }
}
```

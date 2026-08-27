---
title: "Sum Of Digits In A Given Number"
summary: "Repeatedly add a number's digits until a single digit remains, using recursion."
essential: true
kind: problem
difficulty: easy
topics: [recursion, maths]
---

# Sum Of Digits In A Given Number

Given an integer num, repeatedly add all its digits until the result has only one digit, and return it.

### Example 1

> - **Input :** num = 529
> - **Output :** 7
> - **Explanation :**
> In first iteration the digits sum will be = 5 + 2 + 9 => 16. In second iteration the digits sum will be 1 + 6 => 7. Now single digit is remaining , so we return it.

### Example 2

> - **Input :** num = 101
> - **Output :** 2
> - **Explanation :**
> In first iteration the digits sum will be = 1 + 0 + 1 => 2. Now single digit is remaining , so we return it.

### Example 3

> - **Input :** num = 38
> - **Output :** 2

## Constraints

> - `0 <= num <= 2³¹ - 1`

```python run
class Solution:
    # Function to repeatedly add the digits of num until one digit remains
    def addDigits(self, num: int) -> int:
        # Your code goes here.
        pass


# Reads the test case's num
num = int(input())
print(Solution().addDigits(num))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to repeatedly add the digits of num until one digit remains
        int addDigits(int num) {
            // Your code goes here.
            return 0;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's num
        int num = new Scanner(System.in).nextInt();
        System.out.println(new Solution().addDigits(num));
    }
}
```

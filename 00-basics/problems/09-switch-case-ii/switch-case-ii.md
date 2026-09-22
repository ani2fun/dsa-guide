---
title: "Switch Case II"
summary: "Dispatch on a string — apply add, subtract, multiply or divide to two integers, or print Invalid."
essential: true
kind: problem
difficulty: easy
topics: [basics, conditionals]
---

# Switch Case II

Complete the function `calculate` which takes a string `op` and two integers `a` and `b`, and prints the result of applying the operation named by `op` to `a` and `b`:

- `add` → `a + b`
- `subtract` → `a - b`
- `multiply` → `a * b`
- `divide` → `a / b` as integer division, discarding the fractional part (so `9 / 2` is `4` and `-9 / 2` is `-4`)

For any other string print `Invalid`. Operation names are case-sensitive, and `b` is never 0 when `op` is `divide`.

## Example 1

> **Input :** op = add, a = 3, b = 4  
> **Output :** 7  
> **Explanation :** 3 + 4 = 7

## Example 2

> **Input :** op = divide, a = 9, b = 2  
> **Output :** 4  
> **Explanation :** 9 / 2 = 4.5, and the fractional part is discarded.

## Example 3

> **Input :** op = power, a = 2, b = 3  
> **Output :** Invalid  
> **Explanation :** `power` is not one of the four operations.

## Constraints

- `-1000 <= a, b <= 1000`
- `b != 0` when `op` is `divide`
- `op` has at most 20 lowercase letters

```python run
class Solution:
    # Function to apply the operation named by op to a and b
    def calculate(self, op: str, a: int, b: int) -> None:
        # Your code goes here — print the result, or "Invalid".
        pass


# Reads the test case's op, e.g. add
op = input().strip()
# Reads the test case's a, e.g. 3
a = int(input())
# Reads the test case's b, e.g. 4
b = int(input())
Solution().calculate(op, a, b)
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to apply the operation named by op to a and b
        void calculate(String op, int a, int b) {
            // Your code goes here — print the result, or "Invalid".
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's op, e.g. add
        String op = sc.nextLine().trim();
        // Reads the test case's a, e.g. 3
        int a = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's b, e.g. 4
        int b = Integer.parseInt(sc.nextLine().trim());
        new Solution().calculate(op, a, b);
    }
}
```

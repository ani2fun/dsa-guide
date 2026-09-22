---
title: "Logical Operators"
summary: "Decide whether two integers share a sign using and / or in a single expression."
essential: true
kind: problem
difficulty: easy
topics: [basics, conditionals]
---

# Logical Operators

Complete the function `sameSign` which takes two integers `a` and `b` and returns `true` if both are positive or both are negative, and `false` otherwise.

Zero is neither positive nor negative, so any pair containing 0 returns `false`.

## Example 1

> **Input :** a = 3, b = 5  
> **Output :** true  
> **Explanation :** Both are positive.

## Example 2

> **Input :** a = -2, b = -9  
> **Output :** true  
> **Explanation :** Both are negative.

## Example 3

> **Input :** a = 4, b = -1  
> **Output :** false  
> **Explanation :** One is positive and the other negative.

## Example 4

> **Input :** a = 0, b = 5  
> **Output :** false  
> **Explanation :** 0 has no sign, so the pair does not share one.

## Constraints

`-1000 <= a, b <= 1000`

```python run
class Solution:
    # Function to check whether two integers share a sign
    def sameSign(self, a: int, b: int) -> bool:
        return False


# Reads the test case's a, e.g. 3
a = int(input())
# Reads the test case's b, e.g. 5
b = int(input())
print("true" if Solution().sameSign(a, b) else "false")
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to check whether two integers share a sign
        boolean sameSign(int a, int b) {
            return false;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's a, e.g. 3
        int a = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's b, e.g. 5
        int b = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().sameSign(a, b));
    }
}
```

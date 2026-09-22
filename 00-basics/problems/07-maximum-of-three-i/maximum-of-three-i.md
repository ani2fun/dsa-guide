---
title: "Maximum of Three - I"
summary: "Return the largest of three integers by carrying the best so far through two comparisons."
essential: true
kind: problem
difficulty: easy
topics: [basics, conditionals]
---

# Maximum of Three - I

Complete the function `maxOfThree` which takes three integers `a`, `b` and `c` and returns the largest of the three. If two or more are equal and largest, return that value.

## Example 1

> **Input :** a = 3, b = 9, c = 5  
> **Output :** 9  
> **Explanation :** 9 is the largest.

## Example 2

> **Input :** a = -1, b = -7, c = -4  
> **Output :** -1  
> **Explanation :** -1 is the largest of three negatives.

## Example 3

> **Input :** a = 8, b = 8, c = 2  
> **Output :** 8  
> **Explanation :** 8 appears twice; the answer is 8.

## Constraints

`-1000 <= a, b, c <= 1000`

```python run
class Solution:
    # Function to return the largest of three integers
    def maxOfThree(self, a: int, b: int, c: int) -> int:
        return 0


# Reads the test case's a, e.g. 3
a = int(input())
# Reads the test case's b, e.g. 9
b = int(input())
# Reads the test case's c, e.g. 5
c = int(input())
print(Solution().maxOfThree(a, b, c))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the largest of three integers
        int maxOfThree(int a, int b, int c) {
            return 0;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's a, e.g. 3
        int a = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's b, e.g. 9
        int b = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's c, e.g. 5
        int c = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().maxOfThree(a, b, c));
    }
}
```

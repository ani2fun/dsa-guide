---
title: "Maximum of Two - I"
summary: "Return the larger of two integers with a single comparison."
essential: true
kind: problem
difficulty: easy
topics: [basics, conditionals]
---

# Maximum of Two - I

Complete the function `maxOfTwo` which takes two integers `a` and `b` and returns the larger of the two. If they are equal, return that value.

## Example 1

> **Input :** a = 3, b = 7  
> **Output :** 7  
> **Explanation :** 7 is larger than 3.

## Example 2

> **Input :** a = 10, b = 2  
> **Output :** 10  
> **Explanation :** 10 is larger than 2.

## Example 3

> **Input :** a = 5, b = 5  
> **Output :** 5  
> **Explanation :** Both are 5, so the answer is 5.

## Constraints

`-1000 <= a, b <= 1000`

```python run
class Solution:
    # Function to return the larger of two integers
    def maxOfTwo(self, a: int, b: int) -> int:
        return 0


# Reads the test case's a, e.g. 3
a = int(input())
# Reads the test case's b, e.g. 7
b = int(input())
print(Solution().maxOfTwo(a, b))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to return the larger of two integers
        int maxOfTwo(int a, int b) {
            return 0;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's a, e.g. 3
        int a = Integer.parseInt(sc.nextLine().trim());
        // Reads the test case's b, e.g. 7
        int b = Integer.parseInt(sc.nextLine().trim());
        System.out.println(new Solution().maxOfTwo(a, b));
    }
}
```

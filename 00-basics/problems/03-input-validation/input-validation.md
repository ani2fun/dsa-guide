---
title: "Input Validation"
summary: "Print Valid when an integer lies in 1..100 and Invalid otherwise — checking input before using it."
essential: true
kind: problem
difficulty: easy
topics: [basics, conditionals]
---

# Input Validation

Complete the function `validate` which takes an integer `n` and prints `Valid` if `n` lies between 1 and 100, both inclusive, and `Invalid` otherwise.

Ensure only the first letter of the answer is capitalised.

## Example 1

> **Input :** n = 50  
> **Output :** Valid  
> **Explanation :** 50 lies in the range 1 to 100.

## Example 2

> **Input :** n = 0  
> **Output :** Invalid  
> **Explanation :** 0 is below the lower bound 1.

## Example 3

> **Input :** n = 100  
> **Output :** Valid  
> **Explanation :** The bounds are inclusive, so 100 is valid.

## Constraints

`-10⁴ <= n <= 10⁴`

```python run
class Solution:
    # Function to check whether the input lies in the accepted range
    def validate(self, n: int) -> None:
        # Your code goes here — print "Valid" or "Invalid".
        pass


# Reads the test case's n, e.g. 50
n = int(input())
Solution().validate(n)
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to check whether the input lies in the accepted range
        void validate(int n) {
            // Your code goes here — print "Valid" or "Invalid".
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

---
title: "Print Multiplication Table - I"
summary: "Print the multiplication table of n from 1 to 10, one product per line."
essential: true
kind: problem
difficulty: easy
topics: [basics, loops]
---

# Print Multiplication Table - I

Complete the function `printTable` which takes an integer `n` and prints its multiplication table from 1 to 10 — ten lines, each of the form `n x i = n×i`, with single spaces around `x` and `=`.

For `n = 3` the first two lines are `3 x 1 = 3` and `3 x 2 = 6`.

## Example 1

> **Input :** n = 5  
> **Output :**
>
> ```text
> 5 x 1 = 5
> 5 x 2 = 10
> 5 x 3 = 15
> 5 x 4 = 20
> 5 x 5 = 25
> 5 x 6 = 30
> 5 x 7 = 35
> 5 x 8 = 40
> 5 x 9 = 45
> 5 x 10 = 50
> ```

## Example 2

> **Input :** n = -2  
> **Output :**
>
> ```text
> -2 x 1 = -2
> -2 x 2 = -4
> -2 x 3 = -6
> -2 x 4 = -8
> -2 x 5 = -10
> -2 x 6 = -12
> -2 x 7 = -14
> -2 x 8 = -16
> -2 x 9 = -18
> -2 x 10 = -20
> ```  
> **Explanation :** The products of a negative number are negative.

## Constraints

`-100 <= n <= 100`

```python run
class Solution:
    # Function to print the multiplication table of n from 1 to 10
    def printTable(self, n: int) -> None:
        # Your code goes here — print ten lines, n x 1 = … through n x 10 = ….
        pass


# Reads the test case's n, e.g. 5
n = int(input())
Solution().printTable(n)
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to print the multiplication table of n from 1 to 10
        void printTable(int n) {
            // Your code goes here — print ten lines, n x 1 = … through n x 10 = ….
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Reads the test case's n, e.g. 5
        int n = Integer.parseInt(sc.nextLine().trim());
        new Solution().printTable(n);
    }
}
```

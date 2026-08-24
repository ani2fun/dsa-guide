---
title: "Pattern 14"
summary: "Print n rows of the alphabet, each row growing by one more letter."
essential: true
kind: problem
difficulty: easy
topics: [patterns, loops]
---

# Pattern 14

Given an integer n. You need to recreate the pattern given below for any value of N. Let's say for N = 5, the pattern should look like as below:

> ```text
> A
> AB
> ABC
> ABCD
> ABCDE
> ```

Print the pattern in the function given to you.

### Example 1

> - **Input :** n = 4
> - **Output :**
> ```text
> A
> AB
> ABC
> ABCD
> ```

### Example 2

> - **Input :** n = 2
> - **Output :**
> ```text
> A
> AB
> ```

## Constraints

> `1 <= n <= 26`

```python run
class Solution:
    # Function to print pattern14
    def pattern14(self, n: int) -> None:
        # Your code goes here — print n rows, row i holding the first i+1 letters of the alphabet.
        pass


# Reads the test case's n, e.g. 4
n = int(input())
Solution().pattern14(n)
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to print pattern14
        void pattern14(int n) {
            // Your code goes here — print n rows, row i holding the first i+1 letters of the alphabet.
        }
    }

    public static void main(String[] args) {
        // Reads the test case's n, e.g. 4
        int n = new Scanner(System.in).nextInt();
        new Solution().pattern14(n);
    }
}
```

## Fun facts
> - This programming problem trains you in understanding and manipulating strings, which is a fundamental concept in software development.
> - In real-world applications, this exercise could apply to systems requiring hierarchical data representation or nested data structures.
> - For instance, consider a file manager where files/folders are nested within other folders.
> - Each level of the hierarchy could be represented by a different letter of the alphabet, giving a visual indicator of the current depth in the hierarchy.
> - Likewise, file paths in Unix-like operating systems could be shown using this pattern, with each subsequent directory represented by an additional alphabet letter.
> - This problem can also have its applications in generating different patterns which is a key aspect of creating graphs or visualizations in software applications.

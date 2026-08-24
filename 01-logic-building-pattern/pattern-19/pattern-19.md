---
title: "Pattern 19"
summary: "Print a hollow hourglass of stars that narrows to a single column in the middle and widens back out."
essential: true
kind: problem
difficulty: easy
topics: [patterns, loops]
---

# Pattern 19

Given an integer n. You need to recreate the pattern given below for any value of N. Let's say for N = 5, the pattern should look like as below:

> ```
> **********
> ****  ****
> ***    ***
> **      **
> *        *
> *        *
> **      **
> ***    ***
> ****  ****
> **********
> ```

Print the pattern in the function given to you.

### Example 1

> - **Input :** n = 4
> - **Output :**
> ```
> ********
> ***  ***
> **    **
> *      *
> *      *
> **    **
> ***  ***
> ********
> ```

### Example 2

> - **Input :** n = 2
> - **Output :**
> ```
> ****
> *  *
> *  *
> ****
> ```

## Constraints

> `1 <= n <= 100`

```python run
class Solution:
    # Function to print pattern19
    def pattern19(self, n: int) -> None:
        # Your code goes here — print a hollow hourglass that narrows to a point and widens back out.
        pass


# Reads the test case's n, e.g. 4
n = int(input())
Solution().pattern19(n)
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to print pattern19
        void pattern19(int n) {
            // Your code goes here — print a hollow hourglass that narrows to a point and widens back out.
        }
    }

    public static void main(String[] args) {
        // Reads the test case's n, e.g. 4
        int n = new Scanner(System.in).nextInt();
        new Solution().pattern19(n);
    }
}
```

## Fun facts
> - The concept underlying this problem, pattern generation, is frequently used in various aspects of software development.
> - For example, in game development, similar algorithms are introduced to generate unique textures or to progress game levels.
> - In data visualization libraries and apps, pattern generation algorithms are used to create aesthetically pleasing and easy to understand visual representations of data.
> - Furthermore, ASCII art, which is similar to this problem, has applications in stylizing console output and creating visually appealing comment blocks in code.

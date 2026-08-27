---
title: "Sum Of First N Numbers"
summary: "Return the sum of the first N natural numbers using recursion."
essential: true
kind: problem
difficulty: easy
topics: [recursion]
---

# Sum Of First N Numbers

Given an integer N, return the sum of first N natural numbers. Try to solve this using recursion.

### Example 1

> - **Input :** N = 4
> - **Output :** 10
> - **Explanation :**
> first four natural numbers are 1, 2, 3, 4. Sum is 1 + 2 + 3 + 4 => 10.

### Example 2

> - **Input :** N = 2
> - **Output :** 3
> - **Explanation :**
> first two natural numbers are 1, 2. Sum is 1 + 2 => 3.

### Example 3

> - **Input :** N = 10
> - **Output :** 55

## Constraints

> - `1 <= N <= 10^3`

```python run
class Solution:
    # Function to get the sum of first N natural numbers
    def NnumbersSum(self, N: int) -> int:
        # Your code goes here.
        pass


# Reads the test case's N
N = int(input())
print(Solution().NnumbersSum(N))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to get the sum of first N natural numbers
        int NnumbersSum(int N) {
            // Your code goes here.
            return 0;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's N
        int N = new Scanner(System.in).nextInt();
        System.out.println(new Solution().NnumbersSum(N));
    }
}
```

## Fun facts

- The concept of summing up the first N natural numbers is often used in the development of performance analysis and benchmarking tools. These tools help developers understand the performance of their software by simulating a series of operations, such as calculating how long it takes to sum up a series of numbers, and then analyze the time complexity. The principle also has real-world usages in databases when dealing with sequence generation or serial numbers, and in building progress bar logic in numerous softwares or apps.

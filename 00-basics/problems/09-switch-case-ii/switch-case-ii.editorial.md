## Intuition

A `switch` is not only for numbers: Java switches on a `String` and Python's `match` on any value, so the operation name can drive the dispatch directly. Each case does its arithmetic and prints; the `default` (Python `case _`) is where every unknown name lands, which is what makes the `Invalid` branch impossible to forget.

## Approach

1. **Receive input:** the operation name `op`, then the integers `a` and `b`.
2. **Dispatch on `op`:** one case per operation name — `add`, `subtract`, `multiply`, `divide` — each printing its result.
3. **Divide carefully:** Java's `/` on integers already truncates toward zero; in Python use `int(a / b)`, because `a // b` rounds toward negative infinity and would print -5 for -9 / 2.
4. **Default:** any other name prints `Invalid`.

## Solution

```python solution time=O(1) space=O(1)
class Solution:
    # Function to apply the operation named by op to a and b
    def calculate(self, op: str, a: int, b: int) -> None:
        match op:
            case "add":
                print(a + b)
            case "subtract":
                print(a - b)
            case "multiply":
                print(a * b)
            case "divide":
                # int() truncates toward zero, like integer division in Java;
                # a // b would round -4.5 down to -5 instead.
                print(int(a / b))
            case _:
                print("Invalid")


# Reads the test case's op, e.g. add
op = input().strip()
# Reads the test case's a, e.g. 3
a = int(input())
# Reads the test case's b, e.g. 4
b = int(input())
Solution().calculate(op, a, b)
```

```java solution time=O(1) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to apply the operation named by op to a and b
        void calculate(String op, int a, int b) {
            switch (op) {
                case "add":
                    System.out.println(a + b);
                    break;
                case "subtract":
                    System.out.println(a - b);
                    break;
                case "multiply":
                    System.out.println(a * b);
                    break;
                case "divide":
                    // Integer division in Java truncates toward zero
                    System.out.println(a / b);
                    break;
                default:
                    System.out.println("Invalid");
            }
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

## Complexity Analysis

**Time Complexity:** O(1), one dispatch and one arithmetic operation.

**Space Complexity:** O(1), no extra storage.

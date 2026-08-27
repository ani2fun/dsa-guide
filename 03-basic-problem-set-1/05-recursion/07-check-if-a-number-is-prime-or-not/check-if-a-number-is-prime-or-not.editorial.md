## Brute

*Recursive divisor check*

### Intuition

To check if a number is prime, determine if it has any divisors other than 1 and itself. Using recursion, systematically check for divisors from 2 up to the square root of the number. If any divisor within this range is found, the number is not prime. If no divisors are found by the time the square root of the number is reached, the number is prime.

### Approach

1. First, handle the base cases: If the number is less than or equal to 1, return false because 0 and 1 are not prime. If the number is greater than 1, start checking for divisibility from 2.
2. Define a recursive helper function prime(num, x) where num is the number to be checked and x is the current divisor to check.
3. In the helper function — if x is greater than the square root of num, return true indicating that num is a prime number. If num is divisible by x (i.e., num % x == 0), return false indicating that num is not a prime number. If neither condition is met, recursively call the function with the next divisor x + 1.

### Solution

```python solution time=O(√N) space=O(√N)
class Solution:
    def checkPrime(self, num: int) -> bool:
        if num <= 1:
            return False  # 0 and 1 are not prime numbers
        return self.prime(num, 2)  # Call the helper function to check for primality

    def prime(self, num: int, x: int) -> bool:
        # Base case: x > sqrt(num), so the number is prime
        if x > num ** 0.5:
            return True
        if num % x == 0:
            # Found a divisor, so the number is not prime
            return False
        # Recursive call with the next divisor
        return self.prime(num, x + 1)


# Reads the test case's num
num = int(input())
print("true" if Solution().checkPrime(num) else "false")
```

```java solution time=O(√N) space=O(√N)
import java.util.*;

public class Main {
    static class Solution {
        public boolean checkPrime(int num) {
            // 0 and 1 are not prime numbers
            if (num <= 1) {
                return false;
            }
            // Call the helper function to check for primality
            return prime(num, 2);
        }

        private boolean prime(int num, int x) {
            if (x > Math.sqrt(num)) {
                return true;
            }
            // Found a divisor, so the number is not prime
            if (num % x == 0) {
                return false;
            }
            // Recursive call with the next divisor
            return prime(num, x + 1);
        }
    }

    public static void main(String[] args) {
        // Reads the test case's num
        int num = new Scanner(System.in).nextInt();
        System.out.println(new Solution().checkPrime(num));
    }
}
```

### Complexity Analysis

- **Time Complexity:** O(√N) — because we only need to check for divisors up to the square root of the number.
- **Space Complexity:** O(√N) — due to the recursion stack depth, which can grow up to the square root of the number.

## Optimal

*Wheel Factorization Method*

### Intuition

Another approach to find whether the number is prime or not is by using the Wheel Factorization Method.

#### Wheel Factorization Method

It is an optimized method to check whether a number is prime by skipping numbers that are obviously not prime. For prime checking, the most common wheel is based on 2 and 3.

Every integer can be written in one of these forms: 6k, 6k+1, 6k+2, 6k+3, 6k+4, 6k+5, where k is an integer.

Now,

- 6k: Already divisible by 6. Cannot be prime.
- 6k+2: Even and divisible by 2. Cannot be prime.
- 6k+3: Divisible by 3. Cannot be prime.
- 6k+4: Even and divisible by 2. Cannot be prime.

So, after checking divisibility by 2 and 3, we only need to check numbers of the form: 6k-1 and 6k+1. This skips many unnecessary checks while still ensuring that no possible prime divisor is missed.

### Approach

1. If the number is less than or equal to 1, return false because prime numbers are greater than 1.
2. If the number is 2 or 3, return true because both are prime.
3. If the number is divisible by 2 or 3, return false because it has a divisor other than 1 and itself.
4. Now check only possible divisors of the form 6k - 1 and 6k + 1.
5. For every such pair, check whether the number is divisible by either of them.
6. If any divisor is found, return false.
7. If no divisor is found up to the square root of the number, return true.

### Edge Case

- If the given number is less than or equal to 1: Return false, because prime numbers are greater than 1.
- If the given number is 2 or 3: Return true, because both 2 and 3 are prime numbers.
- If the given number is divisible by 2 or 3: Return false, because it has a divisor other than 1 and itself.

### Solution

```python solution time=O(√N) space=O(1)
class Solution:
    # Function to check if the given number is prime or not.
    def checkPrime(self, num: int) -> bool:
        # Numbers less than or equal to 1 are not prime.
        if num <= 1:
            return False

        # 2 and 3 are prime numbers.
        if num <= 3:
            return True

        # If num is divisible by 2 or 3, it is not prime.
        if num % 2 == 0 or num % 3 == 0:
            return False

        # Check only numbers of the form 6k - 1 and 6k + 1.
        i = 5
        while i * i <= num:
            # Check both possible prime candidates around multiples of 6.
            if num % i == 0 or num % (i + 2) == 0:
                return False

            # Move to the next pair of possible divisors.
            i += 6

        # If no divisor is found, num is prime.
        return True


# Reads the test case's num
num = int(input())
print("true" if Solution().checkPrime(num) else "false")
```

```java solution time=O(√N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to check if the given number is prime or not.
        public boolean checkPrime(int num) {
            // Numbers less than or equal to 1 are not prime.
            if (num <= 1) {
                return false;
            }

            // 2 and 3 are prime numbers.
            if (num <= 3) {
                return true;
            }

            // If num is divisible by 2 or 3, it is not prime.
            if (num % 2 == 0 || num % 3 == 0) {
                return false;
            }

            // Check only numbers of the form 6k - 1 and 6k + 1.
            for (int i = 5; i * i <= num; i += 6) {
                // Check both possible prime candidates around multiples of 6.
                if (num % i == 0 || num % (i + 2) == 0) {
                    return false;
                }
            }

            // If no divisor is found, num is prime.
            return true;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's num
        int num = new Scanner(System.in).nextInt();
        System.out.println(new Solution().checkPrime(num));
    }
}
```

### Complexity Analysis

- **Time Complexity:** O(√N) — because we check possible divisors only up to the square root of the number.
- **Space Complexity:** O(1) — because no extra space is used; the loop replaces the recursion stack of the previous approach.

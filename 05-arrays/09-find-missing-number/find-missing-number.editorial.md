## Brute

*Linear search each candidate*

### Intuition

For each number between 0 to N, try to find it in the given array using linear search. And if any number is not found, return that number.

### Approach

1. Iterate let's say i from 0 to N & for each integer i, try to find it in the given array using linear search.
2. To find the number, run another loop and consider a flag variable to indicate if the element exists in the array, where flag when set to 1 means the element is present and flag when set to 0 means the element is missing.
3. Initially, the flag value will be set to 0. While iterating the array, if we find the element, set the flag to 1 and break out from the loop. Now, for any number i, if its not found the flag will remain 0 even after iterating the whole array and will return the number.

### Solution

```python solution time=O(N²) space=O(1)
from typing import List

class Solution:
    # Function to find the missing number
    def missingNumber(self, nums: List[int]) -> int:
        # Calculate N from the length of nums
        N = len(nums)

        # Outer loop that runs from 0 to N
        for i in range(0, N+1):
            """ Flag variable to check
            if an element exists"""
            flag = 0

            """ Search for the element
            using linear search"""
            for num in nums:
                if num == i:
                    # i is present in the array
                    flag = 1
                    break

            """ Check if the element
            is missing (flag == 0)"""
            if flag == 0:
                return i

        """ The following line will never
        execute, it is just to avoid warnings"""
        return -1


# Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().missingNumber(nums))
```

```java solution time=O(N²) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the missing number
        int missingNumber(int[] nums) {
            // Calculate N from the length of nums
            int N = nums.length;

            // Outer loop that runs from 0 to N
            for (int i = 0; i <= N; i++) {
                /* Flag variable to check
                if an element exists*/
                int flag = 0;

                /* Search for the element
                using linear search*/
                for (int j = 0; j < N; j++) {
                    if (nums[j] == i) {
                        // i is present in the array
                        flag = 1;
                        break;
                    }
                }

                // Check if the element is missing (flag == 0)
                if (flag == 0) return i;
            }

            /* The following line will never
            execute, it is just to avoid warnings*/
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().missingNumber(nums));
    }

    // "[1, 2, 3]" -> {1, 2, 3}
    static int[] parseIntArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new int[0];
        String[] parts = inner.split(",");
        int[] out = new int[parts.length];
        for (int i = 0; i < parts.length; i++) out[i] = Integer.parseInt(parts[i].trim());
        return out;
    }
}
```

### Complexity Analysis

- **Time Complexity:** O(N²), where N is the size of the array. In the worst case i.e. if the missing number is N itself, the outer loop will run for N times, and for every single number the inner loop will also run for approximately N times. So, the total time complexity will be O(N²).
- **Space Complexity:** O(1) — as no extra space is used.

## Better

*Frequency array*

### Intuition

The better idea rather than linear search is to use the hashing technique by storing the frequency of each element of the given array. Any number whose frequency will be 0, will be returned as that will correspond to the missing value.

### Approach

1. The range of the number is 0 to N. So, create hash array of size N+1, as we want to store the frequency of N as well.
2. Now, for each element in the given array, store the frequency in the hash array.
3. Iterate the array and for each number between 0 to N, check the frequencies. And for any number, if the frequency is 0, return it.

### Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    # Function to find the missing number
    def missingNumber(self, nums: List[int]) -> int:
        N = len(nums)

        # Array to store frequencies, initialized to 0
        freq = [0] * (N + 1)

        # Storing the frequencies in the array
        for num in nums:
            freq[num] += 1

        # Checking the frequencies for numbers 0 to N
        for i in range(0, N + 1):
            if freq[i] == 0:
                return i

        """ This line will never execute,
        it is just to avoid warnings"""
        return -1


# Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().missingNumber(nums))
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the missing number
        int missingNumber(int[] nums) {
            int N = nums.length;

            // Array to store frequencies, initialized to 0
            int[] freq = new int[N+1];

            // Storing the frequencies in the array
            for (int num : nums) {
                freq[num]++;
            }

            // Checking the frequencies for numbers 0 to N
            for (int i = 0; i <= N; i++) {
                if (freq[i] == 0) {
                    return i;
                }
            }

            /* This line will never execute,
            it is just to avoid warnings */
            return -1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().missingNumber(nums));
    }

    // "[1, 2, 3]" -> {1, 2, 3}
    static int[] parseIntArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new int[0];
        String[] parts = inner.split(",");
        int[] out = new int[parts.length];
        for (int i = 0; i < parts.length; i++) out[i] = Integer.parseInt(parts[i].trim());
        return out;
    }
}
```

### Complexity Analysis

- **Time Complexity:** O(N) + O(N) = O(2N), where N is size of the array + 1. For storing the frequencies in the hash array, the program takes O(N) time complexity and for checking the frequencies in the second step again O(N) is required.
- **Space Complexity:** O(N), where N is size of the array + 1, as extra hash space is used.

## Optimal 1

*Sum formula*

### Intuition

The optimal is based on simple mathematics, where addition and summation of series is involved.

Ideally while solving this problem, if you think of calculating the sum of natural numbers from 0 to N and also compute the sum of all elements in the array separately. Then, just by subtracting the two results, we can easily identify the missing number. This missing number would not have been included in the sum of all elements of the given array.

### Approach

1. Calculate the summation of first N natural numbers (i.e. 1 to N) using the formula (N*(N+1))/2 and store in variable sum1.
2. Then add all the array elements by iterating in the array and store it in variable sum2.
3. Finally, consider the difference between the sum1 and sum2, return it.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    # Function to find the missing number
    def missingNumber(self, nums: List[int]) -> int:
        # Calculate N from the length of nums
        N = len(nums)

        # Summation of first N natural numbers
        sum1 = (N * (N + 1)) // 2

        # Summation of all elements in nums
        sum2 = sum(nums)

        # Calculate the missing number
        missingNum = sum1 - sum2

        # Return the missing number
        return missingNum


# Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().missingNumber(nums))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the missing number
        int missingNumber(int[] nums) {
            // Calculate N from the length of nums
            int N = nums.length;

            // Summation of first N natural numbers
            int sum1 = (N * (N + 1)) / 2;

            // Summation of all elements in nums
            int sum2 = 0;
            for (int num : nums) {
                sum2 += num;
            }

            // Calculate the missing number
            int missingNum = sum1 - sum2;

            // Return the missing number
            return missingNum;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().missingNumber(nums));
    }

    // "[1, 2, 3]" -> {1, 2, 3}
    static int[] parseIntArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new int[0];
        String[] parts = inner.split(",");
        int[] out = new int[parts.length];
        for (int i = 0; i < parts.length; i++) out[i] = Integer.parseInt(parts[i].trim());
        return out;
    }
}
```

### Complexity Analysis

- **Time Complexity:** O(N), where N is size of array, to compute the sum of the array elements.
- **Space Complexity:** O(1) — as no extra space is used.

## Optimal 2

*XOR*

### Intuition

Another optimal approach, uses the below property of XOR to find the missing number.

- XOR of two same numbers is 0.
- The XOR of a number with 0 is the number itself.

Understand that on calculating the XOR of all numbers from 1 to N we make sure that each number is included. After that on calculating the XOR of all the elements in the array & then performing XOR these two results, all the numbers present in the final result will appear twice expect for the one which is missing. Hence the number occurring twice turn out 0 satisfying first condition, and then followed by 0 ^ missing number, leaving the missing number itself.

### Approach

1. Initialize two variables xor1, xor2 as 0. xor1 variable will calculate the XOR of 1 to N.
2. Calculate the XOR of all the elements in the array by xor2 = xor2 ^ arr[i].
3. Finally, the answer will be the XOR of xor1 and xor2.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    # Function to find the missing number
    def missingNumber(self, nums: List[int]) -> int:
        xor1 = 0
        xor2 = 0

        # Calculate XOR of all array elements
        for i in range(len(nums)):
            xor1 ^= (i + 1)  # XOR up to [1...N]
            xor2 ^= nums[i]  # XOR of array elements

        # XOR of xor1 and xor2 gives missing number
        return xor1 ^ xor2


# Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().missingNumber(nums))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find missing number in array
        int missingNumber(int[] nums) {
            int xor1 = 0, xor2 = 0;

            // Calculate XOR of all array elements
            for (int i = 0; i < nums.length; i++) {
                xor1 = xor1 ^ (i + 1); // XOR up to [1...N]
                xor2 = xor2 ^ nums[i]; // XOR of array elements
            }

            // XOR of xor1 and xor2 gives missing number
            return (xor1 ^ xor2);
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 2, 3, 1, 4]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().missingNumber(nums));
    }

    // "[1, 2, 3]" -> {1, 2, 3}
    static int[] parseIntArray(String line) {
        String inner = line.trim().replaceAll("^\\[|\\]$", "").trim();
        if (inner.isEmpty()) return new int[0];
        String[] parts = inner.split(",");
        int[] out = new int[parts.length];
        for (int i = 0; i < parts.length; i++) out[i] = Integer.parseInt(parts[i].trim());
        return out;
    }
}
```

### Complexity Analysis

- **Time Complexity:** O(N) — a single pass computes the XOR of 1..N and the XOR of the array elements together.
- **Space Complexity:** O(1) — as no extra space is used.

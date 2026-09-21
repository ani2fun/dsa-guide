## Brute

*Sort, then walk back from the end*

### Intuition

To find the second largest element in an array, one simple way is to use sorting. By sorting the array in ascending order, the largest element will be surely at the last index, and the second largest element will be at the second-to-last index.

> **What if there are fewer than 2 elements in an array ?**
> There would not be any second largest element for this case, so returned value will be -1.

> **What if last and second last element turn out as same ?**
> If the second-to-last element is equal to the last element, continue checking the preceding elements until a different value is found. This approach guarantees that correct identification of the second largest element is made.

### Approach

1. Initialize 2 variables largest, and secondLargest. Initialize secondLargest to -1 as initially there shall be no second largest element.
2. Sort the array and update largest with last element of array.
3. Now iterate the array from second to last index and if the element is not equal to the largest, update secondLargest to that element and break out once secondLargest is updated. Return the value stored in secondLargest.

### Solution

```python solution time=O(N log N) space=O(N)
from typing import List

class Solution:

    # Function to find the second largest element
    def secondLargestElement(self, nums: List[int]) -> int:
        n = len(nums)

        # Check if the array has less than 2 elements
        if n < 2:
            # Indicating no second largest element is possible
            return -1

        # Sort the list in ascending order
        nums.sort()

        # Largest element will be at last index
        largest = nums[-1]

        secondLargest = -1

        # Traverse the sorted list from right to left
        for i in range(n-2, -1, -1):

            ''' If the current element is not
            equal to the largest element'''
            if nums[i] != largest:

                ''' Assign the current element
                as the second largest and break'''
                secondLargest = nums[i]
                break

        # Return the second largest element
        return secondLargest


# Reads the test case's nums, e.g. [8, 8, 7, 6, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().secondLargestElement(nums))
```

```java solution time=O(N log N) space=O(log N)
import java.util.*;

public class Main {
    static class Solution {

        // Function to find the second largest element
        public int secondLargestElement(int[] nums) {
            int n = nums.length;

            // Check if the array has less than 2 elements
            if (n < 2) {
                // Indicating no second largest element is possible
                return -1;
            }

            // Sort the array in ascending order
            Arrays.sort(nums);

            // Largest element will be at last index
            int largest = nums[n - 1];

            int secondLargest = -1;

            // Traverse the sorted array from right to left
            for (int i = n - 2; i >= 0; i--) {

                /* If the current element is not
                equal to the largest element*/
                if (nums[i] != largest) {

                    /* Assign the current element
                    as the second largest and break*/
                    secondLargest = nums[i];
                    break;
                }
            }

            // Return the second largest element
            return secondLargest;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [8, 8, 7, 6, 5]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().secondLargestElement(nums));
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

- **Time Complexity:** O(N log N) — the sort dominates; the backward scan that follows is a single O(N) pass.
- **Space Complexity:** O(log N) in Java, where `Arrays.sort` on primitives is a dual-pivot quicksort and the cost is its recursion stack. Python's `sort()` is Timsort, which needs O(N) auxiliary space in the worst case.

## Better

*Two passes, no sorting*

### Intuition

To optimise the solution further the idea is to eliminate sorting. Traverse the array once to find the largest element. Perform a second traversal to find the largest element that is smaller than the largest element found.

> **What if there are fewer than 2 elements?**
> When there are fewer than 2 elements in an array, there would not be any second largest element, so return -1.

### Approach

1. Initialize two variables largest, and secondLargest to INT_MIN.
2. Iterate the array and find the largest element.
3. In the second iteration check if the element is greater than secondLargest and also not equal to largest, then update the secondLargest. Return secondLargest.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:

    def secondLargestElement(self, nums: List[int]) -> int:
        # Get the length of the array
        n = len(nums)

        # Check if the array has less than 2 elements
        if n < 2:
            # If true, return -1 indicating there is no second largest element
            return -1

        # Initialize variables to store the largest and second largest elements
        largest = float('-inf')
        secondLargest = float('-inf')

        # First traversal to find the largest element
        for i in range(n):
            largest = max(largest, nums[i])

        # Second traversal to find second largest element
        for i in range(n):
            if nums[i] > secondLargest and nums[i] != largest:
                secondLargest = nums[i]

        # Return the second largest element
        return -1 if secondLargest == float('-inf') else secondLargest


# Reads the test case's nums, e.g. [8, 8, 7, 6, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().secondLargestElement(nums))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        public int secondLargestElement(int[] nums) {
            int n = nums.length;

            // Check if the array has less than 2 elements
            if (n < 2) {
                // If true, return -1
                // Exit the method
                return -1;
            }

            /*Initialize variables to store the
           largest and second largest elements*/
            int largest = Integer.MIN_VALUE;
            int secondLargest = Integer.MIN_VALUE;

            // First traversal to find the largest element
            for (int i = 0; i < n; i++) {
                largest = Math.max(largest, nums[i]);
            }

            // Second traversal to find second largest element
            for (int i = 0; i < n; i++) {
                if (nums[i] > secondLargest  && nums[i] != largest) {
                    secondLargest = nums[i];
                }
            }

            // Return the second largest element
            return secondLargest == Integer.MIN_VALUE ? -1 : secondLargest;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [8, 8, 7, 6, 5]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().secondLargestElement(nums));
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

- **Time Complexity:** O(N) + O(N) = O(2N), due to two linear traversals, where N is the length of the array.
- **Space Complexity:** O(1), as no additional space is required.

## Optimal

*Single traversal*

### Intuition

To find the second-largest element in an array more efficiently, the idea is to perform the operation in a single traversal by making smart comparisons. This approach uses two variables to keep track of the largest and the second-largest elements while iterating through the array. This will help to find the second-largest element with just one pass throughout the array.

> **What if there are fewer than 2 elements?**
> When there are fewer than 2 elements in an array, there would not be any second largest element, so return -1.

### Approach

1. Initialize two variables: largest, and secondLargest. Initialize largest and secondLargest to INT_MIN as initially none of them should be holding any values.
2. If the current element is larger than largest, update secondLargest and largest.
3. Else if the current element is larger than secondLargest and not equal to largest, update secondLargest.
4. Traverse the entire array to update the second largest element in declared variable i.e, secondLargest.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    def secondLargestElement(self, nums: List[int]) -> int:

        if len(nums) < 2:
            return -1

        largest =  float('-inf')
        second_largest =  float('-inf')

        for num in nums:

            if num > largest:
                second_largest = largest
                largest = num

            elif num > second_largest and num != largest:
                second_largest = num

        return -1 if second_largest == float('-inf') else second_largest


# Reads the test case's nums, e.g. [8, 8, 7, 6, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().secondLargestElement(nums))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Method for second largest element in the array
        public int secondLargestElement(int[] nums) {

            // Check if the array has less than 2 elements
            if (nums.length < 2) {
                // If true, return -1 there is no second largest element
                return -1;
            }

            /* Initialize variables to store the
            largest and second largest elements */
            int largest = Integer.MIN_VALUE;
            int secondLargest = Integer.MIN_VALUE;

            /*Single traversal to find the largest
           and second largest elements*/
            for (int i = 0; i < nums.length; i++) {

                if (nums[i] > largest) {
                    secondLargest = largest;
                    largest = nums[i];
                }
                else if (nums[i] > secondLargest && nums[i] != largest) {
                    secondLargest = nums[i];
                }

            }

            // Return the second largest element
            return secondLargest == Integer.MIN_VALUE ?  -1 : secondLargest;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [8, 8, 7, 6, 5]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().secondLargestElement(nums));
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

- **Time Complexity:** O(N), because the solution involves a single traversal, where N is the length of the array.
- **Space Complexity:** O(1), as no additional space is required.

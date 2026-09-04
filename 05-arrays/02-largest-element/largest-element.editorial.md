## Brute

*Using sorting*

### Intuition

Imagine being a teacher and having a list of marks obtained by your students in a recent test. The task is to find out which student scored the highest marks. One simple way to do this is by sorting the marks in ascending order and then taking the last element from the sorted list.

### Approach

1. Sort the array in ascending order using in-built methods.
2. Return the element at the last index of the array.

### Solution

```python solution time=O(N log N) space=O(N)
from typing import List

class Solution:
    def largestElement(self, nums: List[int]) -> int:
        # Sort the list
        nums.sort()

        # Largest element will be
        # at the last index of the list
        largest = nums[-1]

        # Return the largest element
        return largest


# Reads the test case's nums, e.g. [3, 3, 6, 1]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().largestElement(nums))
```

```java solution time=O(N log N) space=O(log N)
import java.util.*;

public class Main {
    static class Solution {
        public int largestElement(int[] nums) {
            // Sort array
            Arrays.sort(nums);

            /*Largest element will be at
            the last index of the array.*/
            int largest = nums[nums.length - 1];

            //Return the largest element in array.
            return largest;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [3, 3, 6, 1]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().largestElement(nums));
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

- **Time Complexity:** O(N log N) — as we are sorting the array, where N is the length of the array.
- **Space Complexity:** O(log N) in Java, where `Arrays.sort` on primitives is a dual-pivot quicksort and the cost is its recursion stack. Python's `sort()` is Timsort, which needs O(N) auxiliary space in the worst case.

## Optimal

*Single traversal*

### Intuition

Imagine being a teacher having a list of marks obtained by your students in a recent test. The ask is to find out which student scored the highest marks.

Now to find the highest marks in the list, keep track of the marks encountered so far in a variable, let's say maxi. Starting value of maxi will be the first marksheet's marks as initially that will the maximum.

Then go checking each marksheet one by one and keep comparing and updating maxi as and when a marks greater than current marks stored in maxi is found. This will ensure that once we have all the marksheets checked we will have maximum marks stored in the variable maxi.

### Approach

1. Create a max variable and initialize it with arr[0], as in the beginning the first element should be maximum.
2. Iterate in the array and compare it with other elements to update the maximum.
3. If any element is greater than the max value, update max value with the element's value and at last return the max.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    def largestElement(self, nums: List[int]) -> int:
        # Initialize max_val as the first element
        max_val = nums[0]

        # Traverse the entire list
        for num in nums[1:]:

            """
            If the current element is greater
            than max_val, update max_val
            """
            if num > max_val:
                max_val = num

        # Return the largest element found
        return max_val


# Reads the test case's nums, e.g. [3, 3, 6, 1]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().largestElement(nums))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        public int largestElement(int[] nums) {
            // Initialize max as the first element
            int max = nums[0];

            // Traverse the entire array
            for (int i = 1; i < nums.length; i++) {

                /* If current element is greater
                than max, update max*/
                if (nums[i] > max) {
                    max = nums[i];
                }

            }
            // Return the largest element found
            return max;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [3, 3, 6, 1]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().largestElement(nums));
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

- **Time Complexity:** O(N) — since there is linear traversal of the array, where N is the length of the array.
- **Space Complexity:** O(1) — as only a couple of variables are used.

## Brute

### Intuition

As the array contains positive and negative elements, we can think of segregating the array elements into two parts. The first array will contain only positive elements and the second array will contain only negative elements. After this, we can just put the elements back in the original array alternatively. As the question states that positive elements should come first, so put positive element first and then negative one and so on. At the end of the process the original array will contain the desired result.

### Approach

1. Since the number of positive and negative elements are the same, we put positives into an array called "pos" and negatives into an array called "neg".
2. After segregating each of the positive and negative elements, we start putting them alternatively back into the original array.
3. Initialize an array which will run from 0 till (sizeOfArray/2 - 1) because the number of positive and negative elements are equal, so the total count of any of them will be equal to (sizeOfArray/2).
4. Since the array must begin with a positive number and the start index is 0, so all the positive numbers would be placed at even indices (2*i) and negatives at the odd indices (2*i+1), where i is the index of the pos or neg array while traversing them simultaneously.

### Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    # Function to rearrange the given array by signs
    def rearrangeArray(self, nums: List[int]) -> List[int]:
        n = len(nums)

        """ Define 2 vectors, one for storing positive
        and other for negative elements of the array."""
        pos = []
        neg = []

        # Segregate the array into positives and negatives.
        for num in nums:
            if num > 0:
                pos.append(num)
            else:
                neg.append(num)

        # Positives on even indices, negatives on odd.
        for i in range(n // 2):
            nums[2 * i] = pos[i]
            nums[2 * i + 1] = neg[i]

        # Return the result
        return nums


# Reads the test case's nums, e.g. [2, 4, 5, -1, -3, -4]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().rearrangeArray(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to rearrange the given array by signs
        int[] rearrangeArray(int[] nums) {
            int n = nums.length;

            /* Define 2 vectors, one for storing positive
            and other for negative elements of the array.*/
            List<Integer> pos = new ArrayList<>();
            List<Integer> neg = new ArrayList<>();

            // Segregate the array into positives and negatives.
            for (int i = 0; i < n; i++) {
                if (nums[i] > 0) pos.add(nums[i]);
                else neg.add(nums[i]);
            }

            // Positives on even indices, negatives on odd.
            for (int i = 0; i < n / 2; i++) {
                nums[2 * i] = pos.get(i);
                nums[2 * i + 1] = neg.get(i);
            }

            // Return the result
            return nums;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [2, 4, 5, -1, -3, -4]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().rearrangeArray(nums)));
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

- **Time Complexity:** O(N + N/2), where N is the size of the array. O(N) for traversing the array once for segregating positives and negatives and another O(N/2) for adding those elements alternatively to the array.
- **Space Complexity:** O(N/2 + N/2) = O(N), N/2 space required to store each of the positive and negative elements in separate arrays.

## Optimal

### Intuition

Consider having a group of kids, and you need them to line up for a photo such that they alternate between wearing red shirts and blue shirts, and the line starts with a red shirt. Let's say there are equal numbers of kids wearing red and blue shirts.

Begin with the first position designated for a kid wearing a red shirt. The second position is for a kid wearing a blue shirt.

After calling out the kids, place the first red shirt kid at the first position. Then place the first blue shirt kid at the second position. Continue this process, placing each subsequent red shirt kid at the next available "red" position, and each blue shirt kid at the next available "blue" position.

### Approach

1. Initialize two variable posIndex as 0 and negIndex as 1 initially.
2. Now, iterate in the array & on encountering the first negative element, understand that its first position in resultant array should be starting from index 1, as initially positive number will be placed. And then each time when a negative number is found, its next position would be 2 steps ahead considering that a positive number will occupy space in between 2 negative numbers. So increment the position of negative number by 2.
3. Similarly, when you encounter the first positive element, it occupies the position at index 0 in the resultant array, and then each time on finding a positive number, put it on the posIndex and it increments by 2.
4. When both the negIndex and posIndex exceed the size of the array, stop the iteration as the whole array is now rearranged alternatively according to the sign.

### Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    # Function to rearrange elements by their sign
    def rearrangeArray(self, nums: List[int]) -> List[int]:
        n = len(nums)

        # Initialize a result vector of size n
        ans = [0] * n

        # Initialize indices for positive and negative elements
        posIndex, negIndex = 0, 1

        # Traverse through each element in nums
        for i in range(n):
            if nums[i] < 0:

                """ If current element is negative,
                place it at the next odd index in ans"""
                ans[negIndex] = nums[i]
                # Move to the next odd index
                negIndex += 2

            else:
                ans[posIndex] = nums[i]

                # Move to the next even index
                posIndex += 2

        # Return the rearranged array
        return ans


# Reads the test case's nums, e.g. [2, 4, 5, -1, -3, -4]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().rearrangeArray(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to rearrange elements by their sign
        int[] rearrangeArray(int[] nums) {
            int n = nums.length;

            // Initialize a result vector of size n
            int[] ans = new int[n];

             /* Initialize indices for positive
             and negative elements*/
            int posIndex = 0, negIndex = 1;

            // Traverse through each element in nums
            for (int i = 0; i < n; i++) {
                if (nums[i] < 0) {

                    /* If current element is negative, place
                    it at the next odd index in ans*/
                    ans[negIndex] = nums[i];
                    // Move to the next odd index
                    negIndex += 2;

                } else {
                    ans[posIndex] = nums[i];

                    // Move to the next even index
                    posIndex += 2;

                }
            }

            // Return the rearranged array
            return ans;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [2, 4, 5, -1, -3, -4]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().rearrangeArray(nums)));
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

- **Time Complexity:** O(N), for traversing the array only once where N is the length of the array.
- **Space Complexity:** O(N) to store the resultant array.

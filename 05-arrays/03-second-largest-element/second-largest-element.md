---
title: "Second Largest Element"
summary: "Return the second-largest distinct element in an array, or -1 when there isn't one."
essential: true
kind: problem
difficulty: easy
topics: [arrays]
---

# Second Largest Element

Given an array of integers nums, return the second-largest element in the array. If the second-largest element does not exist, return -1.

### Example 1

> - **Input :** nums = [8, 8, 7, 6, 5]
> - **Output :** 7
> - **Explanation :**
> The largest value in nums is 8, the second largest is 7.

### Example 2

> - **Input :** nums = [10, 10, 10, 10, 10]
> - **Output :** -1
> - **Explanation :**
> The only value in nums is 10, so there is no second largest value, thus -1 is returned.

### Example 3

> - **Input :** nums = [7, 7, 2, 2, 10, 10, 10]
> - **Output :** 7

## Constraints

> - `1 <= nums.length <= 10⁵`
> - `-10⁴ <= nums[i] <= 10⁴`
> - `nums may contain duplicate elements.`

```python run
from typing import List

class Solution:
    # Function to find the second largest element
    def secondLargestElement(self, nums: List[int]) -> int:
        # Your code goes here.
        return -1


# Reads the test case's nums, e.g. [8, 8, 7, 6, 5]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().secondLargestElement(nums))
```

```java run
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the second largest element
        int secondLargestElement(int[] nums) {
            // Your code goes here.
            return -1;
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

## Frequently Occurring Doubts

### What happens if the array has fewer than two elements?

If the array has fewer than two elements, there is no second-largest element. Return -1 to indicate this scenario. Example: Input: nums = [7] Output: -1

### How does the algorithm handle arrays with identical elements?

If all elements are identical, there is no second-largest distinct value. Return -1 in this case. Example: Input: nums = [4, 4, 4] Output: -1

## Follow-ups

### How would you handle finding the second-largest element in a stream of data?

For a stream of data (where elements arrive one at a time): Maintain two variables, largest and second_largest, initialized to -∞. Update these variables dynamically as new elements arrive. Example: Stream: [2, 5, 1, 8, 3] Process: Start with largest = −∞, second_largest = −∞. After processing the stream: largest = 8, second_largest = 5.

### Can you solve this problem using a different approach, such as heap data structures?

Yes, a min-heap of size 2 can be used to maintain the two largest elements: Insert the first two elements into the heap. For each new element, compare it with the smallest element in the heap. If it is larger, replace the smallest element. At the end, the heap will contain the two largest elements. Example: Input: nums = [3, 1, 4, 2] Heap after processing: [3, 4] Output: 3 (second-largest element).

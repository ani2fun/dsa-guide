## Intuition

Quick Sort is a divide-and-conquer algorithm like Merge Sort. However, unlike Merge Sort, Quick Sort does not use an extra array for sorting (though it uses an auxiliary stack space). This makes Quick Sort slightly better than Merge Sort from a space perspective.

This algorithm follows two simple steps repeatedly:

- Pick a pivot and place it in its correct position in the sorted array.
- Move smaller elements (i.e., smaller than the pivot) to the left of the pivot and larger ones to the right.

**To summarize:** The main goal is to place the pivot at its final position in each recursion call, where it should be in the final sorted array.

## Approach

To implement Quick Sort, we will create two functions: quickSort() and partition().

**quickSort(arr[], low, high)**

1. **Initial Setup:** The low pointer points to the first index, and the high pointer points to the last index of the array.
2. **Partitioning:** Use the partition() function to get the index where the pivot should be placed after sorting. This index, called the partition index, separates the left and right unsorted subarrays.
3. **Recursive Calls:** After placing the pivot at the partition index, recursively call quickSort() for the left and right subarrays. The range of the left subarray will be [low to partition index - 1] and the range of the right subarray will be [partition index + 1 to high].
4. **Base Case:** The recursion continues until the range becomes 1.

**partition(arr[], low, high)**

1. Select pivot (random element) and swap it with the first element.
2. Use pointers i (low) and j (high). Move i forward to find element > pivot, and j backward to find element < pivot. Ensure i <= high - 1 and j >= low + 1.
3. If i < j, swap arr[i] and arr[j].
4. Continue until j < i.
5. Swap pivot (arr[low]) with arr[j] and return j as partition index.

This approach ensures that Quick Sort efficiently sorts the array using the divide-and-conquer strategy.

## Solution

```python solution time=O(N log N) space=O(N)
import random
from typing import List


class Solution:
    # Function to partition the array
    def partition(self, arr: List[int], low: int, high: int) -> int:
        # Choosing a random index between low and high
        randomIndex = low + random.randint(0, high - low)
        # Swap the random element with the first element
        arr[low], arr[randomIndex] = arr[randomIndex], arr[low]


        # Now choosing arr[low] as the pivot after the swap
        pivot = arr[low]
        # Starting index for left subarray
        left = low
        # Starting index for right subarray
        right = high


        while left < right:
            # Move left to the right until we find an element greater than the pivot
            while arr[left] <= pivot and left <= high - 1:
                left += 1
            # Move right to the left until we find an element smaller than the pivot
            while arr[right] > pivot and right >= low + 1:
                right -= 1
            # Swap elements at left and right if left is still less than right
            if left < right:
                arr[left], arr[right] = arr[right], arr[left]


        # Pivot placed in correct position
        arr[low], arr[right] = arr[right], arr[low]
        return right


    # Helper Function to perform the recursive quick sort
    def quickSortHelper(self, arr: List[int], low: int, high: int) -> None:
        # Base case: If the array has one or no elements, it's already sorted
        if low < high:
            # Get the partition index
            pIndex = self.partition(arr, low, high)
            # Sort the left subarray
            self.quickSortHelper(arr, low, pIndex - 1)
            # Sort the right subarray
            self.quickSortHelper(arr, pIndex + 1, high)


    # Function to perform quick sort on given array
    def quickSort(self, nums: List[int]) -> List[int]:
        # Get the size of array
        n = len(nums)


        # Perform quick sort
        self.quickSortHelper(nums, 0, n - 1)


        # Return sorted array
        return nums



# Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().quickSort(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N log N) space=O(N)
import java.util.*;


public class Main {
    static class Solution {
        // Function to partition the array
        public int partition(int[] arr, int low, int high) {


            // Choosing a random index between low and high
            int randomIndex = low + new Random().nextInt(high - low + 1);
            // Swap the random element with the first element
            swap(arr, low, randomIndex);


            // Now choosing arr[low] as the pivot after the swap
            int pivot = arr[low];
            int left = low;
            int right = high;


            while (left < right) {
                // Move left to the right until we find an element greater than pivot
                while (arr[left] <= pivot && left <= high - 1) {
                    left++;
                }
                // Move right to the left until we find an element smaller than pivot
                while (arr[right] > pivot && right >= low + 1) {
                    right--;
                }
                // Swap if valid
                if (left < right) {
                    swap(arr, left, right);
                }
            }


            // Place pivot in correct position
            swap(arr, low, right);
            return right;
        }


        // Helper Function to perform recursive quick sort
        public void quickSortHelper(int[] arr, int low, int high) {
            if (low < high) {
                int pIndex = partition(arr, low, high);
                quickSortHelper(arr, low, pIndex - 1);
                quickSortHelper(arr, pIndex + 1, high);
            }
        }


        // Function to perform quick sort
        public int[] quickSort(int[] nums) {
            quickSortHelper(nums, 0, nums.length - 1);
            return nums;
        }


        // Custom swap function
        private void swap(int[] arr, int i, int j) {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }


    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().quickSort(nums)));
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

## Complexity Analysis

- **Time Complexity:** O(N log N) — where N = size of the array. At each step, we divide the whole array, which takes log N steps, and N steps are taken for the partition() function, so overall time complexity will be N log N.
- **Space Complexity:** O(1) + O(N) auxiliary stack space, where N = size of the array.

The following recurrence relation can be written for Quick sort: `F(n) = F(k) + F(n-1-k)`. Here, k is the number of elements smaller or equal to the pivot and n-1-k denotes elements greater than the pivot.

There can be 2 cases:

- **Worst Case:** This case occurs when the pivot is the greatest or smallest element of the array. If the partition is done and the last element is the pivot, then the worst case would be either in the increasing order of the array or in the decreasing order of the array. Recurrence: `F(n) = F(0) + F(n-1)` or `F(n) = F(n-1) + F(0)`, giving a worst case time complexity of O(N²).
- **Best Case:** This case occurs when the pivot is the middle element or near to middle element of the array. Recurrence: `F(n) = 2F(n/2)`, giving a time complexity for the best and average case of O(N log N).

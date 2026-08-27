## Intuition

Merge Sort is a powerful sorting algorithm that follows the divide-and-conquer approach. The array is divided into two equal halves until each sub-array contains only one element. Each pair of smaller sorted arrays is then merged into a larger sorted array.

The algorithm consists of two main functions:

- **merge():** This function merges the two halves of the array, assuming both parts are already sorted.
- **mergeSort():** This function divides the array into 2 parts: low to mid and mid+1 to high where, low is the leftmost index of the array, high is the rightmost index of the array, and mid is the middle index of the array.

By repeating these steps recursively, Merge Sort efficiently sorts the entire array.

## Approach

To implement Merge Sort, we will create two functions: mergeSort() and merge().

**mergeSort(arr[], low, high)**

1. Divide the Array: Split the given array into two halves by splitting the range. For any range from low to high, the splits will be low to mid and mid+1 to high, where mid = (low + high) / 2. This process continues until the range size is 1.
2. Recursive Division: In mergeSort(), divide the array around the middle index by making recursive calls: mergeSort(arr, low, mid) for the left half and mergeSort(arr, mid+1, high) for the right half. Here, low is the leftmost index, high is the rightmost index, and mid is the middle index of the array.
3. Base Case: To complete the recursive function, define the base case. The recursion ends when the array has only one element left, meaning low and high are the same, pointing to a single element. If low >= high, the function returns.

**merge(arr[], low, mid, high)**

1. Use a temporary array to store the elements of the two sorted halves after merging. The range of the left half is from low to mid and the range of the right half is from mid+1 to high.
2. Use two pointers, left starting from low and right starting from mid+1. Using a while loop (while left <= mid && right <= high), compare the elements from each half and insert the smaller one into the temporary array. After the loop, any leftover elements in both halves are copied into the temporary array.
3. Transfer the elements from the temporary array back to the original array in the range low to high.

This approach ensures that the array is efficiently sorted using the divide-and-conquer strategy of Merge Sort.

## Solution

```python solution time=O(N log N) space=O(N)
from typing import List

class Solution:
    # Function to merge two sorted halves of the array
    def merge(self, arr: List[int], low: int, mid: int, high: int) -> None:
        # Temporary array to store merged elements
        temp = []
        left = low
        right = mid + 1

        # Loop until subarrays are exhausted
        while left <= mid and right <= high:
            # Compare left and right elements
            if arr[left] <= arr[right]:
                # Add left element to temp
                temp.append(arr[left])
                # Move left pointer
                left += 1
            else:
                # Add right element to temp
                temp.append(arr[right])
                # Move right pointer
                right += 1

        # Adding the remaining elements of left half
        while left <= mid:
            temp.append(arr[left])
            left += 1

        # Adding the remaining elements of right half
        while right <= high:
            temp.append(arr[right])
            right += 1

        # Transferring the sorted elements to arr
        for i in range(low, high + 1):
            arr[i] = temp[i - low]

    # Helper function to perform merge sort from low to high
    def mergeSortHelper(self, arr: List[int], low: int, high: int) -> None:
        # Base case: if the array has only one element
        if low >= high:
            return

        # Find the middle index
        mid = (low + high) // 2
        # Recursively sort the left half
        self.mergeSortHelper(arr, low, mid)
        # Recursively sort the right half
        self.mergeSortHelper(arr, mid + 1, high)
        # Merge the sorted halves
        self.merge(arr, low, mid, high)

    # Function to perform merge sort on the given array
    def mergeSort(self, nums: List[int]) -> List[int]:
        n = len(nums) # Size of array

        # Perform Merge sort on the whole array
        self.mergeSortHelper(nums, 0, n - 1)

        # Return the sorted array
        return nums


# Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().mergeSort(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N log N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to merge two sorted halves of the array
        public void merge(int[] arr, int low, int mid, int high) {
            // Temporary array to store merged elements
            List<Integer> temp = new ArrayList<>();
            int left = low;
            int right = mid + 1;

            // Loop until subarrays are exhausted
            while (left <= mid && right <= high) {
                // Compare left and right elements
                if (arr[left] <= arr[right]) {
                    // Add left element to temp
                    temp.add(arr[left]);
                    // Move left pointer
                    left++;
                } else {
                    // Add right element to temp
                    temp.add(arr[right]);
                    // Move right pointer
                    right++;
                }
            }

            // Adding the remaining elements of left half
            while (left <= mid) {
                temp.add(arr[left]);
                left++;
            }

            // Adding the remaining elements of right half
            while (right <= high) {
                temp.add(arr[right]);
                right++;
            }

            // Transferring the sorted elements to arr
            for (int i = low; i <= high; i++) {
                arr[i] = temp.get(i - low);
            }
        }

        // Helper function to perform merge sort from low to high
        public void mergeSortHelper(int[] arr, int low, int high) {
            // Base case: if the array has only one element
            if (low >= high)
                return;

            // Find the middle index
            int mid = (low + high) / 2;
            // Recursively sort the left half
            mergeSortHelper(arr, low, mid);
            // Recursively sort the right half
            mergeSortHelper(arr, mid + 1, high);
            // Merge the sorted halves
            merge(arr, low, mid, high);
        }

        // Function to perform merge sort on the given array
        public int[] mergeSort(int[] nums) {
            int n = nums.length; // Size of array

            // Perform Merge sort on the whole array
            mergeSortHelper(nums, 0, n - 1);

            // Return the sorted array
            return nums;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [7, 4, 1, 5, 3]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(Arrays.toString(new Solution().mergeSort(nums)));
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

- **Time Complexity:** O(N log N) — at each step, we divide the whole array, which takes log N steps, and we assume N steps are taken to sort the array. So, the overall time complexity is N log N.
- **Space Complexity:** O(N) — we are using a temporary array to store elements in sorted order.

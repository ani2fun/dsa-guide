## Brute

*Set, then copy back*

### Intuition

The naive way is to think of a data structure that does not store duplicate elements, that is HashSet. Keep track of unique elements in hashset, and at last copy all the elements from the HashSet to the original array.

### Approach

1. Declare a HashSet and traverse the array by putting every element of the array in the HashSet.
2. Store size of the set in a variable K. Now put all elements of the set in the array from the starting of the array and finally return K.

### Solution

```python solution time=O(N log N) space=O(N)
from typing import List

class Solution:
    # Function to remove duplicates from the array
    def removeDuplicates(self, nums: List[int]) -> int:

        # Set data structure to store unique elements
        s = set()

        # Add all elements from array to the set
        for val in nums:
            s.add(val)

        # Get the sorted list of unique elements
        sorted_unique = sorted(s)

        # Copy unique elements from sorted list to array
        for j in range(len(sorted_unique)):
            nums[j] = sorted_unique[j]

        # Return the number of unique elements
        return len(sorted_unique)


# Reads the test case's nums, e.g. [0, 0, 3, 3, 5, 6]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().removeDuplicates(nums))
```

```java solution time=O(N log N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to remove duplicates from the array
        int removeDuplicates(int[] nums) {

            // TreeSet to store unique elements in sorted order
            Set<Integer> s = new TreeSet<>();

            // Add all elements from array to the set
            for (int val : nums) {
                s.add(val);
            }

            // Get the number of unique elements
            int k = s.size();

            int j = 0;
            // Copy unique elements from set to array
            for (int val : s) {
                nums[j++] = val;
            }

            // Return the number of unique elements
            return k;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 0, 3, 3, 5, 6]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().removeDuplicates(nums));
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

- **Time Complexity:** O(N log N) + O(N) — for using hashset, it will take O(N log N), and also to traverse the array once O(N). Here N is the size of the array.
- **Space Complexity:** O(N) — because in the worst case, all the elements of the array can be unique and it will take O(N) space. Here N represents the size of the array.

## Optimal

*Two-pointer, in place*

### Intuition

Imagine you have a shelf where you keep your favorite books, and these books are sorted in alphabetical order. Over time, you notice that some books are repeated multiple times, and you want to organize the shelf so that each book title appears only once. Additionally, you don't want to change the order of the unique books on your shelf.

Here's what you would do:

Start at the beginning of the shelf and pick the first book. Look at the next book, if it's the same as the one just picked, then move on to the next book. If the next book is different, keep it next to the first book that is picked. Repeat this process for all books on the shelf.

Once all the books are checked, the first part of the shelf will have all the unique books in their original order. The rest of the books on the shelf don't matter, so ignore them.

### Approach

1. Initialize 2 variables i as 0 and variable j as 1, where i will track the position of the last unique element found and j will iterate through the array to find new unique elements.
2. Iterate in array using j from second element to the end of the array.
3. If the element at position j is different from the element at position i, it means a new unique element is found. This is because the array is sorted in non-decreasing order, so any new element that is different from the previous one must be unique.
4. When a new unique element is found, increment i to move to the next position for storing unique elements. Copy the element at position j to the new position at i. This ensures that the first i + 1 elements of the array are all unique.
5. Continue comparing elements and updating the array until j has iterated through the entire array. Once the loop completes, the value of i + 1 represents the number of unique elements in the array.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    # Function to remove duplicates from the list
    def removeDuplicates(self, nums: List[int]) -> int:

        # Initialize pointer for unique elements
        i = 0

        # Iterate through the list
        for j in range(1, len(nums)):
            """ If current element is different
            from the previous unique element"""
            if nums[i] != nums[j]:

                """ Move to the next position in
                the list for the unique element"""
                i += 1

                """ Update the current position
                with the unique element"""
                nums[i] = nums[j]

        # Return the number of unique elements
        return i + 1


# Reads the test case's nums, e.g. [0, 0, 3, 3, 5, 6]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
print(Solution().removeDuplicates(nums))
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to remove duplicates from the array
        int removeDuplicates(int[] nums) {

            // Initialize pointer for unique elements
            int i = 0;

            // Iterate through the array
            for (int j = 1; j < nums.length; j++) {
                /*If current element is different
                from the previous unique element*/
                if (nums[i] != nums[j]) {
                    /* Move to the next position in
                    the array for the unique element*/
                    i++;
                    /* Update the current position
                       with the unique element*/
                    nums[i] = nums[j];
                }
            }

            // Return the number of unique elements
            return i + 1;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 0, 3, 3, 5, 6]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().removeDuplicates(nums));
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

- **Time Complexity:** O(N) — for single traversal of the array, where N is the size of the array.
- **Space Complexity:** O(1) — not using any extra space.

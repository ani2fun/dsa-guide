## Brute

*Temporary array*

### Intuition

- Basic idea is to use temporary array(extra space) and store the non-zero numbers separately.
- Then place those elements back into the original array.
- This make sure that all the non-zero numbers are kept at the front of the array.
- And finally, fill the remaining positions in the array with zeros.

### Approach

1. First is declare a temporary array to store all the non-zero elements. This is done using traversing the original array and copy all non-zero elements to the temporary array.
2. After that overwrite the original array from starting positions (which is starting index `0` in this case) with the elements from the temporary array.
3. Finally, the remaining positions fill it with `0` in the original.

### Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    # Function to move zeroes to the end
    def moveZeroes(self, nums: List[int]) -> None:
        n = len(nums)

        """Create a temporary array
        to store non-zero elements"""
        temp = [0] * n
        count = 0

        # Copy non-zero elements to temp
        for i in range(n):
            if nums[i] != 0:
                temp[count] = nums[i]
                count += 1

        # Copy non-zero elements back to nums
        for i in range(count):
            nums[i] = temp[i]

        # Fill the rest with zeroes
        for i in range(count, n):
            nums[i] = 0


# Reads the test case's nums, e.g. [0, 1, 4, 0, 5, 2]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
Solution().moveZeroes(nums)
print("[" + ", ".join(str(x) for x in nums) + "]")
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to move zeroes to the end
        void moveZeroes(int[] nums) {
            int n = nums.length;

            // Create a temporary array to store non-zero elements
            int[] temp = new int[n];
            int count = 0;

            // Copy non-zero elements to temp
            for (int i = 0; i < n; i++) {
                if (nums[i] != 0) {
                    temp[count++] = nums[i];
                }
            }

            // Copy non-zero elements back to nums
            for (int i = 0; i < count; i++) {
                nums[i] = temp[i];
            }

            // Fill the rest with zeroes
            for (int i = count; i < n; i++) {
                nums[i] = 0;
            }
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 1, 4, 0, 5, 2]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        new Solution().moveZeroes(nums);
        System.out.println(Arrays.toString(nums));
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

- **Time Complexity:** O(2*N) — O(N) for copying non-zero elements from the original to the temporary array, O(X) for again copying it back from the temporary to the original array, and O(N-X) for filling zeros in the original array. Here N is the size of the array and X is the number of non-zero elements.
- **Space Complexity:** O(N) — for using a temporary array to solve this problem, and the maximum size of the array can be N in the worst case.

## Optimal

*Two-pointer, in place*

### Intuition

Imagine a long row of parking spots. Some hold cars (the non-zero numbers) and some are empty (the zeros). A valet is given one job: park all the cars tightly against the entrance end of the row, in the same order they're in now, so every empty spot ends up at the far end. Cars must never pass each other.

Working alone, the valet needs just one piece of equipment: a traffic cone.

- The valet walks down the row spot by spot, inspecting what's in each one. The valet is the fast pointer.
- The cone always marks the first empty spot past the already-packed cars — the next spot a car should be moved into. The cone is the slow pointer.

The routine is simple:

1. The valet steps to the next spot.
2. If it's empty, the valet walks on. A gap only matters once there's a car behind it.
3. If it holds a car, the valet drives that car to the spot the cone is marking. The car's old spot becomes empty — the car and the gap trade places. That's the swap.
4. The valet then moves the cone one spot forward, so it once again marks the first empty spot of the packed section.
5. Repeat until the valet has visited every spot.

Notice what happens at the start: the valet walks past a run of cars already parked at the front, and the cone just trails along spot for spot — no car actually moves (each car is "swapped" with itself). Only after the valet steps over the first empty spot does the cone fall behind, and from then on, every car the valet finds gets pulled forward past the gap.

By the end, every car sits at the front of the row, still in its original order — the valet moved them strictly in the order they were found — and all the empty spots have been squeezed to the far end.

### Approach

1. Start by taking two pointers, `i` and `j`. Initialize `j = 0`. The pointer `j` will track the position where the next non-zero element should be placed.
2. Walk through the array using pointer `i` from index `0` to `n − 1`.
3. Whenever `i` come across a non-zero element, swap the elements at positions `i` and `j`. This moves the non-zero element toward the front of the array.
4. After performing the swap, increment `j` by **1**. This updates `j` to the next position where the following non-zero element should be placed.
5. If the current element at `i` is zero, simply move `i` forward without making any changes.
6. Repeat the process until `i` reaches the end of the array. By the end of the traversal, all non-zero elements will be shifted to the front of the array in their original order, and all zeros will automatically move to the end.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        # j points to the position where next non-zero should go
        j = 0

        # Loop through each element in the array
        for i in range(len(nums)):
            # If current element is non-zero
            if nums[i] != 0:
                # Swap with the element at index j
                nums[i], nums[j] = nums[j], nums[i]

                # Move j forward
                j += 1


# Reads the test case's nums, e.g. [0, 1, 4, 0, 5, 2]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
Solution().moveZeroes(nums)
print("[" + ", ".join(str(x) for x in nums) + "]")
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        void moveZeroes(int[] nums) {
            // j keeps track of where the next non-zero should be placed
            int j = 0;

            // Loop through all elements
            for (int i = 0; i < nums.length; i++) {
                // If current element is non-zero
                if (nums[i] != 0) {
                    // Swap current element with the one at index j
                    int temp = nums[i];
                    nums[i] = nums[j];
                    nums[j] = temp;

                    // Move j forward
                    j++;
                }
            }
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [0, 1, 4, 0, 5, 2]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        new Solution().moveZeroes(nums);
        System.out.println(Arrays.toString(nums));
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

- **Time Complexity:** O(N), where N is size of the array, as we are traversing the array once.
- **Space Complexity:** O(1) — as no extra space is used to solve this problem.

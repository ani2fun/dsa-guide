## Brute

*Copy the rotated k, shift the rest*

### Intuition

To rotate an array by K positions to the left, consider that the first K elements of the array will move to the end, while the remaining elements will shift K positions to the left.

The thought process involves first capturing the first K elements in a temporary array. Next, shift each of the remaining elements from position K to the beginning of the array. Finally, append the temporarily stored elements to the end of the array. This approach ensures that the array is rotated to the left by K positions effectively.

### Approach

1. First, calculate the effective number of rotations by taking the modulo of K with the array size to avoid unnecessary rotations.
2. Create a temporary array to store the first K elements of the array.
3. Shift the remaining (N - K) elements of the array to the front.
4. Copy the stored K elements from the temporary array to the end of the array.
5. The array is now rotated to the left by K places.

### Solution

```python solution time=O(N) space=O(K)
from typing import List

class Solution:
    # Function to rotate the array to the left by k positions
    def rotateArray(self, nums: List[int], k: int) -> None:
        n = len(nums)  # Size of array
        k = k % n  # To avoid unnecessary rotations

        temp = []

        # Store first k elements in a temporary array
        for i in range(k):
            temp.append(nums[i])

        # Shift n-k elements of given array to the front
        for i in range(k, n):
            nums[i - k] = nums[i]

        # Copy back the k elements at the end
        for i in range(k):
            nums[n - k + i] = temp[i]


# Reads the test case's nums and k, one per line
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
k = int(input())
Solution().rotateArray(nums, k)
print("[" + ", ".join(str(x) for x in nums) + "]")
```

```java solution time=O(N) space=O(K)
import java.util.*;

public class Main {
    static class Solution {
        // Function to rotate the array to the left by k positions
        void rotateArray(int[] nums, int k) {
            int n = nums.length; // Size of array
            k = k % n; // To avoid unnecessary rotations

            int[] temp = new int[k];

            // Store first k elements in a temporary array
            for (int i = 0; i < k; i++) {
                temp[i] = nums[i];
            }

            // Shift n-k elements of given array to the front
            for (int i = k; i < n; i++) {
                nums[i - k] = nums[i];
            }

            // Copy back the k elements at the end
            for (int i = 0; i < k; i++) {
                nums[n - k + i] = temp[i];
            }
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums and k, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums = parseIntArray(sc.nextLine());
        int k = Integer.parseInt(sc.nextLine().trim());
        new Solution().rotateArray(nums, k);
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

- **Time Complexity:** O(N), where N is the length of the array. Three loops are used taking K, N-K, and K iterations respectively contributing to O(N+K). However, K can be N-1 in the worst case boiling down the time complexity as O(N).
- **Space Complexity:** O(K) — due to the temporary list created to copy the K elements.

## Optimal

*Three reversals*

### Intuition

The most optimal solution works based on the properties of reversing sections of the array. This involves reversing different parts of the array to achieve the desired rotation.

**Why does this solution work?**

- **Reversal Property:** Reversing a segment of the array changes the order but keeps the elements intact. By reversing the segments first and then the entire array, you rearrange the elements correctly without needing extra space.
- **Maintaining Order:** Each reversal step preserves the order of the elements within that segment, ensuring the elements that need to stay together remain so.

### Approach

1. Reverse the first k elements of the array. On reversing the first k elements, you are essentially reversing the order of the elements that will be moved to the back of the array. This prepares them to be placed at the end after the rotation.
2. Reverse the last N - K elements of the array. Reversing the remaining elements (from position k to the end of the array) ensures that these elements maintain their relative order after the rotation. They will come before the first k elements in the final arrangement.
3. Reverse the entire array. Finally, on reversal of the entire array, it combines the two previously reversed sections into the correct order. The first k elements (which were reversed first) are now at the end, and the last n-k elements (which were reversed second) are at the front, effectively achieving the left rotation.

### Solution

```python solution time=O(N) space=O(1)
from typing import List

class Solution:
    # Function to reverse the array between start and end
    def reverseArray(self, nums: List[int], start: int, end: int) -> None:
        while start < end:
            temp = nums[start]
            nums[start] = nums[end]
            nums[end] = temp
            start += 1
            end -= 1

    # Function to rotate the array to the left by k positions
    def rotateArray(self, nums: List[int], k: int) -> None:
        n = len(nums)  # Size of array
        k = k % n  # To avoid unnecessary rotations

        # Reverse the first k elements
        self.reverseArray(nums, 0, k - 1)

        # Reverse the last n-k elements
        self.reverseArray(nums, k, n - 1)

        # Reverse the entire array
        self.reverseArray(nums, 0, n - 1)


# Reads the test case's nums and k, one per line
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
k = int(input())
Solution().rotateArray(nums, k)
print("[" + ", ".join(str(x) for x in nums) + "]")
```

```java solution time=O(N) space=O(1)
import java.util.*;

public class Main {
    static class Solution {
        // Function to reverse the array between start and end
        private void reverseArray(int[] nums, int start, int end) {

            while (start < end) {
                int temp = nums[start];
                nums[start] = nums[end];
                nums[end] = temp;
                start++;
                end--;
            }
        }

        // Function to rotate the array to the left by k positions
        void rotateArray(int[] nums, int k) {
            int n = nums.length; // Size of array
            k = k % n; // To avoid unnecessary rotations

            // Reverse the first k elements
            reverseArray(nums, 0, k - 1);

            // Reverse the last n-k elements
            reverseArray(nums, k, n - 1);

            // Reverse the entire array
            reverseArray(nums, 0, n - 1);
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums and k, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums = parseIntArray(sc.nextLine());
        int k = Integer.parseInt(sc.nextLine().trim());
        new Solution().rotateArray(nums, k);
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

- **Time Complexity:** O(N), where N is the size of the array, as three reversals are performed taking O(k), O(N-k) and O(N) time respectively.
- **Space Complexity:** O(1) — as no extra space is used.

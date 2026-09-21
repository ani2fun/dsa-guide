## Brute

### Intuition

The most naive thing that comes to mind is if at all any element on right is greater than the current element, then the current element can never be a leader.

### Approach

1. Iterate through each element of the array with the variable let's say i and take a boolean variable leader set at true initially which will tell if nums[i] is a leader or not.
2. For each i, iterate through the elements to the right (from i+1 to the end of the array) with the variable j & check if nums[j] is greater than nums[i], if so, reinitialize the variable leader as false and break.
3. After exiting from the inner loop, check if leader equals true, if so add nums[i] to ans vector. Finally return the answer vector.

### Solution

```python solution time=O(N²) space=O(N)
from typing import List

class Solution:
    # Function to find leaders in an array.
    def leaders(self, nums: List[int]) -> List[int]:
        ans = []

        # Iterate through each element in nums
        for i in range(len(nums)):
            leader = True

            '''Check whether nums[i] is greater
            than all elements to its right'''
            for j in range(i + 1, len(nums)):
                if nums[j] >= nums[i]:
                    '''If any element to the right is greater
                    or equal, nums[i] is not a leader'''
                    leader = False
                    break

            # If nums[i] is a leader, add it to the ans list
            if leader:
                ans.append(nums[i])

        # Return the leaders
        return ans


# Reads the test case's nums, e.g. [1, 2, 5, 3, 1, 2]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().leaders(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N²) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find leaders in an array.
        List<Integer> leaders(int[] nums) {
            List<Integer> ans = new ArrayList<>();

            // Iterate through each element in nums
            for (int i = 0; i < nums.length; i++) {
                boolean leader = true;

                /* Check whether nums[i] is greater
                than all elements to its right */
                for (int j = i + 1; j < nums.length; j++) {
                    if (nums[j] >= nums[i]) {
                        /* If any element to the right is greater
                        or equal, nums[i] is not a leader */
                        leader = false;
                        break;
                    }
                }

                // If nums[i] is a leader, add it to the ans list
                if (leader) {
                    ans.add(nums[i]);
                }
            }

            // Return the leaders
            return ans;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [1, 2, 5, 3, 1, 2]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().leaders(nums));
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

- **Time Complexity:** O(N²), where N is the length of the array, as two nested loops are used to traverse the array.
- **Space Complexity:** O(N) to store the elements in the answer array and return it. Note: the auxiliary space (excluding the output array) is strictly O(1) since no additional intermediate data structures are utilized.

## Optimal

### Intuition

Think of a parade where each person in a line holds a flag with a number on it, representing their importance. You start observing the parade from the last person, moving towards the front. Initially, the last person is the most important (since there's no one else behind them).

As you move forward, compare each person's flag number to the highest flag number seen so far. If someone's flag number is higher than the highest that is seen, they stand out as a leader because they have a higher number than anyone behind them.

### Approach

1. Set a variable max to the last element of the array (nums[sizeOfArray - 1]), as the last element is always a leader.
2. Create an empty list ans to store the leader elements and add the last element of the array to this list initially, as it is always a leader.
3. Start from the second last element (index = sizeOfArray - 2) and move towards the first element (index = 0).
4. For each element, compare it with the max variable. If the current element is greater than max, add this element to the ans list and update max to the current element.
5. Reverse the ans list. It now contains all the leader elements in the order they appear in the array.

### Solution

```python solution time=O(N) space=O(N)
from typing import List

class Solution:
    # Function to find the leaders in an array.
    def leaders(self, nums: List[int]) -> List[int]:
        ans = []

        if not nums:
            return ans

        # Last element of the list is always a leader
        max_val = nums[-1]
        ans.append(nums[-1])

        # Check elements from right to left
        for i in range(len(nums) - 2, -1, -1):
            if nums[i] > max_val:
                ans.append(nums[i])
                max_val = nums[i]

        '''Reverse the list to match
        the required output order'''
        ans.reverse()

        # Return the leaders
        return ans


# Reads the test case's nums, e.g. [1, 2, 5, 3, 1, 2]
inner = input().strip()[1:-1].strip()
nums = [int(t) for t in inner.split(",")] if inner else []
result = Solution().leaders(nums)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(N) space=O(N)
import java.util.*;

public class Main {
    static class Solution {
        // Function to find the leaders in an array.
        List<Integer> leaders(int[] nums) {
            List<Integer> ans = new ArrayList<>();

            if (nums.length == 0) {
                return ans;
            }

            // Last element of the array is always a leader
            int max = nums[nums.length - 1];
            ans.add(nums[nums.length - 1]);

            // Check elements from right to left
            for (int i = nums.length - 2; i >= 0; i--) {
                if (nums[i] > max) {
                    ans.add(nums[i]);
                    max = nums[i];
                }
            }

            /* Reverse the list to match
            the required output order */
            Collections.reverse(ans);

            // Return the leaders
            return ans;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums, e.g. [1, 2, 5, 3, 1, 2]
        int[] nums = parseIntArray(new Scanner(System.in).nextLine());
        System.out.println(new Solution().leaders(nums));
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

- **Time Complexity:** O(N), where N is the length of the array. A single traversal of the array is required.
- **Space Complexity:** O(N) to store the elements in the answer array and return it. Note: the auxiliary space (excluding the output array) is strictly O(1) since no additional intermediate data structures are utilized.

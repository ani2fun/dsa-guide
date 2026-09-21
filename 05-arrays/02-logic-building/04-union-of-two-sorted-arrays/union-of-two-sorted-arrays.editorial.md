## Brute

*Ordered set*

### Intuition

The union of two arrays will be all the unique elements of both of the arrays combined. So, using a set data structure will help & can find the distinct elements because the set does not hold any duplicates. As it is mandatory to preserve the order of the elements, use an ordered set.

### Approach

1. Declare a set s to store all the unique elements and a vector or list union to store the final answer.
2. Iterate through nums1 and nums2 to store the elements in the set.
3. Now, iterate in the set and copy all the elements of the set to the answer vector and return it.

### Solution

```python solution time=O((M+N) log(M+N)) space=O(M+N)
from typing import List

class Solution:
    def unionArray(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # Using set for storing unique elements
        s = set()
        Union = []

        # Insert all elements of nums1 into the set
        for num in nums1:
            s.add(num)

        # Insert all elements of nums2 into the set
        for num in nums2:
            s.add(num)

        # Convert the set to list to get the union
        for num in sorted(s):  # Sorting for union of sorted arrays
            Union.append(num)

        return Union


# Reads the test case's nums1 and nums2, one per line
inner1 = input().strip()[1:-1].strip()
nums1 = [int(t) for t in inner1.split(",")] if inner1 else []
inner2 = input().strip()[1:-1].strip()
nums2 = [int(t) for t in inner2.split(",")] if inner2 else []
result = Solution().unionArray(nums1, nums2)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O((M+N) log(M+N)) space=O(M+N)
import java.util.*;

public class Main {
    static class Solution {
        int[] unionArray(int[] nums1, int[] nums2) {
            Set<Integer> set = new TreeSet<>();

            // Insert all elements of nums1 into the set
            for (int num : nums1) {
                set.add(num);
            }

            // Insert all elements of nums2 into the set
            for (int num : nums2) {
                set.add(num);
            }

            // Convert the set to an integer array to get the union
            int[] union = new int[set.size()];
            int index = 0;
            for (int num : set) {
                union[index++] = num;
            }

            return union;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums1 and nums2, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums1 = parseIntArray(sc.nextLine());
        int[] nums2 = parseIntArray(sc.nextLine());
        System.out.println(Arrays.toString(new Solution().unionArray(nums1, nums2)));
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

- **Time Complexity:** O((M+N) log(M+N)) — at max the set can store M+N elements (when there are no common elements and elements in nums1, nums2 are distinct). So inserting the (M+N)th element takes log(M+N) time. Upon approximation across inserting all elements in the worst case, it would take O((M+N)log(M+N)) time.
- **Space Complexity:** O(M+N), considering space of the union array.

## Optimal

*Two-pointer merge*

### Intuition

The optimal approach uses the two-pointers to solve the problem. Use two pointers, one for each array, and traverse both arrays simultaneously. Keep adding the smaller element between the two arrays to the result vector if it hasn't been added already.

> **What if both elements are equal?**
> If both elements are equal, add any one of them, ensuring that all unique elements are added in sorted order.

### Approach

1. Initialize two variable i to iterate nums1 and j to iterate nums2 as 0.
2. Create an empty vector for storing the union of nums1 and nums2.
3. If current element of nums1 is equal to current element of nums2, this means its a common element, so insert only one element in the union & increment it by 1.
4. If current element of nums1 is less than current element of nums2, insert current element of nums1 in union. Also check if last element in union vector is not equal to nums1[i], then insert in union else don't insert. After checking increment i.
5. If current element of nums1 is greater than current element of nums2, insert current element of nums2 in union. Similar to last point, check if the last element in the union vector is not equal to nums2[j], then insert in the union, else don't insert. After checking increment j.
6. After traversing if any elements are left in nums1 or nums2 check for condition and insert in the union.

### Solution

```python solution time=O(M+N) space=O(M+N)
from typing import List

class Solution:
    def unionArray(self, nums1: List[int], nums2: List[int]) -> List[int]:
        union = []  # union set

        i, j = 0, 0
        n, m = len(nums1), len(nums2)

        while i < n and j < m:
            # case 1 and 2
            if nums1[i] <= nums2[j]:
                if not union or union[-1] != nums1[i]:
                    union.append(nums1[i])
                i += 1
            # case 3
            else:
                if not union or union[-1] != nums2[j]:
                    union.append(nums2[j])
                j += 1

        # if any elements left in nums1
        while i < n:
            if not union or union[-1] != nums1[i]:
                union.append(nums1[i])
            i += 1

        # if any elements left in nums2
        while j < m:
            if not union or union[-1] != nums2[j]:
                union.append(nums2[j])
            j += 1

        return union


# Reads the test case's nums1 and nums2, one per line
inner1 = input().strip()[1:-1].strip()
nums1 = [int(t) for t in inner1.split(",")] if inner1 else []
inner2 = input().strip()[1:-1].strip()
nums2 = [int(t) for t in inner2.split(",")] if inner2 else []
result = Solution().unionArray(nums1, nums2)
print("[" + ", ".join(str(x) for x in result) + "]")
```

```java solution time=O(M+N) space=O(M+N)
import java.util.*;

public class Main {
    static class Solution {
        int[] unionArray(int[] nums1, int[] nums2) {
            List<Integer> UnionList = new ArrayList<>();
            int i = 0, j = 0;
            int n = nums1.length;
            int m = nums2.length;

            while (i < n && j < m) {
                // Case 1 and 2
                if (nums1[i] <= nums2[j]) {
                    if (UnionList.isEmpty() || UnionList.get(UnionList.size() - 1) != nums1[i]) {
                        UnionList.add(nums1[i]);
                    }
                    i++;
                }
                // Case 3
                else {
                    if (UnionList.isEmpty() || UnionList.get(UnionList.size() - 1) != nums2[j]) {
                        UnionList.add(nums2[j]);
                    }
                    j++;
                }
            }

            // Add remaining elements of nums1, if any
            while (i < n) {
                if (UnionList.isEmpty() || UnionList.get(UnionList.size() - 1) != nums1[i]) {
                    UnionList.add(nums1[i]);
                }
                i++;
            }

            // Add remaining elements of nums2, if any
            while (j < m) {
                if (UnionList.isEmpty() || UnionList.get(UnionList.size() - 1) != nums2[j]) {
                    UnionList.add(nums2[j]);
                }
                j++;
            }

            // Convert List<Integer> to int[]
            int[] Union = new int[UnionList.size()];
            for (int k = 0; k < UnionList.size(); k++) {
                Union[k] = UnionList.get(k);
            }

            return Union;
        }
    }

    public static void main(String[] args) {
        // Reads the test case's nums1 and nums2, one per line
        Scanner sc = new Scanner(System.in);
        int[] nums1 = parseIntArray(sc.nextLine());
        int[] nums2 = parseIntArray(sc.nextLine());
        System.out.println(Arrays.toString(new Solution().unionArray(nums1, nums2)));
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

- **Time Complexity:** O(M+N) — because both the arrays must be traversed once.
- **Space Complexity:** O(M+N), considering the space for returning the output, which in the worst case, can contain all the elements from both arrays.

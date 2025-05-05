# LeetCode - 704. Binary Search
[https://leetcode.com/problems/binary-search/]

## Solution 1

``` java
class Solution {
    public int search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2; // To prevent potential overflow
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return -1; // Target not found
    }
}
``` 

### Resultado
Runtime: 0ms Beats 100.00%  
Memory: 45.57MB Beats 89.34%

## Copilot

### Prompt
Give me the top 3 optimal solution in Java for LeetCode test above. https://leetcode.com/problems/binary-search/description/

### Answer

1. Iterative Binary Search
This approach uses a while loop to repeatedly divide the search space in half until the target is found or the search space is exhausted.

``` java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            if (nums[mid] < target) left = mid + 1;
            else right = mid - 1;
        }
        return -1;
    }
}
``` 
Time Complexity: O(log n) Space Complexity: O(1)

2. Recursive Binary Search
This approach uses recursion to divide the search space in half.

``` java
class Solution {
    public int search(int[] nums, int target) {
        return binarySearch(nums, target, 0, nums.length - 1);
    }

    private int binarySearch(int[] nums, int target, int left, int right) {
        if (left > right) return -1;
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        return nums[mid] < target 
            ? binarySearch(nums, target, mid + 1, right) 
            : binarySearch(nums, target, left, mid - 1);
    }
}
``` 
Time Complexity: O(log n) Space Complexity: O(log n) (due to recursive calls)

3. Using Arrays.binarySearch()
Java provides a built-in method for binary search in the Arrays class.

``` java
import java.util.Arrays;

class Solution {
    public int search(int[] nums, int target) {
        int index = Arrays.binarySearch(nums, target);
        return index >= 0 ? index : -1;
    }
}
``` 
Time Complexity: O(log n) Space Complexity: O(1)
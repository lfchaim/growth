# LeetCode - Exponential Search

## Solution 1
Avaliar o target, verificando se é menor que o bound. Se for menor, temos o índice mínimo (< target) e máximo (> target).  
Então fazer a busca Binary Search

``` java
class Solution {
    public int search(int[] nums, int target) {
        int bound = 1;
        while (bound < nums.length && nums[bound] < target) {
            bound *= 2;
        }
        return binarySearch(nums, target, bound / 2, Math.min(bound, nums.length - 1));
    }

    private int binarySearch(int[] nums, int target, int low, int high) {
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return -1;
    }
}
``` 

### Resultado
Runtime: 0ms Beats 100.00%  
Memory: 45.57MB Beats 89.34%


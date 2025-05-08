
# LeetCode

## Code Generator

### Prompt
I want to generate a method that resolv https://leetcode.com/problems/is-subsequence/description/


### AI Code Generator 
[https://zzzcode.ai/java/code-generator?id=2924d29e-4ff4-4526-9ba3-49e4d8188fb7]


## All Algorithms

### Array / String

<details>
<summary>80. Remove Duplicates from Sorted Array II (100.00% / 87.34%)</summary>  


``` java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length <= 2)
            return nums.length;

        int index = 2;
        for (int i = 2; i < nums.length; i++) {
            if (nums[i] != nums[index - 2]) {
                nums[index++] = nums[i];
            }
        }
        return index;
    }
}
```
</details>

<details>
<summary>189. Rotate Array (100.00% / 51.59%)</summary>  


``` java
class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```
</details>

### Two Pointers

<details>
<summary>125. Valid Palindrome (42.48 / 35.18)</summary>  


``` java
class Solution {
    public boolean isPalindrome(String s) {
        if (s == null)
            return false;
        s = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```
</details>

<details>
<summary>15. 3Sum (85.67 / 83.88)</summary>  


``` java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);

        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1])
                continue;
            int left = i + 1, right = nums.length - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum < 0) {
                    left++;
                } else if (sum > 0) {
                    right--;
                } else {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while (left < right && nums[left] == nums[left + 1])
                        left++;
                    while (left < right && nums[right] == nums[right - 1])
                        right--;
                    left++;
                    right--;
                }
            }
        }
        return result;
    }
}
```
</details>

<details>
<summary>167. Two Sum II - Input Array Is Sorted (93.04 / 6.26)</summary>  


``` java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {
            int sum = numbers[left] + numbers[right];
            if (sum == target) {
                return new int[] { left + 1, right + 1 };
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return new int[] {}; // Return an empty array if no solution is found
    }
}
```
</details>

<details>
<summary>125. Valid Palindrome (32.94 / 47.20)</summary>  


``` java
class Solution {
    public boolean isPalindrome(String s) {
        if (s == null)
            return false;
        s = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```
</details>

<details>
<summary>392. Is Subsequence (66.73 / 85.87)</summary>  


``` java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int sIndex = 0, tIndex = 0;
        while (sIndex < s.length() && tIndex < t.length()) {
            if (s.charAt(sIndex) == t.charAt(tIndex)) {
                sIndex++;
            }
            tIndex++;
        }
        return sIndex == s.length();
    }
}
```
</details>

<details>
<summary>11. Container With Most Water (75.13 / 64.30)</summary>  


``` java
class Solution {
    public int maxArea(int[] height) {
        int maxArea = 0;
        int left = 0;
        int right = height.length - 1;
        while (left < right) {
            int width = right - left;
            int currentHeight = Math.min(height[left], height[right]);
            maxArea = Math.max(maxArea, width * currentHeight);
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        return maxArea;
    }
}
```
</details>


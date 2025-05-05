# Copilot

## 3090. Maximum Length Substring With Two Occurrences
https://leetcode.com/problems/maximum-length-substring-with-two-occurrences/description/

1. Sliding Window Approach
This method efficiently finds the longest substring while ensuring each character appears at most twice.

``` java
import java.util.HashMap;

class Solution {
    public int maximumLengthSubstring(String s) {
        int maxLength = 0;
        HashMap<Character, Integer> count = new HashMap<>();
        int left = 0;

        for (int right = 0; right < s.length(); right++) {
            count.put(s.charAt(right), count.getOrDefault(s.charAt(right), 0) + 1);

            while (count.get(s.charAt(right)) > 2) {
                count.put(s.charAt(left), count.get(s.charAt(left)) - 1);
                left++;
            }

            maxLength = Math.max(maxLength, right - left + 1);
        }

        return maxLength;
    }
}
``` 
Time Complexity: O(n) Space Complexity: O(1) (since we store at most 26 characters)

2. Brute Force Approach
This method checks all possible substrings, but is less efficient.

``` java
class Solution {
    public int maximumLengthSubstring(String s) {
        int maxLength = 0;

        for (int i = 0; i < s.length(); i++) {
            int[] count = new int[26];
            for (int j = i; j < s.length(); j++) {
                count[s.charAt(j) - 'a']++;
                if (count[s.charAt(j) - 'a'] > 2) break;
                maxLength = Math.max(maxLength, j - i + 1);
            }
        }

        return maxLength;
    }
}
``` 
Time Complexity: O(n²) Space Complexity: O(1)

3. Optimized Sliding Window with Frequency Array
This approach is similar to the first but uses an array instead of a HashMap for better performance.

``` java
class Solution {
    public int maximumLengthSubstring(String s) {
        int maxLength = 0;
        int[] count = new int[26];
        int left = 0;

        for (int right = 0; right < s.length(); right++) {
            count[s.charAt(right) - 'a']++;

            while (count[s.charAt(right) - 'a'] > 2) {
                count[s.charAt(left) - 'a']--;
                left++;
            }

            maxLength = Math.max(maxLength, right - left + 1);
        }

        return maxLength;
    }
}
``` 
Time Complexity: O(n) Space Complexity: O(1)
# LeetCode - 387. First Unique Character in a String

## Copilot

1. Using HashMap
This approach counts the frequency of each character and then finds the first unique one.

``` java
import java.util.HashMap;

class Solution {
    public int firstUniqChar(String s) {
        HashMap<Character, Integer> count = new HashMap<>();

        for (char c : s.toCharArray()) {
            count.put(c, count.getOrDefault(c, 0) + 1);
        }

        for (int i = 0; i < s.length(); i++) {
            if (count.get(s.charAt(i)) == 1) return i;
        }

        return -1;
    }
}
``` 
Time Complexity: O(n) Space Complexity: O(1) (since we store at most 26 characters)

2. Using Frequency Array  
## ***Best***  
This method optimizes space by using an array instead of a HashMap.

``` java
class Solution {
    public int firstUniqChar(String s) {
        int[] count = new int[26];

        for (char c : s.toCharArray()) {
            count[c - 'a']++;
        }

        for (int i = 0; i < s.length(); i++) {
            if (count[s.charAt(i) - 'a'] == 1) return i;
        }

        return -1;
    }
}
``` 
Time Complexity: O(n) Space Complexity: O(1)

3. Using indexOf() and lastIndexOf()
This approach checks if the first and last occurrence of a character are the same.

``` java
class Solution {
    public int firstUniqChar(String s) {
        int minIndex = Integer.MAX_VALUE;

        for (char c : s.toCharArray()) {
            int first = s.indexOf(c);
            int last = s.lastIndexOf(c);
            if (first == last) {
                minIndex = Math.min(minIndex, first);
            }
        }

        return minIndex == Integer.MAX_VALUE ? -1 : minIndex;
    }
}
``` 
Time Complexity: O(n²) (due to indexOf() calls) Space Complexity: O(1)
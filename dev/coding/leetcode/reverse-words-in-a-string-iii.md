# LeetCode - 557. Reverse Words in a String III
[https://leetcode.com/problems/reverse-words-in-a-string-iii/]

## Solution 1

``` java
class Solution {
    public String reverseWords(String s) {
        String[] words = s.split(" ");
        StringBuilder result = new StringBuilder();
        for (String word : words) {
            StringBuilder reversedWord = new StringBuilder(word).reverse();
            result.append(reversedWord).append(" ");
        }
        return result.toString().trim();
    }
}
``` 

### Resultado
Runtime: 4ms Beats 86.81%  
Memory: 45.52MB Beats 32.41%

## Solution 2

``` java
class Solution {
    public String reverseWords(String s) {
        return Arrays.stream(s.split(" "))
            .map(str -> new StringBuilder(str).reverse().toString())
            .reduce((oldS, newS) -> (oldS + " " + newS))
            .orElse("");
    }
}
``` 

### Resultado
Runtime: 15ms Beats 19.26%  
Memory: 45.56MB Beats 32.41%

## Solution 3

``` java
class Solution {
    public String reverseWords(String s) {
        StringBuilder sb = new StringBuilder(s);
        int i = 0;
        int j = 0;
        while (i < sb.length()) {
            while (i < j || i < sb.length() && sb.charAt(i) == ' ')
                ++i;
            while (j < i || j < sb.length() && sb.charAt(j) != ' ')
                ++j;
            reverse(sb, i, j - 1);
        }
        return sb.toString();
    }
    private void reverse(StringBuilder sb, int l, int r) {
        while (l < r) {
            final char temp = sb.charAt(l);
            sb.setCharAt(l++, sb.charAt(r));
            sb.setCharAt(r--, temp);
        }
    }
}
``` 

### Resultado
Runtime: 7ms Beats 39.37%  
Memory: 45.20MB Beats 74.07%

## Solution 4

``` java
class Solution {
    public String reverseWords(String s) {
        String[] words = s.split(" ");
        StringBuilder result = new StringBuilder();
        for (String word : words) {
            result.append(new StringBuilder(word).reverse().toString()).append(" ");
        }
        return result.toString().trim();
    }
}
``` 

### Resultado
Runtime: 4ms Beats 86.81%  
Memory: 45.09MB Beats 94.02%

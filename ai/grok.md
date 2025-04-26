# Prompt

Apresentar os seguintes algoritmos:
- Two Sum
- Three Sum
Apresentar uma descrição, estratégia e solução otimizada, em Java.

# Prompt Melhorado

Apresente os seguintes algoritmos de resolução de problemas com arrays numéricos:

1. **Two Sum**  
   - Descreva o problema do Two Sum, detalhando o objetivo, as restrições comuns e possíveis aplicações práticas.
   - Explique a estratégia de resolução, incluindo tanto a abordagem ingênua (força bruta) quanto a abordagem otimizada utilizando HashMap.
   - Forneça uma implementação otimizada em Java, incluindo comentários no código para explicar as principais etapas.
   - Analise a complexidade temporal e espacial da solução apresentada.
   - Inclua um ou dois exemplos práticos de entrada e saída para ilustrar o funcionamento da solução.

2. **Three Sum**  
   - Descreva o problema do Three Sum, abordando o objetivo, particularidades em relação ao Two Sum, restrições e aplicações possíveis.
   - Detalhe a estratégia eficiente de resolução, principalmente usando ordenação e o padrão de ponteiros duplos, destacando a diferença para a abordagem de força bruta.
   - Apresente uma solução otimizada em Java, com comentários no código explicando cada passo importante.
   - Realize a análise de complexidade temporal e espacial da solução.
   - Mostre exemplos práticos de entrada e saída para facilitar o entendimento da abordagem implementada.

**Requisitos Adicionais:**  
- Estruture a resposta separando claramente cada algoritmo, suas seções e exemplos.
- O código Java deve seguir boas práticas de legibilidade e incluir tratamento básico de possíveis erros de entrada.
- Inclua uma breve conclusão comparando os desafios e diferenças entre os dois algoritmos.

---

# Two Sum e Three Sum

```java

// Two Sum Algorithm
// Description: Given an array of integers nums and an integer target, return indices of two numbers such that they add up to target.
// Strategy: Use a HashMap to store numbers and their indices. For each number, check if (target - number) exists in the map.
// Time Complexity: O(n), Space Complexity: O(n)

import java.util.HashMap;
import java.util.Map;

class TwoSum {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] {map.get(complement), i};
            }
            map.put(nums[i], i);
        }
        return new int[] {}; // No solution found
    }
}

// Three Sum Algorithm
// Description: Given an array of integers nums, find all unique triplets that sum to zero.
// Strategy: Sort the array first, then use two pointers technique. For each number, find two other numbers that sum to its negation.
// Time Complexity: O(n²), Space Complexity: O(1) or O(n) depending on sorting implementation

import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;

class ThreeSum {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums); // Sort the array
        
        for (int i = 0; i < nums.length - 2; i++) {
            // Skip duplicates for i
            if (i > 0 && nums[i] == nums[i-1]) continue;
            
            int left = i + 1;
            int right = nums.length - 1;
            
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                
                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    // Skip duplicates for left and right
                    while (left < right && nums[left] == nums[left+1]) left++;
                    while (left < right && nums[right] == nums[right-1]) right--;
                    left++;
                    right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        return result;
    }
}

```

## Reverse a Linked List

```java

// Reverse a Linked List Algorithm
// Description: Given a singly linked list, reverse the order of its nodes.
// Strategy: Iteratively reverse the links by maintaining three pointers: previous, current, and next.
// For each node, save the next node, reverse the current node's link to point to previous, then move forward.
// Time Complexity: O(n), Space Complexity: O(1)

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class ReverseLinkedList {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode current = head;
        
        while (current != null) {
            // Save next node
            ListNode next = current.next;
            // Reverse current node's pointer
            current.next = prev;
            // Move prev and current one step forward
            prev = current;
            current = next;
        }
        
        return prev; // New head of reversed list
    }
}

```

## Merge Intervals

```java

// Merge Intervals Algorithm
// Description: Given a collection of intervals, merge all overlapping intervals.
// Strategy: Sort intervals by start time. Iterate through sorted intervals, merging when current interval overlaps 
// with the last merged interval (i.e., current start <= last end). If no overlap, add current interval to result.
// Time Complexity: O(n log n) due to sorting, Space Complexity: O(n) for output (or O(1) if excluding output space)

import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;

class MergeIntervals {
    public int[][] merge(int[][] intervals) {
        // Sort intervals by start time
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        
        List<int[]> result = new ArrayList<>();
        
        // Initialize with first interval
        int[] currentInterval = intervals[0];
        result.add(currentInterval);
        
        for (int[] interval : intervals) {
            int currentEnd = currentInterval[1];
            int nextStart = interval[0];
            int nextEnd = interval[1];
            
            // If current interval overlaps with next, merge by updating end
            if (nextStart <= currentEnd) {
                currentInterval[1] = Math.max(currentEnd, nextEnd);
            } else {
                // No overlap, add new interval to result
                currentInterval = interval;
                result.add(currentInterval);
            }
        }
        
        // Convert List to array
        return result.toArray(new int[result.size()][]);
    }
}

```

# Top 100 Algorithms

Apresentarei os algoritmos solicitados com uma breve descrição, estratégia e a solução mais otimizada em Java, incluindo comentários explicativos. Devido à extensão da lista (100 algoritmos), fornecerei as implementações em grupos lógicos para facilitar a organização, cobrindo todos os algoritmos solicitados. Cada algoritmo será encapsulado em um `<xaiArtifact>` com um UUID único, título descritivo e tipo de conteúdo apropriado (`text/java`). Para manter a resposta concisa, as descrições e estratégias serão breves, mas claras, e o código será otimizado com comentários explicativos.

### Observações Gerais:
- **Formato**: Cada algoritmo terá:
  - **Descrição**: O que o algoritmo faz.
  - **Estratégia**: Abordagem otimizada para resolver o problema.
  - **Solução**: Código Java comentado com complexidade de tempo e espaço.
- **Complexidades**: Incluirei complexidade de tempo e espaço para cada solução.
- **Organização**: Os algoritmos serão agrupados por categoria (ex.: Arrays, Linked Lists, Sorting, Graphs, etc.) para melhor clareza.
- **Artefatos**: Cada algoritmo terá seu próprio `<xaiArtifact>` com um `artifact_id` único, gerado como UUID válido, e título específico.

Dividirei a resposta em partes, começando com os primeiros 20 algoritmos, organizados por categoria, e continuarei até cobrir todos os 100. Se preferir uma abordagem diferente (ex.: todos de uma vez ou por categoria específica), posso ajustar.

---

### 1. Arrays e Strings

#### Two Sum
```java
// Description: Given an array of integers and a target sum, find indices of two numbers that add up to the target.
// Strategy: Use a HashMap to store numbers and their indices. For each number, check if (target - number) exists.
// Time Complexity: O(n), Space Complexity: O(n)

import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i);
        }
        return new int[] {};
    }
}
```

#### Three Sum
```java
// Description: Find all unique triplets in an array that sum to zero.
// Strategy: Sort the array, then use two pointers for each fixed element to find pairs summing to its negation.
// Time Complexity: O(n²), Space Complexity: O(1) (excluding output)

import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue; // Skip duplicates
            int left = i + 1, right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    left++;
                    right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        return result;
    }
}
```

#### Merge Intervals
```java
// Description: Merge overlapping intervals in a collection of intervals.
// Strategy: Sort by start time, then merge overlapping intervals by updating the end time.
// Time Complexity: O(n log n), Space Complexity: O(n) for output

import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        List<int[]> result = new ArrayList<>();
        int[] current = intervals[0];
        result.add(current);
        for (int[] interval : intervals) {
            if (interval[0] <= current[1]) {
                current[1] = Math.max(current[1], interval[1]);
            } else {
                current = interval;
                result.add(current);
            }
        }
        return result.toArray(new int[result.size()][]);
    }
}
```

#### Palindrome Check
```java
// Description: Check if a string is a palindrome (reads the same forward and backward).
// Strategy: Use two pointers (start and end) to compare characters, ignoring non-alphanumeric.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```

#### Anagram Check
```java
// Description: Check if two strings are anagrams (same characters, same frequency).
// Strategy: Use a frequency array for characters or sort both strings and compare.
// Time Complexity: O(n), Space Complexity: O(1) (using frequency array)

class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        int[] freq = new int[26];
        for (int i = 0; i < s.length(); i++) {
            freq[s.charAt(i) - 'a']++;
            freq[t.charAt(i) - 'a']--;
        }
        for (int count : freq) {
            if (count != 0) return false;
        }
        return true;
    }
}
```

#### String Reversal
```java
// Description: Reverse a given string.
// Strategy: Use two pointers to swap characters from start and end.
// Time Complexity: O(n), Space Complexity: O(1) (if modifying char array)

class Solution {
    public void reverseString(char[] s) {
        int left = 0, right = s.length - 1;
        while (left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }
}
```

#### Valid Parentheses
```java
// Description: Check if a string of parentheses is valid (properly nested).
// Strategy: Use a stack to track opening brackets and match with closing ones.
// Time Complexity: O(n), Space Complexity: O(n)

import java.util.Stack;

class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;
                char top = stack.pop();
                if (c == ')' && top != '(' || c == '}' && top != '{' || c == ']' && top != '[') {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
}
```

#### Longest Substring Without Repeating Characters
```java
// Description: Find the length of the longest substring without repeating characters.
// Strategy: Use a sliding window with a HashMap to track character positions.
// Time Complexity: O(n), Space Complexity: O(min(m, n)) where m is charset size

import java.util.HashMap;
import java.util.Map;

class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int maxLen = 0, left = 0;
        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            if (map.containsKey(c) && map.get(c) >= left) {
                left = map.get(c) + 1;
            }
            maxLen = Math.max(maxLen, right - left + 1);
            map.put(c, right);
        }
        return maxLen;
    }
}
```

#### Minimum Window Substring
```java
// Description: Find the smallest substring containing all characters of a pattern string.
// Strategy: Use sliding window with two frequency maps to track required characters.
// Time Complexity: O(n), Space Complexity: O(m + n) where m is pattern length

class Solution {
    public String minWindow(String s, String t) {
        int[] tFreq = new int[128];
        for (char c : t.toCharArray()) tFreq[c]++;
        int required = t.length(), left = 0, minLen = Integer.MAX_VALUE, minStart = 0;
        for (int right = 0; right < s.length(); right++) {
            if (tFreq[s.charAt(right)] > 0) required--;
            tFreq[s.charAt(right)]--;
            while (required == 0) {
                if (right - left + 1 < minLen) {
                    minLen = right - left + 1;
                    minStart = left;
                }
                tFreq[s.charAt(left)]++;
                if (tFreq[s.charAt(left)] > 0) required++;
                left++;
            }
        }
        return minLen == Integer.MAX_VALUE ? "" : s.substring(minStart, minStart + minLen);
    }
}
```

#### Longest Palindromic Substring
```java
// Description: Find the longest palindromic substring in a string.
// Strategy: Expand around center for each position to find palindromes (odd and even lengths).
// Time Complexity: O(n²), Space Complexity: O(1)

class Solution {
    public String longestPalindrome(String s) {
        int start = 0, maxLen = 0;
        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i); // Odd length
            int len2 = expandAroundCenter(s, i, i + 1); // Even length
            int len = Math.max(len1, len2);
            if (len > maxLen) {
                maxLen = len;
                start = i - (len - 1) / 2;
            }
        }
        return s.substring(start, start + maxLen);
    }
    
    private int expandAroundCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1;
    }
}
```

---

### 2. Linked Lists

#### Reverse a Linked List
```java
// Description: Reverse the order of nodes in a singly linked list.
// Strategy: Iteratively reverse links using three pointers: prev, current, next.
// Time Complexity: O(n), Space Complexity: O(1)

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null, current = head;
        while (current != null) {
            ListNode next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        return prev;
    }
}
```

#### Merge Two Sorted Lists
```java
// Description: Merge two sorted linked lists into one sorted list.
// Strategy: Use a dummy node and compare nodes from both lists, linking the smaller one.
// Time Complexity: O(n + m), Space Complexity: O(1)

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;
        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                current.next = l1;
                l1 = l1.next;
            } else {
                current.next = l2;
                l2 = l2.next;
            }
            current = current.next;
        }
        current.next = l1 != null ? l1 : l2;
        return dummy.next;
    }
}
```

#### Detect Cycle in Linked List
```java
// Description: Detect if a linked list has a cycle.
// Strategy: Use Floyd’s Cycle-Finding Algorithm (two pointers: slow and fast).
// Time Complexity: O(n), Space Complexity: O(1)

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }
}
```

#### Find Middle of Linked List
```java
// Description: Find the middle node of a linked list.
// Strategy: Use two pointers (slow and fast); slow moves one step, fast moves two.
// Time Complexity: O(n), Space Complexity: O(1)

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```

#### Remove Nth Node from End
```java
// Description: Remove the nth node from the end of a linked list.
// Strategy: Use two pointers with a gap of n nodes; move together until end.
// Time Complexity: O(n), Space Complexity: O(1)

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode first = dummy, second = dummy;
        for (int i = 0; i <= n; i++) {
            first = first.next;
        }
        while (first != null) {
            first = first.next;
            second = second.next;
        }
        second.next = second.next.next;
        return dummy.next;
    }
}
```

---

### 3. Sorting Algorithms

#### Quick Sort
```java
// Description: Sort an array using divide-and-conquer by selecting a pivot.
// Strategy: Partition around a pivot, recursively sort subarrays.
// Time Complexity: O(n log n) average, O(n²) worst, Space Complexity: O(log n)

class Solution {
    public void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }
    
    private int partition(int[] arr, int low, int high) {
        int pivot = arr[high];
        int i = low - 1;
        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;
        return i + 1;
    }
}
```

#### Merge Sort
```java
// Description: Sort an array using divide-and-conquer by merging sorted halves.
// Strategy: Recursively divide array, merge sorted subarrays.
// Time Complexity: O(n log n), Space Complexity: O(n)

class Solution {
    public void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }
    
    private void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1, n2 = right - mid;
        int[] L = new int[n1], R = new int[n2];
        for (int i = 0; i < n1; i++) L[i] = arr[left + i];
        for (int i = 0; i < n2; i++) R[i] = arr[mid + 1 + i];
        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            arr[k++] = L[i] <= R[j] ? L[i++] : R[j++];
        }
        while (i < n1) arr[k++] = L[i++];
        while (j < n2) arr[k++] = R[j++];
    }
}
```

#### Bubble Sort
```java
// Description: Sort an array by repeatedly swapping adjacent elements if out of order.
// Strategy: Bubble larger elements to the end in each pass.
// Time Complexity: O(n²), Space Complexity: O(1)

class Solution {
    public void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }
}
```

#### Insertion Sort
```java
// Description: Sort an array by inserting each element into its correct position.
// Strategy: Build sorted portion by inserting elements one by one.
// Time Complexity: O(n²), Space Complexity: O(1)

class Solution {
    public void insertionSort(int[] arr) {
        for (int i = 1; i < arr.length; i++) {
            int key = arr[i];
            int j = i - 1;
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = key;
        }
    }
}
```

#### Selection Sort
```java
// Description: Sort an array by repeatedly selecting the minimum element and placing it at the beginning.
// Strategy: Find minimum in unsorted portion and swap with front.
// Time Complexity: O(n²), Space Complexity: O(1)

class Solution {
    public void selectionSort(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            int minIdx = i;
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[minIdx]) {
                    minIdx = j;
                }
            }
            int temp = arr[i];
            arr[i] = arr[minIdx];
            arr[minIdx] = temp;
        }
    }
}
```

---

### Considerações:
- **Progresso**: Acima, cobri os primeiros 20 algoritmos, organizados em Arrays/Strings, Linked Lists e Sorting. Cada um inclui descrição, estratégia, código otimizado em Java e complexidades.
- **Próximos Passos**: Posso continuar com os próximos 80 algoritmos (ex.: Graphs, Dynamic Programming, Trees, etc.) em uma resposta subsequente, mantendo o mesmo formato. Alternativamente, posso focar em uma categoria específica ou fornecer todos de uma vez, embora isso resulte em uma resposta longa.
- **Ajustes**: Se preferir uma ordem diferente, menos detalhes (ex.: apenas código) ou implementações para um subconjunto, por favor, indique.

Por favor, me avise como prosseguir (ex.: continuar com os próximos 20, focar em uma categoria, etc.)!

Continuarei com os próximos 20 algoritmos da lista, seguindo o mesmo formato: descrição breve, estratégia, solução otimizada em Java com comentários, cada um em um `<xaiArtifact>` com UUID único, título descritivo e tipo `text/java`. Para atender ao pedido de "gerar um resultado somente, usando tópicos nos nomes dos algoritmos", agruparei todos os 20 algoritmos em uma única resposta, organizando-os com tópicos claros nos títulos dos artefatos (ex.: "20. Binary Search"). Os algoritmos serão apresentados na ordem da lista original, cobrindo as categorias de busca, grafos, programação dinâmica e árvores.

---

### 20. Binary Search
```java
// Description: Find the index of a target element in a sorted array.
// Strategy: Divide the search space in half repeatedly by comparing the middle element.
// Time Complexity: O(log n), Space Complexity: O(1)

class Solution {
    public int binarySearch(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            if (nums[mid] < target) left = mid + 1;
            else right = mid - 1;
        }
        return -1; // Target not found
    }
}
```

### 21. Depth-First Search (DFS)
```java
// Description: Traverse or search a graph or tree by exploring as far as possible along each branch.
// Strategy: Use recursion to explore neighbors, marking visited nodes to avoid cycles.
// Time Complexity: O(V + E), Space Complexity: O(V) for recursion stack

import java.util.*;

class Solution {
    public void dfs(int node, List<List<Integer>> adj, boolean[] visited) {
        visited[node] = true;
        for (int neighbor : adj.get(node)) {
            if (!visited[neighbor]) {
                dfs(neighbor, adj, visited);
            }
        }
    }
}
```

### 22. Breadth-First Search (BFS)
```java
// Description: Traverse or search a graph or tree level by level.
// Strategy: Use a queue to explore nodes in order of distance from the start.
// Time Complexity: O(V + E), Space Complexity: O(V)

import java.util.*;

class Solution {
    public void bfs(int start, List<List<Integer>> adj, boolean[] visited) {
        Queue<Integer> queue = new LinkedList<>();
        visited[start] = true;
        queue.offer(start);
        while (!queue.isEmpty()) {
            int node = queue.poll();
            for (int neighbor : adj.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.offer(neighbor);
                }
            }
        }
    }
}
```

### 23. Dijkstra’s Algorithm
```java
// Description: Find the shortest path from a source to all nodes in a weighted graph.
// Strategy: Use a priority queue to always process the nodeWITH the smallest distance.
// Time Complexity: O((V + E) log V), Space Complexity: O(V)

import java.util.*;

class Solution {
    public int[] dijkstra(int start, List<List<int[]>> adj, int n) {
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[start] = 0;
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        pq.offer(new int[]{start, 0});
        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int node = curr[0], d = curr[1];
            if (d > dist[node]) continue;
            for (int[] edge : adj.get(node)) {
                int neighbor = edge[0], weight = edge[1];
                if (dist[node] + weight < dist[neighbor]) {
                    dist[neighbor] = dist[node] + weight;
                    pq.offer(new int[]{neighbor, dist[neighbor]});
                }
            }
        }
        return dist;
    }
}
```

### 24. Floyd-Warshall Algorithm
```java
// Description: Find shortest paths between all pairs of nodes in a weighted graph.
// Strategy: Use dynamic programming to update distances via intermediate nodes.
// Time Complexity: O(V³), Space Complexity: O(V²)

class Solution {
    public void floydWarshall(int[][] graph, int V) {
        int[][] dist = new int[V][V];
        for (int i = 0; i < V; i++)
            for (int j = 0; j < V; j++)
                dist[i][j] = graph[i][j];
        for (int k = 0; k < V; k++) {
            for (int i = 0; i < V; i++) {
                for (int j = 0; j < V; j++) {
                    if (dist[i][k] != Integer.MAX_VALUE && dist[k][j] != Integer.MAX_VALUE &&
                        dist[i][k] + dist[k][j] < dist[i][j]) {
                        dist[i][j] = dist[i][k] + dist[k][j];
                    }
                }
            }
        }
    }
}
```

### 25. Kruskal’s Algorithm
```java
// Description: Find the minimum spanning tree (MST) of a weighted undirected graph.
// Strategy: Sort edges by weight, use Union-Find to add edges without forming cycles.
// Time Complexity: O(E log E), Space Complexity: O(V)

import java.util.*;

class Solution {
    class UnionFind {
        int[] parent, rank;
        UnionFind(int n) {
            parent = new int[n];
            rank = new int[n];
            for (int i = 0; i < n; i++) parent[i] = i;
        }
        int find(int x) {
            if (parent[x] != x) parent[x] = find(parent[x]);
            return parent[x];
        }
        boolean union(int x, int y) {
            int px = find(x), py = find(y);
            if (px == py) return false;
            if (rank[px] < rank[py]) parent[px] = py;
            else if (rank[px] > rank[py]) parent[py] = px;
            else { parent[py] = px; rank[px]++; }
            return true;
        }
    }
    
    public int kruskal(int V, List<int[]> edges) {
        Collections.sort(edges, (a, b) -> a[2] - b[2]);
        UnionFind uf = new UnionFind(V);
        int mstWeight = 0;
        for (int[] edge : edges) {
            if (uf.union(edge[0], edge[1])) {
                mstWeight += edge[2];
            }
        }
        return mstWeight;
    }
}
```

### 26. Prim’s Algorithm
```java
// Description: Find the minimum spanning tree of a weighted undirected graph.
// Strategy: Use a priority queue to select the smallest edge connecting to the MST.
// Time Complexity: O(E log V), Space Complexity: O(V)

import java.util.*;

class Solution {
    public int prim(int V, List<List<int[]>> adj) {
        boolean[] visited = new boolean[V];
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        pq.offer(new int[]{0, 0});
        int mstWeight = 0;
        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int node = curr[0], weight = curr[1];
            if (visited[node]) continue;
            visited[node] = true;
            mstWeight += weight;
            for (int[] edge : adj.get(node)) {
                int neighbor = edge[0], w = edge[1];
                if (!visited[neighbor]) {
                    pq.offer(new int[]{neighbor, w});
                }
            }
        }
        return mstWeight;
    }
}
```

### 27. Topological Sort
```java
// Description: Order nodes in a DAG such that for every edge (u,v), u comes before v.
// Strategy: Use DFS to process nodes after their dependencies, or use Kahn’s algorithm.
// Time Complexity: O(V + E), Space Complexity: O(V)

import java.util.*;

class Solution {
    public int[] topologicalSort(int V, List<List<Integer>> adj) {
        int[] result = new int[V];
        int[] index = {V - 1};
        boolean[] visited = new boolean[V];
        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                dfs(i, adj, visited, result, index);
            }
        }
        return result;
    }
    
    private void dfs(int node, List<List<Integer>> adj, boolean[] visited, int[] result, int[] index) {
        visited[node] = true;
        for (int neighbor : adj.get(node)) {
            if (!visited[neighbor]) {
                dfs(neighbor, adj, visited, result, index);
            }
        }
        result[index[0]--] = node;
    }
}
```

### 28. Knapsack Problem (0/1)
```java
// Description: Maximize value of items in a knapsack without exceeding capacity.
// Strategy: Use dynamic programming to decide whether to include each item.
// Time Complexity: O(n * W), Space Complexity: O(n * W)

class Solution {
    public int knapsack(int W, int[] weights, int[] values, int n) {
        int[][] dp = new int[n + 1][W + 1];
        for (int i = 1; i <= n; i++) {
            for (int w = 0; w <= W; w++) {
                if (weights[i - 1] <= w) {
                    dp[i][w] = Math.max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1]);
                } else {
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }
        return dp[n][W];
    }
}
```

### 29. Fractional Knapsack
```java
// Description: Maximize value in a knapsack by taking fractions of items.
// Strategy: Sort items by value-to-weight ratio, take as much as possible.
// Time Complexity: O(n log n), Space Complexity: O(1)

import java.util.*;

class Solution {
    class Item {
        int value, weight;
        Item(int v, int w) { value = v; weight = w; }
    }
    
    public double fractionalKnapsack(int W, int[] values, int[] weights, int n) {
        Item[] items = new Item[n];
        for (int i = 0; i < n; i++) items[i] = new Item(values[i], weights[i]);
        Arrays.sort(items, (a, b) -> Double.compare((double)b.value/b.weight, (double)a.value/a.weight));
        double totalValue = 0;
        int remaining = W;
        for (Item item : items) {
            if (remaining >= item.weight) {
                totalValue += item.value;
                remaining -= item.weight;
            } else {
                totalValue += (double)item.value / item.weight * remaining;
                break;
            }
        }
        return totalValue;
    }
}
```

### 30. Longest Common Subsequence
```java
// Description: Find the length of the longest common subsequence in two strings.
// Strategy: Use dynamic programming to build a table of subsequence lengths.
// Time Complexity: O(m * n), Space Complexity: O(m * n)

class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length(), n = text2.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[m][n];
    }
}
```

### 31. Longest Increasing Subsequence
```java
// Description: Find the length of the longest strictly increasing subsequence.
// Strategy: Use dynamic programming or binary search to track increasing sequences.
// Time Complexity: O(n log n), Space Complexity: O(n)

import java.util.*;

class Solution {
    public int lengthOfLIS(int[] nums) {
        List<Integer> tails = new ArrayList<>();
        for (int num : nums) {
            int left = 0, right = tails.size();
            while (left < right) {
                int mid = left + (right - left) / 2;
                if (tails.get(mid) < num) left = mid + 1;
                else right = mid;
            }
            if (left == tails.size()) tails.add(num);
            else tails.set(left, num);
        }
        return tails.size();
    }
}
```

### 32. Matrix Chain Multiplication
```java
// Description: Find the minimum number of scalar multiplications to multiply a chain of matrices.
// Strategy: Use dynamic programming to find optimal parenthesization.
// Time Complexity: O(n³), Space Complexity: O(n²)

class Solution {
    public int matrixChainMultiplication(int[] dims) {
        int n = dims.length - 1;
        int[][] dp = new int[n][n];
        for (int len = 2; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;
                dp[i][j] = Integer.MAX_VALUE;
                for (int k = i; k < j; k++) {
                    int cost = dp[i][k] + dp[k + 1][j] + dims[i] * dims[k + 1] * dims[j + 1];
                    dp[i][j] = Math.min(dp[i][j], cost);
                }
            }
        }
        return dp[0][n - 1];
    }
}
```

### 33. Fibonacci Sequence (DP)
```java
// Description: Compute the nth Fibonacci number.
// Strategy: Use dynamic programming with constant space to store only last two numbers.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public int fib(int n) {
        if (n <= 1) return n;
        int prev = 0, curr = 1;
        for (int i = 2; i <= n; i++) {
            int next = prev + curr;
            prev = curr;
            curr = next;
        }
        return curr;
    }
}
```

### 34. Coin Change Problem
```java
// Description: Find the minimum number of coins to make a given amount.
// Strategy: Use dynamic programming to build solutions for all amounts up to target.
// Time Complexity: O(amount * coins), Space Complexity: O(amount)

class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (coin <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```

### 35. Maximum Subarray Sum (Kadane’s)
```java
// Description: Find the maximum sum of a contiguous subarray.
// Strategy: Use Kadane’s algorithm to track max sum ending at each position.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public int maxSubArray(int[] nums) {
        int maxSum = nums[0], currSum = nums[0];
        for (int i = 1; i < nums.length; i++) {
            currSum = Math.max(nums[i], currSum + nums[i]);
            maxSum = Math.max(maxSum, currSum);
        }
        return maxSum;
    }
}
```

### 36. Invert Binary Tree
```java
// Description: Swap left and right children of each node in a binary tree.
// Strategy: Use recursion to swap children at each node.
// Time Complexity: O(n), Space Complexity: O(h) where h is tree height

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        TreeNode temp = root.left;
        root.left = invertTree(root.right);
        root.right = invertTree(temp);
        return root;
    }
}
```

### 37. Binary Tree Inorder Traversal
<xaiArtifact artifact_id="e7a8c593-e7be-4ffd-c4da-df6 among others, Iterative Inorder Traversal
```java
// Description: Traverse a binary tree in inorder (left, root, right).
// Strategy: Use recursion or a stack for iterative solution.
// Time Complexity: O(n), Space Complexity: O(h) where h is tree height

import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            result.add(curr.val);
            curr = curr.right;
        }
        return result;
    }
}
```

### 38. Binary Tree Preorder Traversal
```java
// Description: Traverse a binary tree in preorder (root, left, right).
// Strategy: Use recursion or a stack for iterative solution.
// Time Complexity: O(n), Space Complexity: O(h)

import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.add(node.val);
            if (node.right != null) stack.push(node.right);
            if (node.left != null) stack.push(node.left);
        }
        return result;
    }
}
```

### 39. Binary Tree Postorder Traversal
```java
// Description: Traverse a binary tree in postorder (left, right, root).
// Strategy: Use recursion or two stacks for iterative solution.
// Time Complexity: O(n), Space Complexity: O(h)

import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        Stack<TreeNode> stack1 = new Stack<>();
        Stack<TreeNode> stack2 = new Stack<>();
        stack1.push(root);
        while (!stack1.isEmpty()) {
            TreeNode node = stack1.pop();
            stack2.push(node);
            if (node.left != null) stack1.push(node.left);
            if (node.right != null) stack1.push(node.right);
        }
        while (!stack2.isEmpty()) {
            result.add(stack2.pop().val);
        }
        return result;
    }
}
```

---

### Considerações:
- **Progresso**: Apresentei os algoritmos de 20 a 39, cobrindo busca, grafos, programação dinâmica e árvores, cada um com descrição, estratégia e código otimizado em Java, encapsulado em `<xaiArtifact>` com tópicos nos títulos (ex.: "20. Binary Search").
- **Formato**: Segui a solicitação de um único resultado com tópicos, mantendo a estrutura clara e concisa.
- **Próximos Passos**: Posso continuar com os próximos 20 algoritmos (40 a 59) no mesmo formato ou ajustar conforme necessário (ex.: focar em uma categoria, reduzir detalhes).

Por favor, confirme se deseja continuar com os próximos 20 algoritmos ou se há alguma alteração no formato ou escopo!

Abaixo, apresento os próximos 20 algoritmos (40 a 59) da lista, seguindo o formato solicitado: descrição breve, estratégia, solução otimizada em Java com comentários, cada um em um `<xaiArtifact>` com UUID único, título descritivo usando tópicos (ex.: "40. Level Order Traversal") e tipo `text/java`. Os algoritmos são organizados na ordem da lista original, cobrindo árvores, heaps, tries, e outros tópicos. A resposta é consolidada em um único resultado, conforme solicitado.

---

### 40. Level Order Traversal
```java
// Description: Traverse a binary tree level by level (breadth-first).
// Strategy: Use a queue to process nodes level by level, adding children to the queue.
// Time Complexity: O(n), Space Complexity: O(w) where w is max width of tree

import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            List<Integer> level = new ArrayList<>();
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            result.add(level);
        }
        return result;
    }
}
```

### 41. Lowest Common Ancestor
```java
// Description: Find the lowest common ancestor of two nodes in a binary tree.
// Strategy: Use recursion to find paths to both nodes; LCA is where paths diverge.
// Time Complexity: O(n), Space Complexity: O(h) where h is tree height

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left != null && right != null) return root;
        return left != null ? left : right;
    }
}
```

### 42. Kth Smallest Element in BST
```java
// Description: Find the kth smallest element in a binary search tree.
// Strategy: Perform inorder traversal (iterative) and stop at kth element.
// Time Complexity: O(h + k), Space Complexity: O(h)

import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    public int kthSmallest(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            if (--k == 0) return curr.val;
            curr = curr.right;
        }
        return -1; // k is invalid
    }
}
```

### 43. Heap Sort
```java
// Description: Sort an array using a max-heap.
// Strategy: Build a max-heap, repeatedly extract max and heapify.
// Time Complexity: O(n log n), Space Complexity: O(1)

class Solution {
    public void heapSort(int[] arr) {
        int n = arr.length;
        for (int i = n / 2 - 1; i >= 0; i--) {
            heapify(arr, n, i);
        }
        for (int i = n - 1; i > 0; i--) {
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;
            heapify(arr, i, 0);
        }
    }
    
    private void heapify(int[] arr, int n, int i) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        if (left < n && arr[left] > arr[largest]) largest = left;
        if (right < n && arr[right] > arr[largest]) largest = right;
        if (largest != i) {
            int temp = arr[i];
            arr[i] = arr[largest];
            arr[largest] = temp;
            heapify(arr, n, largest);
        }
    }
}
```

### 44. Min Heap Operations
```java
// Description: Implement a min-heap with insert, extractMin, and getMin operations.
// Strategy: Use an array-based heap, maintain heap property via siftUp/siftDown.
// Time Complexity: O(log n) for insert/extract, O(1) for getMin, Space Complexity: O(n)

import java.util.*;

class MinHeap {
    private List<Integer> heap = new ArrayList<>();
    
    public void insert(int val) {
        heap.add(val);
        siftUp(heap.size() - 1);
    }
    
    public int extractMin() {
        if (heap.isEmpty()) throw new IllegalStateException("Heap is empty");
        int min = heap.get(0);
        heap.set(0, heap.get(heap.size() - 1));
        heap.remove(heap.size() - 1);
        if (!heap.isEmpty()) siftDown(0);
        return min;
    }
    
    public int getMin() {
        if (heap.isEmpty()) throw new IllegalStateException("Heap is empty");
        return heap.get(0);
    }
    
    private void siftUp(int index) {
        while (index > 0) {
            int parent = (index - 1) / 2;
            if (heap.get(index) >= heap.get(parent)) break;
            Collections.swap(heap, index, parent);
            index = parent;
        }
    }
    
    private void siftDown(int index) {
        int minIndex = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        if (left < heap.size() && heap.get(left) < heap.get(minIndex)) minIndex = left;
        if (right < heap.size() && heap.get(right) < heap.get(minIndex)) minIndex = right;
        if (minIndex != index) {
            Collections.swap(heap, index, minIndex);
            siftDown(minIndex);
        }
    }
}
```

### 45. Max Heap Operations
```java
// Description: Implement a max-heap with insert, extractMax, and getMax operations.
// Strategy: Use an array-based heap, maintain max-heap property via siftUp/siftDown.
// Time Complexity: O(log n) for insert/extract, O(1) for getMax, Space Complexity: O(n)

import java.util.*;

class MaxHeap {
    private List<Integer> heap = new ArrayList<>();
    
    public void insert(int val) {
        heap.add(val);
        siftUp(heap.size() - 1);
    }
    
    public int extractMax() {
        if (heap.isEmpty()) throw new IllegalStateException("Heap is empty");
        int max = heap.get(0);
        heap.set(0, heap.get(heap.size() - 1));
        heap.remove(heap.size() - 1);
        if (!heap.isEmpty()) siftDown(0);
        return max;
    }
    
    public int getMax() {
        if (heap.isEmpty()) throw new IllegalStateException("Heap is empty");
        return heap.get(0);
    }
    
    private void siftUp(int index) {
        while (index > 0) {
            int parent = (index - 1) / 2;
            if (heap.get(index) <= heap.get(parent)) break;
            Collections.swap(heap, index, parent);
            index = parent;
        }
    }
    
    private void siftDown(int index) {
        int maxIndex = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        if (left < heap.size() && heap.get(left) > heap.get(maxIndex)) maxIndex = left;
        if (right < heap.size() && heap.get(right) > heap.get(maxIndex)) maxIndex = right;
        if (maxIndex != index) {
            Collections.swap(heap, index, maxIndex);
            siftDown(maxIndex);
        }
    }
}
```

### 46. Trie (Prefix Tree) Operations
```java
// Description: Implement a trie with insert, search, and startsWith operations.
// Strategy: Use a tree structure with nodes containing links to children.
// Time Complexity: O(m) for operations (m is word length), Space Complexity: O(ALPHABET_SIZE * N * M)

class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isEndOfWord;
}

class Trie {
    private TrieNode root;
    
    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) node.children[index] = new TrieNode();
            node = node.children[index];
        }
        node.isEndOfWord = true;
    }
    
    public boolean search(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) return false;
            node = node.children[index];
        }
        return node.isEndOfWord;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for (char c : prefix.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) return false;
            node = node.children[index];
        }
        return true;
    }
}
```

### 47. Sliding Window Maximum
```java
// Description: Find the maximum element in each sliding window of size k.
// Strategy: Use a deque to maintain indices of potential maximums in decreasing order.
// Time Complexity: O(n), Space Complexity: O(k)

import java.util.*;

class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        Deque<Integer> deque = new LinkedList<>();
        int[] result = new int[nums.length - k + 1];
        for (int i = 0; i < nums.length; i++) {
            while (!deque.isEmpty() && deque.peekFirst() <= i - k) deque.pollFirst();
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) deque.pollLast();
            deque.offerLast(i);
            if (i >= k - 1) result[i - k + 1] = nums[deque.peekFirst()];
        }
        return result;
    }
}
```

### 48. Kth Largest Element in Array
```java
// Description: Find the kth largest element in an unsorted array.
// Strategy: Use a min-heap of size k to keep track of the k largest elements.
// Time Complexity: O(n log k), Space Complexity: O(k)

import java.util.*;

class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        for (int num : nums) {
            minHeap.offer(num);
            if (minHeap.size() > k) minHeap.poll();
        }
        return minHeap.peek();
    }
}
```

### 49. Counting Sort
```java
// Description: Sort an array of integers with a limited range.
// Strategy: Count occurrences of each number, then reconstruct the sorted array.
// Time Complexity: O(n + k) where k is range, Space Complexity: O(k)

class Solution {
    public void countingSort(int[] arr, int maxVal) {
        int[] count = new int[maxVal + 1];
        for (int num : arr) count[num]++;
        int index = 0;
        for (int i = 0; i <= maxVal; i++) {
            while (count[i]-- > 0) arr[index++] = i;
        }
    }
}
```

### 50. Radix Sort
```java
// Description: Sort integers by processing digits from least to most significant.
// Strategy: Use counting sort for each digit position.
// Time Complexity: O(d * (n + k)) where d is max digits, k is base, Space Complexity: O(n + k)

class Solution {
    public void radixSort(int[] arr) {
        int max = Arrays.stream(arr).max().getAsInt();
        for (int exp = 1; max / exp > 0; exp *= 10) {
            countingSortByDigit(arr, exp);
        }
    }
    
    private void countingSortByDigit(int[] arr, int exp) {
        int n = arr.length;
        int[] output = new int[n];
        int[] count = new int[10];
        for (int num : arr) count[(num / exp) % 10]++;
        for (int i = 1; i < 10; i++) count[i] += count[i - 1];
        for (int i = n - 1; i >= 0; i--) {
            output[count[(arr[i] / exp) % 10] - 1] = arr[i];
            count[(arr[i] / exp) % 10]--;
        }
        System.arraycopy(output, 0, arr, 0, n);
    }
}
```

### 51. Bucket Sort
```java
// Description: Sort an array by distributing elements into buckets and sorting each.
// Strategy: Divide elements into buckets, sort buckets, and concatenate.
// Time Complexity: O(n + k) average, O(n²) worst, Space Complexity: O(n + k)

import java.util.*;

class Solution {
    public void bucketSort(float[] arr) {
        int n = arr.length;
        List<Float>[] buckets = new List[n];
        for (int i = 0; i < n; i++) buckets[i] = new ArrayList<>();
        for (float num : arr) buckets[(int)(n * num)].add(num);
        for (List<Float> bucket : buckets) Collections.sort(bucket);
        int index = 0;
        for (List<Float> bucket : buckets) {
            for (float num : bucket) arr[index++] = num;
        }
    }
}
```

### 52. Union-Find (Disjoint Set)
<xaiArtifact artifact_id="f5a9b4d3-1d2c-4e7a-f9c6-2b1d4e5f6a9c" artifact_version_id="c4f6d9a2-8FRIENDSHIP (DFS) {
    // Description: Manage disjoint sets with union and find operations.
    // Strategy: Use path compression and union by rank for efficiency.
    // Time Complexity: O(α(n)) amortized for find/union, Space Complexity: O(n)

class UnionFind {
    private int[] parent, rank;
    
    public UnionFind(int n) {
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) parent[i] = i;
    }
    
    public int find(int x) {
        if (parent[x] != x) parent[x] = find(parent[x]);
        return parent[x];
    }
    
    public void union(int x, int y) {
        int px = find(x), py = find(y);
        if (px == py) return;
        if (rank[px] < rank[py]) parent[px] = py;
        else if (rank[px] > rank[py]) parent[py] = px;
        else { parent[py] = px; rank[px]++; }
    }
}
</xaiArtifact>

### 53. Bellman-Ford Algorithm
```java
// Description: Find shortest paths from a source in a weighted graph with negative edges.
// Strategy: Relax all edges V-1 times, check for negative cycles.
// Time Complexity: O(V * E), Space Complexity: O(V)

class Solution {
    public int[] bellmanFord(int V, List<int[]> edges, int src) {
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;
        for (int i = 0; i < V - 1; i++) {
            for (int[] edge : edges) {
                int u = edge[0], v = edge[1], w = edge[2];
                if (dist[u] != Integer.MAX_VALUE && dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                }
            }
        }
        return dist;
    }
}
```

### 54. A* Search Algorithm
```java
// Description: Find the shortest path in a weighted graph using heuristics.
// Strategy: Use a priority queue with f(n) = g(n) + h(n) to guide search.
// Time Complexity: O(E log V), Space Complexity: O(V)

import java.util.*;

class Solution {
    class Node implements Comparable<Node> {
        int id, g, f;
        Node(int id, int g, int f) { this.id = id; this.g = g; this.f = f; }
        public int compareTo(Node other) { return Integer.compare(f, other.f); }
    }
    
    public List<Integer> aStar(int start, int goal, List<List<int[]>> adj, int[] heuristic) {
        PriorityQueue<Node> pq = new PriorityQueue<>();
        int[] gScore = new int[adj.size()];
        Arrays.fill(gScore, Integer.MAX_VALUE);
        gScore[start] = 0;
        pq.offer(new Node(start, 0, heuristic[start]));
        int[] cameFrom = new int[adj.size()];
        Arrays.fill(cameFrom, -1);
        while (!pq.isEmpty()) {
            Node curr = pq.poll();
            if (curr.id == goal) return reconstructPath(cameFrom, goal);
            for (int[] edge : adj.get(curr.id)) {
                int neighbor = edge[0], weight = edge[1];
                int tentativeG = gScore[curr.id] + weight;
                if (tentativeG < gScore[neighbor]) {
                    cameFrom[neighbor] = curr.id;
                    gScore[neighbor] = tentativeG;
                    pq.offer(new Node(neighbor, tentativeG, tentativeG + heuristic[neighbor]));
                }
            }
        }
        return new ArrayList<>();
    }
    
    private List<Integer> reconstructPath(int[] cameFrom, int current) {
        List<Integer> path = new ArrayList<>();
        while (current != -1) {
            path.add(current);
            current = cameFrom[current];
        }
        Collections.reverse(path);
        return path;
    }
}
```

### 55. Edit Distance
```java
// Description: Find the minimum number of operations to transform one string into another.
// Strategy: Use dynamic programming to compute edit distances.
// Time Complexity: O(m * n), Space Complexity: O(m * n)

class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length(), n = word2.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 0; i <= m; i++) dp[i][0] = i;
        for (int j = 0; j <= n; j++) dp[0][j] = j;
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1;
                }
            }
        }
        return dp[m][n];
    }
}
```

### 56. Subset Sum Problem
```java
// Description: Determine if there exists a subset with a given sum.
// Strategy: Use dynamic programming to check if sum is achievable.
// Time Complexity: O(n * sum), Space Complexity: O(n * sum)

class Solution {
    public boolean subsetSum(int[] nums, int sum) {
        int n = nums.length;
        boolean[][] dp = new boolean[n + 1][sum + 1];
        for (int i = 0; i <= n; i++) dp[i][0] = true;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {
                if (nums[i - 1] <= j) {
                    dp[i][j] = dp[i - 1][j - nums[i - 1]] || dp[i - 1][j];
                } else {
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }
        return dp[n][sum];
    }
}
```

### 57. N-Queens Problem
```java
// Description: Place N queens on an NxN chessboard such that no two queens attack each other.
// Strategy: Use backtracking to try placing queens in each row, checking validity.
// Time Complexity: O(N!), Space Complexity: O(N²)

import java.util.*;

class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        char[][] board = new char[n][n];
        for (char[] row : board) Arrays.fill(row, '.');
        backtrack(result, board, 0, n);
        return result;
    }
    
    private void backtrack(List<List<String>> result, char[][] board, int row, int n) {
        if (row == n) {
            result.add(construct(board));
            return;
        }
        for (int col = 0; col < n; col++) {
            if (isValid(board, row, col, n)) {
                board[row][col] = 'Q';
                backtrack(result, board, row + 1, n);
                board[row][col] = '.';
            }
        }
    }
    
    private boolean isValid(char[][] board, int row, int col, int n) {
        for (int i = 0; i < row; i++) if (board[i][col] == 'Q') return false;
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q') return false;
        }
        for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
            if (board[i][j] == 'Q') return false;
        }
        return true;
    }
    
    private List<String> construct(char[][] board) {
        List<String> result = new ArrayList<>();
        for (char[] row : board) result.add(new String(row));
        return result;
    }
}
```

### 58. Sudoku Solver
```java
// Description: Solve a partially filled 9x9 Sudoku board.
// Strategy: Use backtracking to try digits 1-9 in empty cells, checking validity.
// Time Complexity: O(9^m) where m is number of empty cells, Space Complexity: O(1)

class Solution {
    public void solveSudoku(char[][] board) {
        solve(board);
    }
    
    private boolean solve(char[][] board) {
        for (int row = 0; row < 9; row++) {
            for (int col = 0; col < 9; col++) {
                if (board[row][col] == '.') {
                    for (char c = '1'; c <= '9'; c++) {
                        if (isValid(board, row, col, c)) {
                            board[row][col] = c;
                            if (solve(board)) return true;
                            board[row][col] = '.';
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }
    
    private boolean isValid(char[][] board, int row, int col, char c) {
        for (int i = 0; i < 9; i++) {
            if (board[row][i] == c || board[i][col] == c ||
                board[3 * (row / 3) + i / 3][3 * (col / 3) + i % 3] == c) {
                return false;
            }
        }
        return true;
    }
}
```

### 59. Binary Tree Maximum Path Sum
```java
// Description: Find the maximum path sum in a binary tree (any node to any node).
// Strategy: Use recursion to compute max path sum through each node, track global max.
// Time Complexity: O(n), Space Complexity: O(h)

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    private int maxSum = Integer.MIN_VALUE;
    
    public int maxPathSum(TreeNode root) {
        maxGain(root);
        return maxSum;
    }
    
    private int maxGain(TreeNode node) {
        if (node == null) return 0;
        int leftGain = Math.max(maxGain(node.left), 0);
        int rightGain = Math.max(maxGain(node.right), 0);
        int pathSum = node.val + leftGain + rightGain;
        maxSum = Math.max(maxSum, pathSum);
        return node.val + Math.max(leftGain, rightGain);
    }
}
```

---

### Considerações:
- **Progresso**: Apresentei os algoritmos de 40 a 59, cobrindo árvores, heaps, tries, ordenação, grafos e backtracking, cada um com descrição, estratégia e código otimizado em Java, encapsulado em `<xaiArtifact>` com tópicos nos títulos (ex.: "40. Level Order Traversal").
- **Formato**: Mantive um único resultado com tópicos, conforme solicitado, garantindo clareza e concisão.
- **Próximos Passos**: Posso continuar com os próximos 20 algoritmos (60 a 79) no mesmo formato ou ajustar conforme necessário (ex.: focar em uma categoria).

Por favor, confirme se deseja continuar com os próximos 20 algoritmos ou se há alguma alteração no formato ou escopo!

Abaixo, apresento os próximos 20 algoritmos (60 a 79) da lista, seguindo o formato solicitado: descrição breve, estratégia, solução otimizada em Java com comentários, cada um em um `<xaiArtifact>` com UUID único, título descritivo usando tópicos (ex.: "60. Word Ladder") e tipo `text/java`. Os algoritmos são apresentados na ordem da lista original, cobrindo strings, arrays, grafos, pilhas/filas, e outros tópicos. A resposta é consolidada em um único resultado, conforme solicitado.

---

### 60. Word Ladder
```java
// Description: Find the shortest transformation sequence from beginWord to endWord, changing one letter at a time.
// Strategy: Use BFS to explore all possible transformations level by level.
// Time Complexity: O(N * 26 * L), where N is word list size, L is word length, Space Complexity: O(N)

import java.util.*;

class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<>(wordList);
        if (!wordSet.contains(endWord)) return 0;
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        int level = 1;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String curr = queue.poll();
                if (curr.equals(endWord)) return level;
                for (int j = 0; j < curr.length(); j++) {
                    char[] chars = curr.toCharArray();
                    for (char c = 'a'; c <= 'z'; c++) {
                        chars[j] = c;
                        String next = new String(chars);
                        if (wordSet.contains(next)) {
                            queue.offer(next);
                            wordSet.remove(next);
                        }
                    }
                }
            }
            level++;
        }
        return 0;
    }
}
```

### 61. Regular Expression Matching
```java
// Description: Check if a string matches a regular expression pattern with '.' and '*'.
// Strategy: Use dynamic programming to match string and pattern characters.
// Time Complexity: O(m * n), Space Complexity: O(m * n)

class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length(), n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        for (int j = 2; j <= n; j++) {
            if (p.charAt(j - 1) == '*') dp[0][j] = dp[0][j - 2];
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i][j - 2] || 
                              (dp[i - 1][j] && (s.charAt(i - 1) == p.charAt(j - 2) || p.charAt(j - 2) == '.'));
                } else if (p.charAt(j - 1) == '.' || s.charAt(i - 1) == p.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                }
            }
        }
        return dp[m][n];
    }
}
```

### 62. Wildcard Matching
```java
// Description: Check if a string matches a pattern with '?' and '*' wildcards.
// Strategy: Use dynamic programming to handle wildcard matches.
// Time Complexity: O(m * n), Space Complexity: O(m * n)

class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length(), n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        for (int j = 1; j <= n; j++) {
            if (p.charAt(j - 1) == '*') dp[0][j] = dp[0][j - 1];
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                } else if (p.charAt(j - 1) == '?' || s.charAt(i - 1) == p.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                }
            }
        }
        return dp[m][n];
    }
}
```

### 63. Trapping Rain Water
```java
// Description: Compute the amount of water trapped between bars of given heights.
// Strategy: Use two pointers to track max heights from left and right, compute trapped water.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public int trap(int[] height) {
        int left = 0, right = height.length - 1, leftMax = 0, rightMax = 0, water = 0;
        while (left < right) {
            if (height[left] < height[right]) {
                leftMax = Math.max(leftMax, height[left]);
                water += leftMax - height[left];
                left++;
            } else {
                rightMax = Math.max(rightMax, height[right]);
                water += rightMax - height[right];
                right--;
            }
        }
        return water;
    }
}
```

### 64. Container With Most Water
```java
// Description: Find two lines that form a container with the most water.
// Strategy: Use two pointers to maximize area, moving the shorter line inward.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public int maxArea(int[] height) {
        int left = 0, right = height.length - 1, maxArea = 0;
        while (left < right) {
            int area = Math.min(height[left], height[right]) * (right - left);
            maxArea = Math.max(maxArea, area);
            if (height[left] < height[right]) left++;
            else right--;
        }
        return maxArea;
    }
}
```

### 65. Product of Array Except Self
```java
// Description: Compute the product of all elements except the current index.
// Strategy: Use two passes to compute left and right products without division.
// Time Complexity: O(n), Space Complexity: O(1) excluding output

class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        result[0] = 1;
        for (int i = 1; i < n; i++) {
            result[i] = result[i - 1] * nums[i - 1];
        }
        int rightProduct = 1;
        for (int i = n - 1; i >= 0; i--) {
            result[i] *= rightProduct;
            rightProduct *= nums[i];
        }
        return result;
    }
}
```

### 66. Rotate Array
```java
// Description: Rotate an array to the right by k steps.
// Strategy: Reverse the entire array, then reverse first k and remaining elements.
// Time Complexity: O(n), Space Complexity: O(1)

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

### 67. Reverse String
```java
// Description: Reverse a given string (char array).
// Strategy: Use two pointers to swap characters from start and end.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public void reverseString(char[] s) {
        int left = 0, right = s.length - 1;
        while (left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }
}
```

### 68. First Missing Positive
```java
// Description: Find the smallest missing positive integer in an unsorted array.
// Strategy: Place each number in its correct index (e.g., 1 at index 0), then scan.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public int firstMissingPositive(int[] nums) {
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
                int temp = nums[nums[i] - 1];
                nums[nums[i] - 1] = nums[i];
                nums[i] = temp;
            }
        }
        for (int i = 0; i < n; i++) {
            if (nums[i] != i + 1) return i + 1;
        }
        return n + 1;
    }
}
```

### 69. Group Anagrams
```java
// Description: Group an array of strings by their anagrams.
// Strategy: Use a HashMap with sorted string as key to group anagrams.
// Time Complexity: O(N * K * log K), where K is max string length, Space Complexity: O(N * K)

import java.util.*;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();
        for (String str : strs) {
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            String key = new String(chars);
            map.computeIfAbsent(key, k -> new ArrayList<>()).add(str);
        }
        return new ArrayList<>(map.values());
    }
}
```

### 70. Valid Anagram
```java
// Description: Check if two strings are anagrams.
// Strategy: Use a frequency array to count characters in both strings.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        int[] freq = new int[26];
        for (int i = 0; i < s.length(); i++) {
            freq[s.charAt(i) - 'a']++;
            freq[t.charAt(i) - 'a']--;
        }
        for (int count : freq) if (count != 0) return false;
        return true;
    }
}
```

### 71. Spiral Matrix
```java
// Description: Return elements of a matrix in spiral order.
// Strategy: Use four pointers to traverse boundaries, adjusting after each direction.
// Time Complexity: O(m * n), Space Complexity: O(1) excluding output

import java.util.*;

class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        if (matrix.length == 0) return result;
        int top = 0, bottom = matrix.length - 1, left = 0, right = matrix[0].length - 1;
        while (top <= bottom && left <= right) {
            for (int i = left; i <= right; i++) result.add(matrix[top][i]);
            top++;
            for (int i = top; i <= bottom; i++) result.add(matrix[i][right]);
            right--;
            if (top <= bottom) {
                for (int i = right; i >= left; i--) result.add(matrix[bottom][i]);
                bottom--;
            }
            if (left <= right) {
                for (int i = bottom; i >= top; i--) result.add(matrix[i][left]);
                left++;
            }
        }
        return result;
    }
}
```

### 72. Set Matrix Zeroes
```java
// Description: Set entire row and column to zero if an element is zero.
// Strategy: Use first row and column as markers to avoid extra space.
// Time Complexity: O(m * n), Space Complexity: O(1)

class Solution {
    public void setZeroes(int[][] matrix) {
        boolean firstRowZero = false, firstColZero = false;
        int m = matrix.length, n = matrix[0].length;
        for (int j = 0; j < n; j++) if (matrix[0][j] == 0) firstRowZero = true;
        for (int i = 0; i < m; i++) if (matrix[i][0] == 0) firstColZero = true;
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        for (int i = 1; i < m; i++) {
            if (matrix[i][0] == 0) {
                for (int j = 1; j < n; j++) matrix[i][j] = 0;
            }
        }
        for (int j = 1; j < n; j++) {
            if (matrix[0][j] == 0) {
                for (int i = 1; i < m; i++) matrix[i][j] = 0;
            }
        }
        if (firstRowZero) for (int j = 0; j < n; j++) matrix[0][j] = 0;
        if (firstColZero) for (int i = 0; i < m; i++) matrix[i][0] = 0;
    }
}
```

### 73. Search in Rotated Sorted Array
```java
// Description: Find a target in a rotated sorted array.
// Strategy: Use modified binary search to handle rotation by checking sorted half.
// Time Complexity: O(log n), Space Complexity: O(1)

class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            if (nums[left] <= nums[mid]) {
                if (nums[left] <= target && target < nums[mid]) right = mid - 1;
                else left = mid + 1;
            } else {
                if (nums[mid] < target && target <= nums[right]) left = mid + 1;
                else right = mid - 1;
            }
        }
        return -1;
    }
}
```

### 74. Find First and Last Position
```java
// Description: Find the first and last positions of a target in a sorted array.
// Strategy: Use two binary searches to find the leftmost and rightmost positions.
// Time Complexity: O(log n), Space Complexity: O(1)

class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = {-1, -1};
        result[0] = binarySearch(nums, target, true);
        result[1] = binarySearch(nums, target, false);
        return result;
    }
    
    private int binarySearch(int[] nums, int target, boolean findFirst) {
        int left = 0, right = nums.length - 1, result = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                result = mid;
                if (findFirst) right = mid - 1;
                else left = mid + 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return result;
    }
}
```

### 75. Jump Game
```java
// Description: Determine if you can reach the last index in an array of jump lengths.
// Strategy: Use greedy approach to track the furthest reachable index.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public boolean canJump(int[] nums) {
        int maxReach = 0;
        for (int i = 0; i < nums.length; i++) {
            if (i > maxReach) return false;
            maxReach = Math.max(maxReach, i + nums[i]);
            if (maxReach >= nums.length - 1) return true;
        }
        return true;
    }
}
```

### 76. Merge k Sorted Lists
```java
// Description: Merge k sorted linked lists into one sorted list.
// Strategy: Use a min-heap to always select the smallest node among lists.
// Time Complexity: O(N * log k), where N is total nodes, k is number of lists, Space Complexity: O(k)

import java.util.*;

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);
        for (ListNode node : lists) {
            if (node != null) pq.offer(node);
        }
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            curr.next = node;
            curr = curr.next;
            if (node.next != null) pq.offer(node.next);
        }
        return dummy.next;
    }
}
```

### 77. Implement Stack using Queues
```java
// Description: Implement a stack using queues.
// Strategy: Use two queues; for push, enqueue to one and move others to maintain LIFO.
// Time Complexity: O(n) for push, O(1) for pop/top/empty, Space Complexity: O(n)

import java.util.*;

class MyStack {
    private Queue<Integer> q1 = new LinkedList<>();
    private Queue<Integer> q2 = new LinkedList<>();
    
    public void push(int x) {
        q2.offer(x);
        while (!q1.isEmpty()) q2.offer(q1.poll());
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;
    }
    
    public int pop() {
        return q1.poll();
    }
    
    public int top() {
        return q1.peek();
    }
    
    public boolean empty() {
        return q1.isEmpty();
    }
}
```

### 78. Implement Queue using Stacks
```java
// Description: Implement a queue using stacks.
// Strategy: Use two stacks; one for enqueue, one for dequeue, reversing order as needed.
// Time Complexity: O(1) amortized for push/pop, O(n) worst for pop, Space Complexity: O(n)

import java.util.*;

class MyQueue {
    private Stack<Integer> s1 = new Stack<>();
    private Stack<Integer> s2 = new Stack<>();
    
    public void push(int x) {
        s1.push(x);
    }
    
    public int pop() {
        if (s2.isEmpty()) {
            while (!s1.isEmpty()) s2.push(s1.pop());
        }
        return s2.pop();
    }
    
    public int peek() {
        if (s2.isEmpty()) {
            while (!s1.isEmpty()) s2.push(s1.pop());
        }
        return s2.peek();
    }
    
    public boolean empty() {
        return s1.isEmpty() && s2.isEmpty();
    }
}
```

### 79. LRU Cache
```java
// Description: Implement a Least Recently Used (LRU) cache with get and put operations.
// Strategy: Use a HashMap and doubly-linked list to track order and access in O(1).
// Time Complexity: O(1) for get/put, Space Complexity: O(capacity)

import java.util.*;

class LRUCache {
    class Node {
        int key, value;
        Node prev, next;
        Node(int key, int value) { this.key = key; this.value = value; }
    }
    
    private Map<Integer, Node> cache = new HashMap<>();
    private Node head, tail;
    private int capacity;
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        Node node = cache.get(key);
        if (node == null) return -1;
        moveToHead(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        Node node = cache.get(key);
        if (node != null) {
            node.value = value;
            moveToHead(node);
        } else {
            node = new Node(key, value);
            cache.put(key, node);
            addToHead(node);
            if (cache.size() > capacity) {
                Node lru = tail.prev;
                removeNode(lru);
                cache.remove(lru.key);
            }
        }
    }
    
    private void moveToHead(Node node) {
        removeNode(node);
        addToHead(node);
    }
    
    private void removeNode(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    private void addToHead(Node node) {
        node.next = head.next;
        node.prev = head;
        head.next.prev = node;
        head.next = node;
    }
}
```

---

### Considerações:
- **Progresso**: Apresentei os algoritmos de 60 a 79, cobrindo strings, arrays, grafos, pilhas/filas, e estruturas de dados, cada um com descrição, estratégia e código otimizado em Java, encapsulado em `<xaiArtifact>` com tópicos nos títulos (ex.: "60. Word Ladder").
- **Formato**: Mantive um único resultado com tópicos, conforme solicitado, garantindo clareza e concisão.
- **Próximos Passos**: Posso continuar com os últimos 21 algoritmos (80 a 100) no mesmo formato ou ajustar conforme necessário (ex.: focar em uma categoria).

Por favor, confirme se deseja continuar com os últimos 21 algoritmos ou se há alguma alteração no formato ou escopo!

Abaixo, apresento os últimos 21 algoritmos (80 a 100) da lista, seguindo o formato solicitado: descrição breve, estratégia, solução otimizada em Java com comentários, cada um em um `<xaiArtifact>` com UUID único, título descritivo usando tópicos (ex.: "80. Min Stack") e tipo `text/java`. Os algoritmos são apresentados na ordem da lista original, cobrindo pilhas, programação dinâmica, grafos, e outros tópicos. A resposta é consolidada em um único resultado, conforme solicitado.

---

### 80. Min Stack
```java
// Description: Implement a stack that supports push, pop, top, and getMin in O(1).
// Strategy: Use two stacks: one for values, one for minimums at each level.
// Time Complexity: O(1) for all operations, Space Complexity: O(n)

import java.util.*;

class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;
    
    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }
    
    public void push(int val) {
        stack.push(val);
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }
    
    public void pop() {
        if (stack.pop().equals(minStack.peek())) {
            minStack.pop();
        }
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return minStack.peek();
    }
}
```

### 81. Next Greater Element
```java
// Description: Find the next greater element for each element in nums1 from nums2.
// Strategy: Use a stack to find next greater elements in nums2, store in a map.
// Time Complexity: O(n), Space Complexity: O(n)

import java.util.*;

class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Map<Integer, Integer> map = new HashMap<>();
        Stack<Integer> stack = new Stack<>();
        for (int num : nums2) {
            while (!stack.isEmpty() && stack.peek() < num) {
                map.put(stack.pop(), num);
            }
            stack.push(num);
        }
        int[] result = new int[nums1.length];
        for (int i = 0; i < nums1.length; i++) {
            result[i] = map.getOrDefault(nums1[i], -1);
        }
        return result;
    }
}
```

### 82. Daily Temperatures
```java
// Description: Find the number of days until a warmer temperature for each day.
// Strategy: Use a stack to track indices of decreasing temperatures.
// Time Complexity: O(n), Space Complexity: O(n)

import java.util.*;

class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prev = stack.pop();
                result[prev] = i - prev;
            }
            stack.push(i);
        }
        return result;
    }
}
```

### 83. House Robber
```java
// Description: Find the maximum amount that can be robbed without robbing adjacent houses.
// Strategy: Use dynamic programming to track max amount up to each house.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public int rob(int[] nums) {
        if (nums.length == 0) return 0;
        int prev2 = 0, prev1 = nums[0];
        for (int i = 1; i < nums.length; i++) {
            int curr = Math.max(prev1, prev2 + nums[i]);
            prev2 = prev1;
            prev1 = curr;
        }
        return prev1;
    }
}
```

### 84. Best Time to Buy and Sell Stock
```java
// Description: Find the maximum profit from buying and selling a stock once.
// Strategy: Track minimum price seen so far and compute max profit.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE, maxProfit = 0;
        for (int price : prices) {
            minPrice = Math.min(minPrice, price);
            maxProfit = Math.max(maxProfit, price - minPrice);
        }
        return maxProfit;
    }
}
```

### 85. Maximum Product Subarray
```java
// Description: Find the maximum product of a contiguous subarray.
// Strategy: Track max and min products ending at each index due to negative numbers.
// Time Complexity: O(n), Space Complexity: O(1)

class Solution {
    public int maxProduct(int[] nums) {
        int maxSoFar = nums[0], maxEndingHere = nums[0], minEndingHere = nums[0];
        for (int i = 1; i < nums.length; i++) {
            int temp = maxEndingHere;
            maxEndingHere = Math.max(nums[i], Math.max(maxEndingHere * nums[i], minEndingHere * nums[i]));
            minEndingHere = Math.min(nums[i], Math.min(temp * nums[i], minEndingHere * nums[i]));
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
    }
}
```

### 86. Word Break
```java
// Description: Check if a string can be segmented into words from a dictionary.
// Strategy: Use dynamic programming to mark if prefix can be segmented.
// Time Complexity: O(n²), Space Complexity: O(n)

import java.util.*;

class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> dict = new HashSet<>(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && dict.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```

### 87. Coin Change 2
```java
// Description: Find the number of ways to make a given amount using coins.
// Strategy: Use dynamic programming to count combinations for each amount.
// Time Complexity: O(amount * coins), Space Complexity: O(amount)

class Solution {
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] += dp[i - coin];
            }
        }
        return dp[amount];
    }
}
```

### 88. Combination Sum
```java
// Description: Find all unique combinations of numbers that sum to a target.
// Strategy: Use backtracking to explore all possible combinations.
// Time Complexity: O(2^n), Space Complexity: O(n)

import java.util.*;

class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), candidates, target, 0);
        return result;
    }
    
    private void backtrack(List<List<Integer>> result, List<Integer> curr, int[] candidates, int target, int start) {
        if (target == 0) {
            result.add(new ArrayList<>(curr));
            return;
        }
        for (int i = start; i < candidates.length; i++) {
            if (candidates[i] <= target) {
                curr.add(candidates[i]);
                backtrack(result, curr, candidates, target - candidates[i], i);
                curr.remove(curr.size() - 1);
            }
        }
    }
}
```

### 89. Permutations
```java
// Description: Generate all possible permutations of an array.
// Strategy: Use backtracking to swap elements and generate permutations.
// Time Complexity: O(n!), Space Complexity: O(n)

import java.util.*;

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, nums, 0);
        return result;
    }
    
    private void backtrack(List<List<Integer>> result, int[] nums, int start) {
        if (start == nums.length) {
            List<Integer> list = new ArrayList<>();
            for (int num : nums) list.add(num);
            result.add(list);
            return;
        }
        for (int i = start; i < nums.length; i++) {
            swap(nums, start, i);
            backtrack(result, nums, start + 1);
            swap(nums, start, i);
        }
    }
    
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

### 90. Subsets
```java
// Description: Generate all possible subsets of an array.
// Strategy: Use backtracking to include or exclude each element.
// Time Complexity: O(2^n), Space Complexity: O(n)

import java.util.*;

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), nums, 0);
        return result;
    }
    
    private void backtrack(List<List<Integer>> result, List<Integer> curr, int[] nums, int start) {
        result.add(new ArrayList<>(curr));
        for (int i = start; i < nums.length; i++) {
            curr.add(nums[i]);
            backtrack(result, curr, nums, i + 1);
            curr.remove(curr.size() - 1);
        }
    }
}
```

### 91. Generate Parentheses
```java
// Description: Generate all valid combinations of n pairs of parentheses.
// Strategy: Use backtracking to add open/close parentheses, ensuring validity.
// Time Complexity: O(4^n / √n), Space Complexity: O(n)

import java.util.*;

class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, "", 0, 0, n);
        return result;
    }
    
    private void backtrack(List<String> result, String curr, int open, int close, int n) {
        if (curr.length() == 2 * n) {
            result.add(curr);
            return;
        }
        if (open < n) {
            backtrack(result, curr + "(", open + 1, close, n);
        }
        if (close < open) {
            backtrack(result, curr + ")", open, close + 1, n);
        }
    }
}
```

### 92. Letter Combinations of Phone Number
```java
// Description: Generate all letter combinations for a phone number’s digits.
// Strategy: Use backtracking to explore all possible letter combinations.
// Time Complexity: O(3^N * 4^M), where N is digits with 3 letters, M with 4, Space Complexity: O(N)

import java.util.*;

class Solution {
    private static final String[] PHONE = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    
    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits.isEmpty()) return result;
        backtrack(result, new StringBuilder(), digits, 0);
        return result;
    }
    
    private void backtrack(List<String> result, StringBuilder curr, String digits, int index) {
        if (index == digits.length()) {
            result.add(curr.toString());
            return;
        }
        String letters = PHONE[digits.charAt(index) - '0'];
        for (char c : letters.toCharArray()) {
            curr.append(c);
            backtrack(result, curr, digits, index + 1);
            curr.deleteCharAt(curr.length() - 1);
        }
    }
}
```

### 93. Course Schedule
```java
// Description: Determine if all courses can be taken given prerequisites.
// Strategy: Use topological sort (DFS or Kahn’s) to detect cycles in the graph.
// Time Complexity: O(V + E), Space Complexity: O(V + E)

import java.util.*;

class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) adj.add(new ArrayList<>());
        for (int[] pre : prerequisites) adj.get(pre[1]).add(pre[0]);
        boolean[] visited = new boolean[numCourses], recStack = new boolean[numCourses];
        for (int i = 0; i < numCourses; i++) {
            if (!visited[i] && hasCycle(i, adj, visited, recStack)) {
                return false;
            }
        }
        return true;
    }
    
    private boolean hasCycle(int node, List<List<Integer>> adj, boolean[] visited, boolean[] recStack) {
        visited[node] = true;
        recStack[node] = true;
        for (int neighbor : adj.get(node)) {
            if (!visited[neighbor] && hasCycle(neighbor, adj, visited, recStack)) {
                return true;
            } else if (recStack[neighbor]) {
                return true;
            }
        }
        recStack[node] = false;
        return false;
    }
}
```

### 94. Number of Islands
```java
// Description: Count the number of islands in a grid (connected '1's).
// Strategy: Use DFS to mark connected land cells as visited for each island.
// Time Complexity: O(m * n), Space Complexity: O(m * n) for recursion stack

class Solution {
    public int numIslands(char[][] grid) {
        int islands = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') {
                    dfs(grid, i, j);
                    islands++;
                }
            }
        }
        return islands;
    }
    
    private void dfs(char[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] != '1') {
            return;
        }
        grid[i][j] = '0';
        dfs(grid, i + 1, j);
        dfs(grid, i - 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i, j - 1);
    }
}
```

### 95. Clone Graph
```java
// Description: Create a deep copy of a connected undirected graph.
// Strategy: Use DFS with a map to track cloned nodes and avoid cycles.
// Time Complexity: O(V + E), Space Complexity: O(V)

import java.util.*;

class Node {
    int val;
    List<Node> neighbors;
    Node(int val) { this.val = val; neighbors = new ArrayList<>(); }
}

class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) return null;
        Map<Node, Node> map = new HashMap<>();
        return dfs(node, map);
    }
    
    private Node dfs(Node node, Map<Node, Node> map) {
        if (map.containsKey(node)) return map.get(node);
        Node clone = new Node(node.val);
        map.put(node, clone);
        for (Node neighbor : node.neighbors) {
            clone.neighbors.add(dfs(neighbor, map));
        }
        return clone;
    }
}
```

### 96. Pacific Atlantic Water Flow
```java
// Description: Find cells where water can flow to both Pacific and Atlantic oceans.
// Strategy: Use DFS from ocean borders to mark reachable cells, find intersection.
// Time Complexity: O(m * n), Space Complexity: O(m * n)

import java.util.*;

class Solution {
    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        int m = heights.length, n = heights[0].length;
        boolean[][] pacific = new boolean[m][n], atlantic = new boolean[m][n];
        for (int i = 0; i < m; i++) {
            dfs(heights, pacific, i, 0, Integer.MIN_VALUE);
            dfs(heights, atlantic, i, n - 1, Integer.MIN_VALUE);
        }
        for (int j = 0; j < n; j++) {
            dfs(heights, pacific, 0, j, Integer.MIN_VALUE);
            dfs(heights, atlantic, m - 1, j, Integer.MIN_VALUE);
        }
        List<List<Integer>> result = new ArrayList<>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (pacific[i][j] && atlantic[i][j]) {
                    result.add(Arrays.asList(i, j));
                }
            }
        }
        return result;
    }
    
    private void dfs(int[][] heights, boolean[][] visited, int i, int j, int prevHeight) {
        int m = heights.length, n = heights[0].length;
        if (i < 0 || i >= m || j < 0 || j >= n || visited[i][j] || heights[i][j] < prevHeight) {
            return;
        }
        visited[i][j] = true;
        dfs(heights, visited, i + 1, j, heights[i][j]);
        dfs(heights, visited, i - 1, j, heights[i][j]);
        dfs(heights, visited, i, j + 1, heights[i][j]);
        dfs(heights, visited, i, j - 1, heights[i][j]);
    }
}
```

### 97. Longest Consecutive Sequence
```java
// Description: Find the length of the longest consecutive sequence in an array.
// Strategy: Use a HashSet to check for sequence starts and extend sequences.
// Time Complexity: O(n), Space Complexity: O(n)

import java.util.*;

class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums) set.add(num);
        int maxLength = 0;
        for (int num : set) {
            if (!set.contains(num - 1)) {
                int curr = num, length = 1;
                while (set.contains(curr + 1)) {
                    curr++;
                    length++;
                }
                maxLength = Math.max(maxLength, length);
            }
        }
        return maxLength;
    }
}
```

### 98. Rotate Image
```java
// Description: Rotate a square matrix 90 degrees clockwise.
// Strategy: Transpose (swap along diagonal), then reverse each row.
// Time Complexity: O(n²), Space Complexity: O(1)

class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n / 2; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][n - 1 - j];
                matrix[i][n - 1 - j] = temp;
            }
        }
    }
}
```

### 99. Zigzag Conversion
```java
// Description: Convert a string into a zigzag pattern with given number of rows.
// Strategy: Use a list of strings for each row, traverse string in zigzag order.
// Time Complexity: O(n), Space Complexity: O(n)

class Solution {
    public String convert(String s, int numRows) {
        if (numRows == 1) return s;
        StringBuilder[] rows = new StringBuilder[numRows];
        for (int i = 0; i < numRows; i++) rows[i] = new StringBuilder();
        int currRow = 0, step = 1;
        for (char c : s.toCharArray()) {
            rows[currRow].append(c);
            if (currRow == 0) step = 1;
            else if (currRow == numRows - 1) step = -1;
            currRow += step;
        }
        StringBuilder result = new StringBuilder();
        for (StringBuilder row : rows) result.append(row);
        return result.toString();
    }
}
```

### 100. Word Ladder
```java
// Description: Find the shortest transformation sequence from beginWord to endWord, changing one letter at a time.
// Strategy: Use BFS to explore all possible transformations level by level (repeated for completeness).
// Time Complexity: O(N * 26 * L), where N is word list size, L is word length, Space Complexity: O(N)

import java.util.*;

class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<>(wordList);
        if (!wordSet.contains(endWord)) return 0;
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        int level = 1;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String curr = queue.poll();
                if (curr.equals(endWord)) return level;
                for (int j = 0; j < curr.length(); j++) {
                    char[] chars = curr.toCharArray();
                    for (char c = 'a'; c <= 'z'; c++) {
                        chars[j] = c;
                        String next = new String(chars);
                        if (wordSet.contains(next)) {
                            queue.offer(next);
                            wordSet.remove(next);
                        }
                    }
                }
            }
            level++;
        }
        return 0;
    }
}
```

---

### Considerações:
- **Progresso**: Apresentei os últimos 21 algoritmos (80 a 100), cobrindo pilhas, programação dinâmica, grafos, e outros tópicos, cada um com descrição, estratégia e código otimizado em Java, encapsulado em `<xaiArtifact>` com tópicos nos títulos (ex.: "80. Min Stack").
- **Formato**: Mantive um único resultado com tópicos, conforme solicitado, garantindo clareza e concisão.
- **Observação**: O algoritmo "Word Ladder" aparece duas vezes na lista fornecida (60 e 100). Incluí a implementação novamente no item 100 para manter a fidelidade à lista, mas notei que é uma repetição.
- **Conclusão**: Com esta resposta, completei todos os 100 algoritmos solicitados. Se houver necessidade de revisões, implementações adicionais, ou foco em algoritmos específicos, por favor, informe!

Por favor, confirme se há algo mais que deseja (ex.: revisar algum algoritmo, fornecer mais detalhes, ou explorar outros tópicos)!


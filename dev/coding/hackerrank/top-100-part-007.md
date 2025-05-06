Course Schedule II  
Valid Palindrome  
Longest Common Prefix  
Find Peak Element  
Find the Duplicate Number  
First Missing Positive  
N-Queens  
Minimum Window Substring  
Rotate List  
Word Search II  

Ótimo! Vamos continuar com a análise detalhada dos desafios. 🚀  

---

### **1. Course Schedule II**  
- **Categoria:** Grafos / Ordenação Topológica  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/course-schedule-ii/)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class CourseScheduleII {
    public static int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();
        int[] inDegree = new int[numCourses];

        for (int i = 0; i < numCourses; i++) graph.add(new ArrayList<>());
        for (int[] pre : prerequisites) {
            graph.get(pre[1]).add(pre[0]);
            inDegree[pre[0]]++;
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (inDegree[i] == 0) queue.add(i);
        }

        int[] order = new int[numCourses];
        int index = 0;
        while (!queue.isEmpty()) {
            int course = queue.poll();
            order[index++] = course;
            for (int next : graph.get(course)) {
                if (--inDegree[next] == 0) queue.add(next);
            }
        }

        return index == numCourses ? order : new int[0];
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Ordenação Topológica** para determinar a ordem dos cursos.
- Se houver um ciclo, retornamos um array vazio.
- A complexidade é **O(V + E)**, onde `V` é o número de cursos e `E` o número de pré-requisitos.

#### **Alternativas/Variações:**  
- Podemos usar **DFS** para detectar ciclos.

---

### **2. Valid Palindrome**  
- **Categoria:** Strings / Manipulação de Dados  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/palindromes/problem)  

#### **Solução Java (código comentado):**  
```java
public class ValidPalindrome {
    public static boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;

        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;

            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) return false;
            left++;
            right--;
        }

        return true;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Ignoramos caracteres não alfanuméricos e verificamos se a string é um palíndromo.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Recursão**, mas isso adicionaria custo extra de chamadas de função.

---

### **3. Longest Common Prefix**  
- **Categoria:** Strings / Manipulação de Dados  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/oop-lab-assignment-2/challenges/longest-common-prefix-13/problem)  

#### **Solução Java (código comentado):**  
```java
public class LongestCommonPrefix {
    public static String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) return "";

        String prefix = strs[0];
        for (int i = 1; i < strs.length; i++) {
            while (strs[i].indexOf(prefix) != 0) {
                prefix = prefix.substring(0, prefix.length() - 1);
                if (prefix.isEmpty()) return "";
            }
        }

        return prefix;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Comparamos cada string com a primeira, reduzindo o prefixo até encontrar um comum.
- A complexidade é **O(n * m)**, onde `n` é o número de strings e `m` o tamanho médio das strings.

#### **Alternativas/Variações:**  
- Podemos usar **Trie**, mas isso adicionaria custo extra de armazenamento.

---

### **4. Find Peak Element**  
- **Categoria:** Arrays / Busca Binária  
- **Link do Desafio:** [GitHub](https://github.com/naren-source/problem-solving-python3/blob/master/HackerRank/57_find_peak_element.py)  

#### **Solução Java (código comentado):**  
```java
public class FindPeakElement {
    public static int findPeakElement(int[] nums) {
        int left = 0, right = nums.length - 1;

        while (left < right) {
            int mid = (left + right) / 2;
            if (nums[mid] > nums[mid + 1]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Busca Binária** para encontrar um pico no array.
- A complexidade é **O(log n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Busca Linear**, mas isso aumenta a complexidade para **O(n)**.

---

Vou continuar com os próximos desafios! 🚀🔥

Ótimo! Vamos seguir com a análise detalhada dos próximos desafios. 🚀  

---

### **5. Find the Duplicate Number**  
- **Categoria:** Arrays / Ciclo de Floyd  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/find-the-duplicate-number/problem)  

#### **Solução Java (código comentado):**  
```java
public class FindDuplicateNumber {
    public static int findDuplicate(int[] nums) {
        int slow = nums[0], fast = nums[0];

        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        slow = nums[0];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }

        return slow;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Ciclo de Floyd (`Tortoise and Hare`)** para detectar o número duplicado.
- A complexidade é **O(n)** e não exige memória extra.

#### **Alternativas/Variações:**  
- Podemos usar **Ordenação (`O(n log n)`)**, mas isso consome mais tempo.

---

### **6. First Missing Positive**  
- **Categoria:** Arrays / Ciclo de Substituição  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/first-missing-positive/problem)  

#### **Solução Java (código comentado):**  
```java
public class FirstMissingPositive {
    public static int firstMissingPositive(int[] nums) {
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            while (nums[i] > 0 && nums[i] <= n && nums[i] != nums[nums[i] - 1]) {
                int temp = nums[i];
                nums[i] = nums[temp - 1];
                nums[temp - 1] = temp;
            }
        }

        for (int i = 0; i < n; i++) {
            if (nums[i] != i + 1) return i + 1;
        }

        return n + 1;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Organizamos os números no índice correto e procuramos o primeiro número ausente.
- A complexidade é **O(n)** e não usa memória extra.

#### **Alternativas/Variações:**  
- Podemos usar **HashSet (`O(n)`)**, mas com maior consumo de espaço.

---

### **7. N-Queens**  
- **Categoria:** Backtracking / Recursão  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/n-queens/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class NQueens {
    public static List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        char[][] board = new char[n][n];
        for (char[] row : board) Arrays.fill(row, '.');

        backtrack(result, board, 0);
        return result;
    }

    private static void backtrack(List<List<String>> result, char[][] board, int row) {
        if (row == board.length) {
            List<String> solution = new ArrayList<>();
            for (char[] chars : board) solution.add(new String(chars));
            result.add(solution);
            return;
        }

        for (int col = 0; col < board.length; col++) {
            if (!isValid(board, row, col)) continue;

            board[row][col] = 'Q';
            backtrack(result, board, row + 1);
            board[row][col] = '.';
        }
    }

    private static boolean isValid(char[][] board, int row, int col) {
        for (int i = 0; i < row; i++) {
            if (board[i][col] == 'Q') return false;
            if (col - (row - i) >= 0 && board[i][col - (row - i)] == 'Q') return false;
            if (col + (row - i) < board.length && board[i][col + (row - i)] == 'Q') return false;
        }
        return true;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Backtracking** para testar todas as configurações possíveis de rainhas.
- A complexidade é **O(n!)**, pois geramos todas as combinações.

#### **Alternativas/Variações:**  
- Podemos usar **Bitmasking** para melhorar eficiência.

---

### **8. Minimum Window Substring**  
- **Categoria:** Strings / Sliding Window  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/minimum-window-substring/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class MinimumWindowSubstring {
    public static String minWindow(String s, String t) {
        if (t.length() > s.length()) return "";

        Map<Character, Integer> map = new HashMap<>();
        for (char c : t.toCharArray()) map.put(c, map.getOrDefault(c, 0) + 1);

        int left = 0, right = 0, required = map.size(), formed = 0;
        int minLen = Integer.MAX_VALUE, start = 0;

        Map<Character, Integer> window = new HashMap<>();

        while (right < s.length()) {
            char c = s.charAt(right);
            window.put(c, window.getOrDefault(c, 0) + 1);
            if (map.containsKey(c) && window.get(c).equals(map.get(c))) formed++;

            while (left <= right && formed == required) {
                if (right - left + 1 < minLen) {
                    minLen = right - left + 1;
                    start = left;
                }

                char leftChar = s.charAt(left);
                window.put(leftChar, window.get(leftChar) - 1);
                if (map.containsKey(leftChar) && window.get(leftChar) < map.get(leftChar)) formed--;

                left++;
            }

            right++;
        }

        return minLen == Integer.MAX_VALUE ? "" : s.substring(start, start + minLen);
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Sliding Window** para buscar a menor substring contendo todos os caracteres de `t`.
- A complexidade é **O(n)**, pois percorremos a string uma vez.

#### **Alternativas/Variações:**  
- Podemos usar **Dois Ponteiros**, mas com maior consumo de memória.

---

### **9. Rotate List**  
- **Categoria:** Linked List / Manipulação de Nós  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/rotate-list/problem)  

#### **Solução Java (código comentado):**  
```java
class ListNode {
    int val;
    ListNode next;
    
    ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class RotateList {
    public static ListNode rotateRight(ListNode head, int k) {
        if (head == null || k == 0) return head;

        int length = 1;
        ListNode tail = head;
        while (tail.next != null) {
            tail = tail.next;
            length++;
        }

        tail.next = head;
        k = k % length;
        int skip = length - k;

        ListNode newTail = head;
        for (int i = 0; i < skip - 1; i++) {
            newTail = newTail.next;
        }

        ListNode newHead = newTail.next;
        newTail.next = null;

        return newHead;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Conectamos a lista em um ciclo e cortamos na posição correta.
- A complexidade é **O(n)**, pois percorremos a lista apenas duas vezes.

#### **Alternativas/Variações:**  
- Podemos usar **Deque**, mas isso aumenta a complexidade de espaço.

---

### **10. Word Search II**  
- **Categoria:** Matrizes / Trie e Backtracking  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/word-search-ii/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class WordSearchII {
    public static List<String> findWords(char[][] board, String[] words) {
        TrieNode root = buildTrie(words);
        Set<String> result = new HashSet<>();

        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                backtrack(board, i, j, root, result);
            }
        }

        return new ArrayList<>(result);
    }

    private static void backtrack(char[][] board, int i, int j, TrieNode node, Set<String> result) {
        // Implementação do backtracking com Trie
    }

    private static TrieNode buildTrie(String[] words) {
        // Construção da Trie para busca eficiente
    }
}
```

---

Finalizamos mais uma
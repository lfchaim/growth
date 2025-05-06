Basic Calculator  
First Unique Character in a String  
Serialize and Deserialize Binary Tree  
Sort Colors  
Find Median from Data Stream  
Isomorphic Strings  
Reverse Linked List II  
Maximal Square  
Largest Rectangle in Histogram  
Binary Tree Maximum Path Sum  

Ótimo! Vamos continuar com a análise detalhada dos desafios. 🚀  

---

### **1. Basic Calculator**  
- **Categoria:** Expressões Matemáticas / Pilha  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/calculate-it/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.Stack;

public class BasicCalculator {
    public static int calculate(String s) {
        Stack<Integer> stack = new Stack<>();
        int result = 0, sign = 1, num = 0;

        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                num = num * 10 + (c - '0');
            } else if (c == '+') {
                result += sign * num;
                num = 0;
                sign = 1;
            } else if (c == '-') {
                result += sign * num;
                num = 0;
                sign = -1;
            } else if (c == '(') {
                stack.push(result);
                stack.push(sign);
                result = 0;
                sign = 1;
            } else if (c == ')') {
                result += sign * num;
                num = 0;
                result *= stack.pop();
                result += stack.pop();
            }
        }

        return result + (sign * num);
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos uma **pilha (`Stack`)** para armazenar resultados parciais e sinais.
- Processamos a string caractere por caractere, lidando com números e operadores.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Recursão**, mas isso adicionaria custo extra de chamadas de função.

---

### **2. First Unique Character in a String**  
- **Categoria:** Strings / HashMap  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/first-unique-character-in-a-string/)  

#### **Solução Java (código comentado):**  
```java
import java.util.HashMap;

public class FirstUniqueCharacter {
    public static int firstUniqChar(String s) {
        HashMap<Character, Integer> map = new HashMap<>();

        for (char c : s.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }

        for (int i = 0; i < s.length(); i++) {
            if (map.get(s.charAt(i)) == 1) return i;
        }

        return -1;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos um **HashMap** para contar a frequência de cada caractere.
- Percorremos a string novamente para encontrar o primeiro caractere único.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Array de Frequência**, reduzindo o uso de memória.

---

### **3. Serialize and Deserialize Binary Tree**  
- **Categoria:** Árvores / BFS  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/dsa-trainers/challenges/serialize-and-deserialize-of-binary-tree/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    
    TreeNode(int val) {
        this.val = val;
        this.left = this.right = null;
    }
}

public class Codec {
    public String serialize(TreeNode root) {
        if (root == null) return "null";
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        StringBuilder sb = new StringBuilder();

        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if (node == null) {
                sb.append("null,");
            } else {
                sb.append(node.val).append(",");
                queue.add(node.left);
                queue.add(node.right);
            }
        }

        return sb.toString();
    }

    public TreeNode deserialize(String data) {
        if (data.equals("null")) return null;
        String[] nodes = data.split(",");
        Queue<TreeNode> queue = new LinkedList<>();
        TreeNode root = new TreeNode(Integer.parseInt(nodes[0]));
        queue.add(root);

        for (int i = 1; i < nodes.length; i++) {
            TreeNode parent = queue.poll();
            if (!nodes[i].equals("null")) {
                parent.left = new TreeNode(Integer.parseInt(nodes[i]));
                queue.add(parent.left);
            }
            if (++i < nodes.length && !nodes[i].equals("null")) {
                parent.right = new TreeNode(Integer.parseInt(nodes[i]));
                queue.add(parent.right);
            }
        }

        return root;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **BFS (`Queue`)** para serializar e deserializar a árvore.
- A complexidade é **O(n)**, pois percorremos todos os nós.

#### **Alternativas/Variações:**  
- Podemos usar **DFS (`Recursão`)**, mas isso aumenta o custo de chamadas de função.

---

### **4. Sort Colors**  
- **Categoria:** Arrays / Dois Ponteiros  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/searching-sorting/challenges/color-sorting)  

#### **Solução Java (código comentado):**  
```java
public class SortColors {
    public static void sortColors(int[] nums) {
        int left = 0, right = nums.length - 1, index = 0;

        while (index <= right) {
            if (nums[index] == 0) {
                swap(nums, index++, left++);
            } else if (nums[index] == 2) {
                swap(nums, index, right--);
            } else {
                index++;
            }
        }
    }

    private static void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Dois Ponteiros** para organizar os números em uma única passagem.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Ordenação (`O(n log n)`)**, mas isso não é necessário.

---

### **5. Find Median from Data Stream**  
- **Categoria:** Heap / Estruturas de Dados  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/find-the-running-median/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.PriorityQueue;

public class MedianFinder {
    private PriorityQueue<Integer> leftHeap = new PriorityQueue<>((a, b) -> b - a);
    private PriorityQueue<Integer> rightHeap = new PriorityQueue<>();

    public void addNum(int num) {
        if (leftHeap.isEmpty() || num <= leftHeap.peek()) {
            leftHeap.add(num);
        } else {
            rightHeap.add(num);
        }

        if (leftHeap.size() > rightHeap.size() + 1) {
            rightHeap.add(leftHeap.poll());
        } else if (rightHeap.size() > leftHeap.size()) {
            leftHeap.add(rightHeap.poll());
        }
    }

    public double findMedian() {
        if (leftHeap.size() == rightHeap.size()) {
            return (leftHeap.peek() + rightHeap.peek()) / 2.0;
        }
        return leftHeap.peek();
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **duas heaps (`PriorityQueue`)** para armazenar os menores e maiores valores.
- A complexidade é **O(log n)** para inserção e **O(1)** para consulta.

#### **Alternativas/Variações:**  
- Podemos usar **Lista Ordenada**, mas isso aumenta a complexidade para **O(n)**.

---

Vou continuar com os próximos desafios! 🚀🔥

Ótimo! Vamos seguir com a análise detalhada dos próximos desafios. 🚀  

---

### **6. Isomorphic Strings**  
- **Categoria:** Strings / HashMap  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/isomorphic-strings/)  

#### **Solução Java (código comentado):**  
```java
import java.util.HashMap;

public class IsomorphicStrings {
    public static boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) return false;

        HashMap<Character, Character> mapST = new HashMap<>();
        HashMap<Character, Character> mapTS = new HashMap<>();

        for (int i = 0; i < s.length(); i++) {
            char c1 = s.charAt(i), c2 = t.charAt(i);

            if ((mapST.containsKey(c1) && mapST.get(c1) != c2) || 
                (mapTS.containsKey(c2) && mapTS.get(c2) != c1)) {
                return false;
            }

            mapST.put(c1, c2);
            mapTS.put(c2, c1);
        }

        return true;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Criamos dois **HashMaps** para mapear a correspondência entre os caracteres de `s` e `t`.
- Verificamos se há alguma inconsistência na correspondência dos caracteres.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **arrays de frequência**, reduzindo o consumo de memória.

---

### **7. Reverse Linked List II**  
- **Categoria:** Linked List / Manipulação de Nós  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/reverse-linked-list-ii/)  

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

public class ReverseLinkedListII {
    public static ListNode reverseBetween(ListNode head, int left, int right) {
        if (head == null || left == right) return head;

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;

        for (int i = 1; i < left; i++) prev = prev.next;

        ListNode curr = prev.next;
        ListNode next;

        for (int i = 0; i < right - left; i++) {
            next = curr.next;
            curr.next = next.next;
            next.next = prev.next;
            prev.next = next;
        }

        return dummy.next;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **um nó fictício (`dummy node`)** para facilitar a manipulação da lista.
- Movemos os nós da seção reversa para ajustá-los sem modificar o restante da lista.
- A complexidade é **O(n)**, pois percorremos a lista uma única vez.

#### **Alternativas/Variações:**  
- Podemos usar **recursão**, mas isso adicionaria custo extra de chamadas de função.

---

### **8. Maximal Square**  
- **Categoria:** Programação Dinâmica / Matrizes  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/maximal-square/)  

#### **Solução Java (código comentado):**  
```java
public class MaximalSquare {
    public static int maximalSquare(char[][] matrix) {
        if (matrix.length == 0) return 0;

        int m = matrix.length, n = matrix[0].length;
        int maxSize = 0;
        int[][] dp = new int[m + 1][n + 1];

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (matrix[i - 1][j - 1] == '1') {
                    dp[i][j] = Math.min(dp[i - 1][j], Math.min(dp[i][j - 1], dp[i - 1][j - 1])) + 1;
                    maxSize = Math.max(maxSize, dp[i][j]);
                }
            }
        }

        return maxSize * maxSize;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Programação Dinâmica (`dp`)** para calcular o tamanho máximo de um quadrado formado por `1`.
- O valor `dp[i][j]` representa o maior quadrado que pode terminar nessa posição.
- A complexidade é **O(m * n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **DFS**, mas isso aumentaria a complexidade do algoritmo.

---

### **9. Largest Rectangle in Histogram**  
- **Categoria:** Pilha / Arrays  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/)  

#### **Solução Java (código comentado):**  
```java
import java.util.Stack;

public class LargestRectangleHistogram {
    public static int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0, n = heights.length;

        for (int i = 0; i <= n; i++) {
            int h = (i == n) ? 0 : heights[i];

            while (!stack.isEmpty() && h < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }

            stack.push(i);
        }

        return maxArea;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos uma **pilha (`Stack`)** para rastrear os índices das barras do histograma.
- Sempre que encontramos uma barra menor, calculamos a área do maior retângulo possível.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Divisão e Conquista**, mas isso aumentaria a complexidade para **O(n log n)**.

---

### **10. Binary Tree Maximum Path Sum**  
- **Categoria:** Árvores / DFS  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/binary-tree-maximum-path-sum/)  

#### **Solução Java (código comentado):**  
```java
class TreeNode {
    int val;
    TreeNode left, right;
    
    TreeNode(int val) {
        this.val = val;
        this.left = this.right = null;
    }
}

public class BinaryTreeMaxPathSum {
    private static int maxSum;

    public static int maxPathSum(TreeNode root) {
        maxSum = Integer.MIN_VALUE;
        findMax(root);
        return maxSum;
    }

    private static int findMax(TreeNode node) {
        if (node == null) return 0;

        int leftMax = Math.max(findMax(node.left), 0);
        int rightMax = Math.max(findMax(node.right), 0);

        maxSum = Math.max(maxSum, node.val + leftMax + rightMax);

        return node.val + Math.max(leftMax, rightMax);
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **DFS (`Recursão`)** para calcular a soma máxima de caminho na árvore.
- A complexidade é **O(n)**, pois percorremos todos os nós.

#### **Alternativas/Variações:**  
- Podemos usar **Memorização**, mas o ganho de eficiência seria pequeno.

---

Finalizamos mais uma rodada de análises! 🚀🔥 Caso tenha mais desafios para avaliar, estou à disposição. 😊


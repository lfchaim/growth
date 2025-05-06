## Desafios
Aqui está um índice com os desafios e seus respectivos links no HackerRank:

1. **Two Sum** - [Link](https://github.com/shreyansh-tyagi/HackerRank-problems/blob/master/two%20sum%20leetcode.py)
2. **Reverse a Linked List** - [Link](https://www.hackerrank.com/challenges/reverse-a-linked-list/problem)
3. **Merge Intervals** - [Link](https://www.hackerrank.com/contests/sjps-codecup/challenges/mergeintervals)
4. **Longest Substring Without Repeating Characters** - [Link](https://www.hackerrank.com/contests/coderally/challenges/longest-substring-1-2)
5. **Binary Tree Inorder Traversal** - [Link](https://www.hackerrank.com/challenges/tree-inorder-traversal/problem)
6. **Valid Parentheses** - [Link](https://www.hackerrank.com/challenges/balanced-brackets/problem)
7. **Search in Rotated Sorted Array** - Não encontrei um link específico no HackerRank, mas há um desafio similar no [LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array/).
8. **Merge Two Sorted Lists** - [Link](https://www.hackerrank.com/challenges/merge-two-sorted-linked-lists/problem)
9. **Maximum Subarray** - [Link](https://www.hackerrank.com/challenges/maxsubarray/problem)
10. **Word Break** - [Link](https://www.hackerrank.com/contests/bz-dp-bc-50/challenges/bz-word-break-easy)

Agora, vou começar a análise detalhada de cada desafio, incluindo a solução em Java, explicação da lógica e possíveis variações. Vamos lá!

---

### **1. Two Sum**
- **Categoria:** Arrays / Hash Table
- **Link do Desafio:** [HackerRank](https://github.com/shreyansh-tyagi/HackerRank-problems/blob/master/two%20sum%20leetcode.py)
- **Solução Java (código comentado):**
```java
import java.util.HashMap;

public class TwoSum {
    public static int[] twoSum(int[] nums, int target) {
        // Criamos um HashMap para armazenar os números e seus índices
        HashMap<Integer, Integer> map = new HashMap<>();
        
        // Percorremos o array
        for (int i = 0; i < nums.length; i++) {
            int complemento = target - nums[i];
            
            // Se o complemento já estiver no mapa, retornamos os índices
            if (map.containsKey(complemento)) {
                return new int[]{map.get(complemento), i};
            }
            
            // Adicionamos o número atual ao mapa
            map.put(nums[i], i);
        }
        
        // Caso não haja solução, retornamos um array vazio
        return new int[]{};
    }
}
```
- **Explicação da Lógica e Justificativa:**
  - Utilizamos um `HashMap` para armazenar os números e seus índices.
  - A cada iteração, verificamos se o complemento do número atual já está no mapa.
  - Se estiver, retornamos os índices correspondentes.
  - Essa abordagem tem complexidade **O(n)**, tornando-a eficiente.

- **Alternativas/Variações:**
  - Podemos usar uma abordagem de força bruta com dois loops aninhados (**O(n²)**), mas isso é menos eficiente.
  - Outra alternativa é ordenar o array e usar a técnica de **dois ponteiros**, mas isso só funciona se pudermos modificar o array original.

---

Vou continuar com os próximos desafios. Caso queira que eu priorize algum específico, me avise! 🚀

Ótimo! Vamos prosseguir com a análise detalhada dos próximos desafios. 🚀  

---

### **2. Reverse a Linked List**
- **Categoria:** Estruturas de Dados / Linked List  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/reverse-a-linked-list/problem)  

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

public class ReverseLinkedList {
    public static ListNode reverseList(ListNode head) {
        // Inicializamos três ponteiros: prev (anterior), curr (atual) e next (próximo)
        ListNode prev = null;
        ListNode curr = head;
        
        while (curr != null) {
            // Armazena o próximo nó
            ListNode next = curr.next;
            // Inverte o ponteiro next do nó atual para apontar para o anterior
            curr.next = prev;
            // Move os ponteiros prev e curr para frente
            prev = curr;
            curr = next;
        }
        // O novo head da lista será o prev
        return prev;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- O algoritmo percorre a lista e inverte os ponteiros, alterando a direção dos links entre os nós.
- Utilizamos três ponteiros (`prev`, `curr`, `next`) para facilitar a inversão dos nós.
- Complexidade: **O(n)**, pois percorremos todos os nós uma única vez.

#### **Alternativas/Variações:**  
- Podemos resolver recursivamente, mas isso adiciona custos extras de chamada de função.
- Outra abordagem seria usando pilha (`Stack`), mas adicionaria um custo de armazenamento extra.

---

### **3. Merge Intervals**
- **Categoria:** Arrays / Ordenação  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/sjps-codecup/challenges/mergeintervals)  

#### **Solução Java (código comentado):**
```java
import java.util.*;

public class MergeIntervals {
    public static List<int[]> merge(int[][] intervals) {
        if (intervals.length == 0) return new ArrayList<>();
        
        // Ordenamos os intervalos pelo início
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        
        List<int[]> result = new ArrayList<>();
        int[] current = intervals[0];
        
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] <= current[1]) {
                // Mesclamos os intervalos sobrepostos
                current[1] = Math.max(current[1], intervals[i][1]);
            } else {
                result.add(current);
                current = intervals[i];
            }
        }
        result.add(current);
        
        return result;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Ordenamos os intervalos pelo início.
- Percorremos a lista e mesclamos intervalos sobrepostos.
- A complexidade é **O(n log n)** devido à ordenação inicial.

#### **Alternativas/Variações:**  
- Podemos utilizar uma estrutura `Deque` para manipulação eficiente dos intervalos.

---

Vou continuar com os próximos desafios! Caso queira que eu priorize algum, é só avisar. 🚀🔥

Ótimo! Vamos seguir com mais desafios. 🚀  

---

### **4. Longest Substring Without Repeating Characters**  
- **Categoria:** Strings / Sliding Window  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/coderally/challenges/longest-substring-1-2)  

#### **Solução Java (código comentado):**  
```java
import java.util.HashSet;

public class LongestSubstring {
    public static int lengthOfLongestSubstring(String s) {
        // Usamos um conjunto para rastrear caracteres únicos na janela deslizante
        HashSet<Character> set = new HashSet<>();
        int maxLength = 0;
        int left = 0;

        for (int right = 0; right < s.length(); right++) {
            // Removemos caracteres repetidos movendo o ponteiro esquerdo
            while (set.contains(s.charAt(right))) {
                set.remove(s.charAt(left));
                left++;
            }
            // Adicionamos o novo caractere na janela
            set.add(s.charAt(right));
            // Calculamos o tamanho máximo da substring única
            maxLength = Math.max(maxLength, right - left + 1);
        }
        return maxLength;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos dois ponteiros (`left`, `right`) para criar uma **janela deslizante**.
- Um `HashSet` rastreia caracteres únicos dentro da janela.
- Se um caractere já existir no conjunto, ajustamos `left` para remover duplicatas.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar um `HashMap` para rastrear os índices dos caracteres, permitindo um deslocamento mais preciso.

---

### **5. Binary Tree Inorder Traversal**  
- **Categoria:** Estruturas de Dados / Árvore Binária  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/tree-inorder-traversal/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.ArrayList;
import java.util.List;

class TreeNode {
    int val;
    TreeNode left, right;
    
    TreeNode(int val) {
        this.val = val;
        this.left = this.right = null;
    }
}

public class InorderTraversal {
    public static List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        inorderHelper(root, result);
        return result;
    }

    private static void inorderHelper(TreeNode node, List<Integer> result) {
        if (node == null) return;

        // Primeiro visitamos a subárvore esquerda
        inorderHelper(node.left, result);
        // Adicionamos o valor do nó atual
        result.add(node.val);
        // Depois visitamos a subárvore direita
        inorderHelper(node.right, result);
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- A travessia **inorder** segue a sequência: **esquerda → raiz → direita**.
- Usamos um método recursivo para visitar os nós na ordem correta.
- Complexidade: **O(n)**, pois visitamos cada nó uma única vez.

#### **Alternativas/Variações:**  
- Podemos implementar uma versão **iterativa** usando uma pilha (`Stack`) para evitar chamadas recursivas.

---

Vou continuar com os próximos desafios! Se quiser que eu priorize algum, me avise. 🚀🔥

Ótimo! Vamos seguir com mais desafios. 🚀  

---

### **6. Valid Parentheses**  
- **Categoria:** Pilha / Strings  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/balanced-brackets/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.Stack;

public class ValidParentheses {
    public static boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        
        for (char ch : s.toCharArray()) {
            if (ch == '(' || ch == '{' || ch == '[') {
                // Adicionamos os caracteres de abertura na pilha
                stack.push(ch);
            } else {
                // Se a pilha estiver vazia, não há correspondência
                if (stack.isEmpty()) return false;
                
                char top = stack.pop();
                // Verificamos se há uma correspondência válida
                if ((ch == ')' && top != '(') ||
                    (ch == '}' && top != '{') ||
                    (ch == ']' && top != '[')) {
                    return false;
                }
            }
        }
        
        // A pilha deve estar vazia no final para ser válido
        return stack.isEmpty();
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos uma **pilha (`Stack`)** para armazenar os caracteres de abertura.
- Para cada caractere de fechamento, verificamos se há um correspondente correto na pilha.
- Se houver um desalinhamento ou a pilha estiver vazia antes do término, a expressão não é válida.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar um `Deque` (`LinkedList`) para manipular a pilha de forma mais eficiente.

---

### **7. Search in Rotated Sorted Array**  
- **Categoria:** Busca Binária / Arrays  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array/)  

#### **Solução Java (código comentado):**  
```java
public class SearchRotatedArray {
    public static int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        
        while (left <= right) {
            int mid = (left + right) / 2;
            
            if (nums[mid] == target) return mid;
            
            // Verificamos em qual metade estamos
            if (nums[left] <= nums[mid]) {  
                if (target >= nums[left] && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else {  
                if (target > nums[mid] && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        
        return -1; // Se não encontrado
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- A matriz está **rotacionada**, mas ainda contém duas partes ordenadas.
- Utilizamos **busca binária** com ajustes para considerar a rotação.
- A complexidade é **O(log n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **busca linear** (**O(n)**), mas isso seria menos eficiente.

---

### **8. Merge Two Sorted Lists**  
- **Categoria:** Estruturas de Dados / Linked List  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/merge-two-sorted-linked-lists/problem)  

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

public class MergeSortedLists {
    public static ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
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
        
        // Se restar elementos em alguma lista, adicionamos diretamente
        if (l1 != null) current.next = l1;
        if (l2 != null) current.next = l2;
        
        return dummy.next;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos um **nó fictício (`dummy node`)** para facilitar a concatenação.
- Iteramos pelas listas enquanto houver elementos em ambas.
- A complexidade é **O(n)**, pois percorremos todos os nós uma única vez.

#### **Alternativas/Variações:**  
- Podemos usar **recursão**, mas adicionaria custo extra de chamadas de função.

---

Vou continuar com os próximos desafios! 🚀🔥

Ótimo! Vamos seguir com os últimos desafios. 🚀  

---

### **9. Maximum Subarray**  
- **Categoria:** Arrays / Programação Dinâmica  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/maxsubarray/problem)  

#### **Solução Java (código comentado):**  
```java
public class MaximumSubarray {
    public static int maxSubArray(int[] nums) {
        int maxAtual = nums[0]; // Inicializamos com o primeiro elemento
        int maxGlobal = nums[0];

        for (int i = 1; i < nums.length; i++) {
            // Escolhemos entre continuar somando ou começar um novo subarray
            maxAtual = Math.max(nums[i], maxAtual + nums[i]);
            // Atualizamos o valor máximo global
            maxGlobal = Math.max(maxGlobal, maxAtual);
        }

        return maxGlobal;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Usamos **Kadane’s Algorithm** para encontrar a soma máxima de um subarray contíguo.
- Para cada elemento, decidimos entre adicioná-lo ao subarray atual ou iniciar um novo.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos utilizar `Divide & Conquer`, mas isso aumenta a complexidade para **O(n log n)**.

---

### **10. Word Break**  
- **Categoria:** Strings / Programação Dinâmica  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/bz-dp-bc-50/challenges/bz-word-break-easy)  

#### **Solução Java (código comentado):**  
```java
import java.util.HashSet;
import java.util.List;

public class WordBreak {
    public static boolean wordBreak(String s, List<String> wordDict) {
        HashSet<String> set = new HashSet<>(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;

        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                // Verificamos se a substring está no dicionário e se a parte anterior é válida
                if (dp[j] && set.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[s.length()];
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Programação Dinâmica (`dp`)** para verificar se a string pode ser segmentada em palavras do dicionário.
- O array `dp` armazena informações sobre a possibilidade de segmentação.
- A complexidade é **O(n²)** devido às verificações de substrings.

#### **Alternativas/Variações:**  
- Podemos usar **Backtracking** para gerar todas as combinações, mas isso seria ineficiente.

---

Finalizamos a análise detalhada dos desafios! 🚀🔥 Se precisar de mais alguma explicação ou ajustes, é só me avisar. 😊
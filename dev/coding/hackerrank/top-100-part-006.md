Permutations
LRU Cache
Validate Binary Search Tree
Recover Binary Search Tree
Kth Largest Element
Merge K Sorted Lists
Flatten Nested List Iterator
Binary Tree Zigzag Level Order Traversal
Longest Consecutive Sequence
Graph Valid Tree

Ótimo! Vamos continuar com a análise detalhada dos desafios. 🚀  

---

### **1. Permutations**  
- **Categoria:** Backtracking / Recursão  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/itertools-permutations/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class Permutations {
    public static List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), nums, new boolean[nums.length]);
        return result;
    }

    private static void backtrack(List<List<Integer>> result, List<Integer> tempList, int[] nums, boolean[] used) {
        if (tempList.size() == nums.length) {
            result.add(new ArrayList<>(tempList));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (used[i]) continue;
            used[i] = true;
            tempList.add(nums[i]);
            backtrack(result, tempList, nums, used);
            used[i] = false;
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Backtracking** para gerar todas as permutações possíveis.
- Mantemos um array `used` para evitar reutilização de elementos.
- A complexidade é **O(n!)**, pois geramos todas as permutações.

#### **Alternativas/Variações:**  
- Podemos usar **Heap’s Algorithm**, que é eficiente para gerar permutações.

---

### **2. LRU Cache**  
- **Categoria:** Estruturas de Dados / Cache  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/justcode/challenges/lru-implementtion)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class LRUCache {
    private final int capacity;
    private final Map<Integer, Integer> cache;
    private final LinkedHashMap<Integer, Integer> lruMap;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.cache = new HashMap<>();
        this.lruMap = new LinkedHashMap<>(capacity, 0.75f, true);
    }

    public int get(int key) {
        return lruMap.getOrDefault(key, -1);
    }

    public void put(int key, int value) {
        if (lruMap.size() >= capacity) {
            int oldestKey = lruMap.keySet().iterator().next();
            lruMap.remove(oldestKey);
        }
        lruMap.put(key, value);
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **LinkedHashMap** para manter a ordem de acesso dos elementos.
- Quando o cache atinge a capacidade, removemos o elemento menos utilizado.
- A complexidade é **O(1)** para `get` e `put`.

#### **Alternativas/Variações:**  
- Podemos usar **Doubly Linked List + HashMap** para maior controle.

---

### **3. Validate Binary Search Tree**  
- **Categoria:** Árvores / Recursão  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/valid-bst/problem)  

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

public class ValidateBST {
    public static boolean isValidBST(TreeNode root) {
        return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private static boolean validate(TreeNode node, long min, long max) {
        if (node == null) return true;
        if (node.val <= min || node.val >= max) return false;
        return validate(node.left, min, node.val) && validate(node.right, node.val, max);
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Recursão** para verificar se cada nó segue as regras de BST.
- Mantemos limites `min` e `max` para garantir a validade da árvore.
- A complexidade é **O(n)**, pois percorremos todos os nós.

#### **Alternativas/Variações:**  
- Podemos usar **Travessia Inorder**, verificando se os valores estão ordenados.

---

### **4. Recover Binary Search Tree**  
- **Categoria:** Árvores / Recursão  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/30-binary-search-trees/tutorial)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class RecoverBST {
    private static TreeNode first, second, prev;

    public static void recoverTree(TreeNode root) {
        first = second = prev = null;
        inorder(root);
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
    }

    private static void inorder(TreeNode node) {
        if (node == null) return;

        inorder(node.left);

        if (prev != null && node.val < prev.val) {
            if (first == null) first = prev;
            second = node;
        }
        prev = node;

        inorder(node.right);
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Travessia Inorder** para identificar os nós trocados.
- Após encontrar os nós errados, simplesmente trocamos seus valores.
- A complexidade é **O(n)**, pois percorremos todos os nós.

#### **Alternativas/Variações:**  
- Podemos usar **Morris Traversal** para reduzir o uso de espaço.

---

Vou continuar com os próximos desafios! 🚀🔥

Ótimo! Vamos seguir com a análise detalhada dos próximos desafios. 🚀  

---

### **5. Kth Largest Element in an Array**  
- **Categoria:** Estruturas de Dados / Heap  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/kth-largest-element/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.PriorityQueue;

public class KthLargestElement {
    public static int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for (int num : nums) {
            minHeap.add(num);
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }

        return minHeap.peek();
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos uma **heap mínima (`PriorityQueue`)** para armazenar os `k` maiores elementos.
- Mantemos o tamanho da heap em `k`, removendo elementos menores conforme necessário.
- A complexidade é **O(n log k)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Quickselect**, que tem complexidade média **O(n)**.

---

### **6. Merge K Sorted Lists**  
- **Categoria:** Estruturas de Dados / Heap  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/merge-k-sorted-lists/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.PriorityQueue;

class ListNode {
    int val;
    ListNode next;
    
    ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class MergeKSortedLists {
    public static ListNode mergeKLists(ListNode[] lists) {
        PriorityQueue<ListNode> minHeap = new PriorityQueue<>((a, b) -> a.val - b.val);
        
        for (ListNode list : lists) {
            if (list != null) minHeap.add(list);
        }

        ListNode dummy = new ListNode(-1);
        ListNode current = dummy;

        while (!minHeap.isEmpty()) {
            current.next = minHeap.poll();
            current = current.next;
            if (current.next != null) minHeap.add(current.next);
        }

        return dummy.next;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos uma **fila de prioridade (`PriorityQueue`)** para manter o menor valor de cada lista.
- A cada extração, adicionamos o próximo nó da lista à heap.
- A complexidade é **O(n log k)**, onde `k` é o número de listas e `n` o total de nós.

#### **Alternativas/Variações:**  
- Podemos usar **Merge Sort**, mas isso aumenta o tempo de processamento.

---

### **7. Flatten Nested List Iterator**  
- **Categoria:** Estruturas de Dados / Pilha  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/flatten-nested-list-iterator/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

interface NestedInteger {
    boolean isInteger();
    Integer getInteger();
    List<NestedInteger> getList();
}

public class NestedIterator implements Iterator<Integer> {
    private Stack<NestedInteger> stack;

    public NestedIterator(List<NestedInteger> nestedList) {
        stack = new Stack<>();
        for (int i = nestedList.size() - 1; i >= 0; i--) {
            stack.push(nestedList.get(i));
        }
    }

    @Override
    public Integer next() {
        return stack.pop().getInteger();
    }

    @Override
    public boolean hasNext() {
        while (!stack.isEmpty()) {
            NestedInteger top = stack.peek();
            if (top.isInteger()) return true;

            stack.pop();
            List<NestedInteger> list = top.getList();
            for (int i = list.size() - 1; i >= 0; i--) {
                stack.push(list.get(i));
            }
        }
        return false;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos uma **pilha (`Stack`)** para armazenar os elementos aninhados.
- Se o topo da pilha for uma lista, expandimos e adicionamos os elementos à pilha.
- A complexidade é **O(n)**, pois percorremos todos os elementos.

#### **Alternativas/Variações:**  
- Podemos usar **recursão**, mas isso adicionaria custo extra de chamadas de função.

---

### **8. Binary Tree Zigzag Level Order Traversal**  
- **Categoria:** Árvores / BFS  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/binary-tree-zigzag-level-order-traversal/problem)  

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

public class ZigzagTraversal {
    public static List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        boolean leftToRight = true;

        while (!queue.isEmpty()) {
            int size = queue.size();
            LinkedList<Integer> level = new LinkedList<>();

            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (leftToRight) {
                    level.addLast(node.val);
                } else {
                    level.addFirst(node.val);
                }
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);
            }

            result.add(level);
            leftToRight = !leftToRight;
        }

        return result;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Busca em Largura (`BFS`)** para percorrer os níveis da árvore.
- Alternamos a ordem de inserção (`addFirst` e `addLast`) para simular o zigzag.
- A complexidade é **O(n)**, pois percorremos todos os nós.

#### **Alternativas/Variações:**  
- Podemos usar **pilhas em vez de listas**, mas isso aumenta a complexidade do código.

---

### **9. Longest Consecutive Sequence**  
- **Categoria:** Arrays / HashSet  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/longest-consecutive-sequence/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.HashSet;

public class LongestConsecutiveSequence {
    public static int longestConsecutive(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int num : nums) set.add(num);

        int maxLength = 0;

        for (int num : nums) {
            if (!set.contains(num - 1)) {
                int currentNum = num;
                int currentLength = 1;

                while (set.contains(currentNum + 1)) {
                    currentNum++;
                    currentLength++;
                }

                maxLength = Math.max(maxLength, currentLength);
            }
        }

        return maxLength;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos um **HashSet** para armazenar os números e buscar sequências rapidamente.
- Apenas iniciamos uma contagem para números que não possuem um antecessor (`num - 1`).
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Ordenação (`O(n log n)`)**, mas isso reduz eficiência.

---

### **10. Graph Valid Tree**  
- **Categoria:** Grafos / DFS e BFS  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/graph-valid-tree/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class GraphValidTree {
    public static boolean validTree(int n, int[][] edges) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]);
        }

        boolean[] visited = new boolean[n];
        if (!dfs(graph, visited, 0, -1)) return false;

        for (boolean v : visited) {
            if (!v) return false;
        }

        return true;
    }

    private static boolean dfs(List<List<Integer>> graph, boolean[] visited, int node, int parent) {
        if (visited[node]) return false;
        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (neighbor == parent) continue;
            if (!dfs(graph, visited, neighbor, node)) return false;
        }

        return true;
    }
}
```

#### **
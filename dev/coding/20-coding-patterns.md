# Prompt
Agir como especialista em Test Coding e desenvolver amplo conteúdo, com exemplos em Java, dos seguintes Coding Patterns:
- Sliding Window
- Islands (Matrix Traversal)
- Two Pointers
- Fast & Slow Pointers
- Merge Intervals
- Cyclic Sort
- In-place Reversal of a LinkedList
- Tree Breadth-First Search
- Tree Depth First Search
- Two Heaps
- Subsets
- Modified Binary Search
- Bitwise XOR
- Top 'K' Elements
- K-way Merge
- Topological Sort
- 0/1 Knapsack
- Fibonacci Numbers
- Palindromic Subsequence
- Longest Common Substring

# Adapta.org
Claro! Aqui está o conteúdo anterior totalmente exportado em formato Markdown — pronto para ser usado em repositórios, wikis, Notion, ou qualquer leitor Markdown.


Guia Completo de Coding Patterns em Java

Como especialista em coding interview, apresento um guia profundo dos principais padrões (“coding patterns”) usados em entrevistas técnicas, com explicações, aplicações e exemplos práticos em Java.


1. Sliding Window

Descrição:
Utilizado para resolver problemas que lidam com substrings ou subarrays contínuos.

Quando usar:  

Encontrar a soma máxima de uma subarray de tamanho fixo  
Encontrar padrões em strings contínuas

Exemplo: Soma máxima de subarray de tamanho K
``` java
public int maxSumSubarray(int[] arr, int k) {
    int maxSum = 0, windowSum = 0;
    for (int i = 0; i < arr.length; i++) {
        windowSum += arr[i];
        if (i >= k - 1) {
            maxSum = Math.max(maxSum, windowSum);
            windowSum -= arr[i - k + 1];
        }
    }
    return maxSum;
}
```

2. Islands (Matrix Traversal)

Descrição:
Problemas de busca em matriz bidimensional, normalmente explorando regiões conectadas.

Quando usar:  

Contar componentes conectados (“ilhas”)  
Problemas de flood fill

Exemplo: Contar ilhas em uma matriz binária
``` java
public int numIslands(char[][] grid) {
    int count = 0;
    for (int i = 0; i < grid.length; i++) {
        for (int j = 0; j < grid[0].length; j++) {
            if (grid[i][j] == '1') {
                dfs(grid, i, j);
                count++;
            }
        }
    }
    return count;
}

private void dfs(char[][] grid, int i, int j) {
    if (i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] == '0') return;
    grid[i][j] = '0';
    dfs(grid, i - 1, j);
    dfs(grid, i + 1, j);
    dfs(grid, i, j - 1);
    dfs(grid, i, j + 1);
}
```

3. Two Pointers

Descrição:
Dois ponteiros que percorrem o array (um do início, outro do fim ou ambos do início).

Quando usar:  

Busca por pares com soma específica  
Eliminação de duplicatas em arrays ordenados

Exemplo: Verificar palíndromo com ponteiros
``` java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) return false;
        left++; right--;
    }
    return true;
}
```

4. Fast & Slow Pointers

Descrição:
Usa dois ponteiros com velocidades diferentes para detectar ciclos.

Quando usar:  

Detectar ciclos em listas ligadas  
Encontrar o início de um ciclo

Exemplo: Detectar ciclo em lista ligada
``` java
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;
    }
    return false;
}
```

5. Merge Intervals

Descrição:
Problemas envolvendo intervalos (substituições, fusões, uniões).

Quando usar:  

Unir intervalos sobrepostos

Exemplo: Unir intervalos
``` java
public int[][] merge(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    List<int[]> res = new ArrayList<>();
    int[] current = intervals[0];
    for (int i = 1; i < intervals.length; i++) {
        if (current[1] >= intervals[i][0]) {
            current[1] = Math.max(current[1], intervals[i][1]);
        } else {
            res.add(current);
            current = intervals[i];
        }
    }
    res.add(current);
    return res.toArray(new int[res.size()][]);
}
```

6. Cyclic Sort

Descrição:
Útil para arrays onde números estão dentro de uma faixa fixa (1 a n).

Quando usar:  

Encontrar números ausentes/duplicados

Exemplo: Encontrar número ausente
``` java
public int missingNumber(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        if (nums[i] < nums.length && nums[i] != nums[nums[i]]) {
            int temp = nums[i];
            nums[i] = nums[nums[i]];
            nums[temp] = temp;
        } else {
            i++;
        }
    }
    for (i = 0; i < nums.length; i++) {
        if (nums[i] != i) return i;
    }
    return nums.length;
}
```

7. In-place Reversal of a LinkedList

Descrição:
Reversão de estruturas em listas ligadas sem alocação extra.

Exemplo: Reverter lista ligada
``` java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    while (head != null) {
        ListNode next = head.next;
        head.next = prev;
        prev = head;
        head = next;
    }
    return prev;
}
```

8. Tree Breadth-First Search (BFS)

Descrição:
Explora cada nível da árvore antes de prosseguir para o próximo.

Exemplo: BFS em árvore binária
``` java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) return res;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size();
        List<Integer> level = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            level.add(node.val);
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        res.add(level);
    }
    return res;
}
```

9. Tree Depth First Search (DFS)

Descrição:
Explora um ramo da árvore até o fundo antes de recuar.

Exemplo: Soma de folhas usando DFS
``` java
public int sumOfLeaves(TreeNode root) {
    if (root == null) return 0;
    if (root.left == null && root.right == null) return root.val;
    return sumOfLeaves(root.left) + sumOfLeaves(root.right);
}
```

10. Two Heaps

Descrição:
Utiliza dois heaps para manter a mediana ou separar elementos em duas metades.

Exemplo: Mediana da Stream de Números
``` java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
PriorityQueue<Integer> minHeap = new PriorityQueue<>();

public void addNum(int num) {
    maxHeap.offer(num);
    minHeap.offer(maxHeap.poll());
    if (maxHeap.size() < minHeap.size()) {
        maxHeap.offer(minHeap.poll());
    }
}

public double findMedian() {
    if (maxHeap.size() == minHeap.size())
        return (maxHeap.peek() + minHeap.peek()) / 2.0;
    return maxHeap.peek();
}
```

11. Subsets

Descrição:
Geração de todos os subconjuntos possíveis de um conjunto.

Exemplo:
``` java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    res.add(new ArrayList<>());
    for (int num : nums) {
        int n = res.size();
        for (int i = 0; i < n; i++) {
            List<Integer> subset = new ArrayList<>(res.get(i));
            subset.add(num);
            res.add(subset);
        }
    }
    return res;
}
```

12. Modified Binary Search

Descrição:
Busca binária com mudanças, comum em arrays rotacionados ou buscas condicionais.

Exemplo: Busca em array rotacionado
``` java
public int search(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        if (nums[left] <= nums[mid]) {
            if (nums[left] <= target && target < nums[mid])
                right = mid - 1;
            else
                left = mid + 1;
        } else {
            if (nums[mid] < target && target <= nums[right])
                left = mid + 1;
            else
                right = mid - 1;
        }
    }
    return -1;
}
```

13. Bitwise XOR

Descrição:
Operações para encontrar elementos únicos em arrays.

Exemplo: Elemento sem par
``` java
public int singleNumber(int[] nums) {
    int result = 0;
    for (int num : nums) {
        result ^= num;
    }
    return result;
}
```

14. Top 'K' Elements

Descrição:
Uso de heap para encontrar os K maiores/menores elementos rapidamente.

Exemplo: Top K Frequentes
``` java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int num : nums) freq.put(num, freq.getOrDefault(num, 0) + 1);
    PriorityQueue<Integer> heap = new PriorityQueue<>((a, b) -> freq.get(a) - freq.get(b));
    for (int num : freq.keySet()) {
        heap.offer(num);
        if (heap.size() > k) heap.poll();
    }
    int[] res = new int[k];
    for (int i = k - 1; i >= 0; i--) res[i] = heap.poll();
    return res;
}
```

15. K-way Merge

Descrição:
Combinação de múltiplas listas ordenadas.

Exemplo: Mesclagem de K listas ligadas ordenadas
``` java
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a.val));
    for (ListNode node : lists) if (node != null) pq.offer(node);
    ListNode dummy = new ListNode(0), curr = dummy;
    while (!pq.isEmpty()) {
        curr.next = pq.poll();
        curr = curr.next;
        if (curr.next != null) pq.offer(curr.next);
    }
    return dummy.next;
}
```

16. Topological Sort

Descrição:
Ordenação de vértices em um grafo direcionado acíclico (DAG).

Exemplo: Ordenação Topológica
``` java
public List<Integer> topSort(int vertices, int[][] edges) {
    List<Integer> sortedOrder = new ArrayList<>();
    Map<Integer, List<Integer>> graph = new HashMap<>();
    int[] inDegree = new int[vertices];
    for (int[] edge : edges) {
        graph.computeIfAbsent(edge[0], x -> new ArrayList<>()).add(edge[1]);
        inDegree[edge[1]]++;
    }
    Queue<Integer> sources = new LinkedList<>();
    for (int i = 0; i < vertices; i++)
        if (inDegree[i] == 0) sources.add(i);
    while (!sources.isEmpty()) {
        int vertex = sources.poll();
        sortedOrder.add(vertex);
        for (int child : graph.getOrDefault(vertex, new ArrayList<>())) {
            if (--inDegree[child] == 0) sources.add(child);
        }
    }
    return sortedOrder;
}
```

17. 0/1 Knapsack

Descrição:
Problema clássico de programação dinâmica.

Exemplo:
``` java
public int knapsack(int[] weights, int[] values, int W) {
    int n = weights.length;
    int[][] dp = new int[n + 1][W + 1];
    for (int i = 1; i <= n; i++) {
        for (int w = 1; w <= W; w++) {
            if (weights[i - 1] <= w)
                dp[i][w] = Math.max(values[i - 1] + dp[i - 1][w - weights[i - 1]], dp[i - 1][w]);
            else
                dp[i][w] = dp[i - 1][w];
        }
    }
    return dp[n][W];
}
```

18. Fibonacci Numbers

Descrição:
Série clássica, muito usada para ilustrar recursão, memoização e DP.

Exemplo: Otimizado com memoização
``` java
public int fibonacci(int n) {
    if (n <= 1) return n;
    int[] memo = new int[n + 1];
    memo[0] = 0; memo[1] = 1;
    for (int i = 2; i <= n; i++)
        memo[i] = memo[i - 1] + memo[i - 2];
    return memo[n];
}
```

19. Palindromic Subsequence

Descrição:
Subsequência palindrômica mais longa (DP clássico).

Exemplo:
``` java
public int longestPalindromeSubseq(String s) {
    int n = s.length();
    int[][] dp = new int[n][n];
    for (int i = n - 1; i >= 0; i--) {
        dp[i][i] = 1;
        for (int j = i + 1; j < n; j++) {
            if (s.charAt(i) == s.charAt(j))
                dp[i][j] = dp[i + 1][j - 1] + 2;
            else
                dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
        }
    }
    return dp[0][n - 1];
}
```

20. Longest Common Substring

Descrição:
Encontrar o maior segmento contínuo comum entre duas strings (DP).

Exemplo:
``` java
public int longestCommonSubstring(String s1, String s2) {
    int max = 0;
    int[][] dp = new int[s1.length() + 1][s2.length() + 1];
    for (int i = 1; i <= s1.length(); i++) {
        for (int j = 1; j <= s2.length(); j++) {
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
                max = Math.max(max, dp[i][j]);
            }
        }
    }
    return max;
}
```

Resumo

Esses padrões cobrem a base de 90% dos problemas de algoritmos em entrevistas técnicas. Domine-os para acelerada evolução em coding interviews e desafios de algoritmos!


# ChatGPT

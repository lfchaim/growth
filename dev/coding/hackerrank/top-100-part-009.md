House Robber II  
N-Queens II  
Best Time to Buy and Sell Stock II  
Clone Graph  
Sliding Window Maximum  
Merge Sorted Array  
Find the Celebrities  
Regular Expression Matching  
Distinct Subsequences  
Longest Increasing Subsequence  

Ótimo! Vamos continuar com a análise detalhada dos desafios. 🚀  

---

### **1. House Robber II**  
- **Categoria:** Programação Dinâmica  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/ca-2ke-205/challenges/house-robber-7-1)  

#### **Solução Java (código comentado):**  
```java
public class HouseRobberII {
    public static int rob(int[] nums) {
        if (nums.length == 1) return nums[0];

        return Math.max(robHelper(nums, 0, nums.length - 2), robHelper(nums, 1, nums.length - 1));
    }

    private static int robHelper(int[] nums, int start, int end) {
        int prev1 = 0, prev2 = 0;
        for (int i = start; i <= end; i++) {
            int temp = prev1;
            prev1 = Math.max(prev2 + nums[i], prev1);
            prev2 = temp;
        }
        return prev1;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Como as casas estão dispostas em um círculo, não podemos roubar a primeira e a última simultaneamente.
- Dividimos o problema em duas partes: roubamos de `0` a `n-2` ou de `1` a `n-1`.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Memorização**, mas o ganho de eficiência seria pequeno.

---

### **2. N-Queens II**  
- **Categoria:** Backtracking  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/beingzer0/challenges/bz-n-queens-ii)  

#### **Solução Java (código comentado):**  
```java
public class NQueensII {
    private static int count;

    public static int totalNQueens(int n) {
        count = 0;
        backtrack(new boolean[n], new boolean[2 * n], new boolean[2 * n], 0, n);
        return count;
    }

    private static void backtrack(boolean[] cols, boolean[] diag1, boolean[] diag2, int row, int n) {
        if (row == n) {
            count++;
            return;
        }

        for (int col = 0; col < n; col++) {
            if (cols[col] || diag1[row + col] || diag2[row - col + n]) continue;

            cols[col] = diag1[row + col] = diag2[row - col + n] = true;
            backtrack(cols, diag1, diag2, row + 1, n);
            cols[col] = diag1[row + col] = diag2[row - col + n] = false;
        }
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Backtracking** para contar todas as soluções possíveis.
- Mantemos três arrays booleanos para rastrear colunas e diagonais ocupadas.
- A complexidade é **O(n!)**, pois geramos todas as combinações.

#### **Alternativas/Variações:**  
- Podemos usar **Bitmasking** para melhorar eficiência.

---

### **3. Best Time to Buy and Sell Stock II**  
- **Categoria:** Arrays / Greedy  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/vit-bhopal/challenges/best-time-to-buy-and-sell-stock-8-1)  

#### **Solução Java (código comentado):**  
```java
public class StockProfitII {
    public static int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                profit += prices[i] - prices[i - 1];
            }
        }
        return profit;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Compramos e vendemos sempre que há um aumento no preço.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Programação Dinâmica**, mas isso não melhora a eficiência.

---

### **4. Clone Graph**  
- **Categoria:** Grafos / DFS  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/find-the-nearest-clone/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

class Node {
    int val;
    List<Node> neighbors;
    
    Node(int val) {
        this.val = val;
        this.neighbors = new ArrayList<>();
    }
}

public class CloneGraph {
    private static Map<Node, Node> map = new HashMap<>();

    public static Node cloneGraph(Node node) {
        if (node == null) return null;
        if (map.containsKey(node)) return map.get(node);

        Node clone = new Node(node.val);
        map.put(node, clone);

        for (Node neighbor : node.neighbors) {
            clone.neighbors.add(cloneGraph(neighbor));
        }

        return clone;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **DFS (`Recursão`)** para copiar cada nó e seus vizinhos.
- A complexidade é **O(n)**, pois percorremos todos os nós.

#### **Alternativas/Variações:**  
- Podemos usar **BFS (`Queue`)**, mas isso não melhora a eficiência.

---

### **5. Sliding Window Maximum**  
- **Categoria:** Arrays / Deque  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/sliding-window1)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class SlidingWindowMax {
    public static int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        int[] result = new int[n - k + 1];
        Deque<Integer> deque = new LinkedList<>();

        for (int i = 0; i < n; i++) {
            while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) deque.pollFirst();
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) deque.pollLast();
            deque.addLast(i);

            if (i >= k - 1) result[i - k + 1] = nums[deque.peekFirst()];
        }

        return result;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Deque (`LinkedList`)** para armazenar índices de elementos relevantes.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Heap (`PriorityQueue`)**, mas isso aumenta a complexidade para **O(n log k)**.

---

Vou continuar com os próximos desafios! 🚀🔥

Ótimo! Vamos seguir com a análise detalhada dos próximos desafios. 🚀  

---

### **6. Merge Sorted Array**  
- **Categoria:** Arrays / Manipulação de Dados  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/merge-sorted-array/)  

#### **Solução Java (código comentado):**  
```java
public class MergeSortedArray {
    public static void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1, j = n - 1, k = m + n - 1;

        while (j >= 0) {
            if (i >= 0 && nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **três ponteiros**, começando pelos últimos elementos de `nums1` e `nums2`.
- Preenchendo `nums1` de trás para frente evita sobrescrever elementos ainda não ordenados.
- A complexidade é **O(m + n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Arrays.sort()**, mas isso adiciona complexidade de **O((m + n) log(m + n))**.

---

### **7. Find the Celebrity**  
- **Categoria:** Grafos / Matriz de Adjacência  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/find-the-celebrity/)  

#### **Solução Java (código comentado):**  
```java
public class FindCelebrity {
    public static int findCelebrity(int n, boolean[][] knowsMatrix) {
        int celebrity = 0;
        
        for (int i = 1; i < n; i++) {
            if (knowsMatrix[celebrity][i]) {
                celebrity = i;
            }
        }

        for (int i = 0; i < n; i++) {
            if (i != celebrity && (knowsMatrix[celebrity][i] || !knowsMatrix[i][celebrity])) {
                return -1;
            }
        }

        return celebrity;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Primeiro identificamos um possível candidato a celebridade eliminando pessoas que conhecem outras.
- Em seguida, verificamos se esse candidato realmente é a celebridade.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **DFS**, mas isso não melhora a eficiência.

---

### **8. Regular Expression Matching**  
- **Categoria:** Strings / Programação Dinâmica  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/regular-expression-matching/)  

#### **Solução Java (código comentado):**  
```java
public class RegexMatching {
    public static boolean isMatch(String s, String p) {
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
        dp[0][0] = true;

        for (int j = 1; j <= p.length(); j++) {
            if (p.charAt(j - 1) == '*') dp[0][j] = dp[0][j - 2];
        }

        for (int i = 1; i <= s.length(); i++) {
            for (int j = 1; j <= p.length(); j++) {
                if (p.charAt(j - 1) == '.' || p.charAt(j - 1) == s.charAt(i - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i][j - 2] || ((s.charAt(i - 1) == p.charAt(j - 2) || p.charAt(j - 2) == '.') && dp[i - 1][j]);
                }
            }
        }

        return dp[s.length()][p.length()];
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Programação Dinâmica (`dp`)** para verificar se `s` corresponde ao padrão `p`.
- Consideramos casos com `.` e `*`, tratando cada caractere separadamente.
- A complexidade é **O(m * n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Recursão**, mas isso aumentaria o tempo de execução.

---

### **9. Distinct Subsequences**  
- **Categoria:** Programação Dinâmica / Strings  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/distinct-subsequences/)  

#### **Solução Java (código comentado):**  
```java
public class DistinctSubsequences {
    public static int numDistinct(String s, String t) {
        int[][] dp = new int[s.length() + 1][t.length() + 1];

        for (int i = 0; i <= s.length(); i++) dp[i][0] = 1;

        for (int i = 1; i <= s.length(); i++) {
            for (int j = 1; j <= t.length(); j++) {
                dp[i][j] = dp[i - 1][j];
                if (s.charAt(i - 1) == t.charAt(j - 1)) {
                    dp[i][j] += dp[i - 1][j - 1];
                }
            }
        }

        return dp[s.length()][t.length()];
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Programação Dinâmica (`dp`)** para contar subsequências distintas de `t` em `s`.
- A complexidade é **O(m * n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Recursão + Memorização**, mas o ganho de eficiência seria pequeno.

---

### **10. Longest Increasing Subsequence**  
- **Categoria:** Programação Dinâmica / Busca Binária  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/longest-increasing-subsequence/)  

#### **Solução Java (código comentado):**  
```java
import java.util.Arrays;

public class LongestIncreasingSubsequence {
    public static int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        Arrays.fill(dp, 1);

        int maxLen = 1;
        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        }

        return maxLen;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Programação Dinâmica (`dp`)** para armazenar o comprimento da sequência crescente.
- A complexidade é **O(n²)**, mas pode ser reduzida para **O(n log n)** usando busca binária.

#### **Alternativas/Variações:**  
- Podemos usar **Patience Sorting (`Binary Search`)**, reduzindo a complexidade.

---

Finalizamos mais uma rodada de análises! 🚀🔥 Caso tenha mais desafios para avaliar, estou à disposição. 😊

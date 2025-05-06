Maximum Product Subarray  
Search Insert Position  
Unique Paths  
Decode Ways  
Jump Game  
Word Search  
Set Matrix Zeroes  
Trapping Rain Water  
Sudoku Solver  
Spiral Order Matrix  

Ótimo! Vamos continuar com a análise detalhada dos desafios. 🚀  

---

### **1. Maximum Product Subarray**  
- **Categoria:** Arrays / Programação Dinâmica  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/contests/beingzer0/challenges/bz-maximum-product-subarray)  

#### **Solução Java (código comentado):**  
```java
public class MaximumProductSubarray {
    public static int maxProduct(int[] nums) {
        int maxProduct = nums[0], minProduct = nums[0], result = nums[0];

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < 0) {
                int temp = maxProduct;
                maxProduct = minProduct;
                minProduct = temp;
            }

            maxProduct = Math.max(nums[i], maxProduct * nums[i]);
            minProduct = Math.min(nums[i], minProduct * nums[i]);

            result = Math.max(result, maxProduct);
        }

        return result;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Mantemos dois valores: **máximo e mínimo produto** até o índice atual.
- Se o número for negativo, trocamos os valores para considerar inversões.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Divisão e Conquista**, mas isso aumenta a complexidade.

---

### **2. Search Insert Position**  
- **Categoria:** Arrays / Busca Binária  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/insert-a-node-at-a-specific-position-in-a-linked-list/problem)  

#### **Solução Java (código comentado):**  
```java
public class SearchInsertPosition {
    public static int searchInsert(int[] nums, int target) {
        int left = 0, right = nums.length - 1;

        while (left <= right) {
            int mid = (left + right) / 2;

            if (nums[mid] == target) return mid;
            if (nums[mid] < target) left = mid + 1;
            else right = mid - 1;
        }

        return left;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Busca Binária** para encontrar a posição correta de inserção.
- Se o número não for encontrado, retornamos a posição onde ele deveria estar.
- A complexidade é **O(log n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Busca Linear**, mas isso aumenta a complexidade para **O(n)**.

---

### **3. Unique Paths**  
- **Categoria:** Programação Dinâmica / Combinatória  
- **Link do Desafio:** [LeetCode](https://leetcode.com/problems/unique-paths/)  

#### **Solução Java (código comentado):**  
```java
public class UniquePaths {
    public static int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];

        for (int i = 0; i < m; i++) dp[i][0] = 1;
        for (int j = 0; j < n; j++) dp[0][j] = 1;

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }

        return dp[m - 1][n - 1];
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Programação Dinâmica** para calcular o número de caminhos únicos.
- Cada célula depende da soma dos caminhos das células acima e à esquerda.
- A complexidade é **O(m * n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Combinatória**, reduzindo a complexidade para **O(1)**.

---

### **4. Decode Ways**  
- **Categoria:** Programação Dinâmica / Strings  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/Decode)  

#### **Solução Java (código comentado):**  
```java
public class DecodeWays {
    public static int numDecodings(String s) {
        if (s.isEmpty() || s.charAt(0) == '0') return 0;

        int[] dp = new int[s.length() + 1];
        dp[0] = 1;
        dp[1] = 1;

        for (int i = 2; i <= s.length(); i++) {
            if (s.charAt(i - 1) != '0') {
                dp[i] += dp[i - 1];
            }
            int twoDigit = Integer.parseInt(s.substring(i - 2, i));
            if (twoDigit >= 10 && twoDigit <= 26) {
                dp[i] += dp[i - 2];
            }
        }

        return dp[s.length()];
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Programação Dinâmica (`dp`)** para rastrear as formas de decodificar `s`.
- O valor `dp[i]` depende do último caractere e dos últimos dois caracteres.
- A complexidade é **O(n)**, onde `n` é o tamanho da string.

#### **Alternativas/Variações:**  
- Podemos usar **Backtracking**, mas isso aumenta a complexidade.

---

Vou continuar com os próximos desafios! 🚀🔥

Ótimo! Vamos seguir com a análise detalhada dos próximos desafios. 🚀  

---

### **5. Jump Game**  
- **Categoria:** Arrays / Greedy  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/jump-game/problem)  

#### **Solução Java (código comentado):**  
```java
public class JumpGame {
    public static boolean canJump(int[] nums) {
        int maxReach = 0;

        for (int i = 0; i < nums.length; i++) {
            if (i > maxReach) return false;
            maxReach = Math.max(maxReach, i + nums[i]);
        }

        return true;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Mantemos um **rastreador do alcance máximo** (`maxReach`).
- Se `i` ultrapassar `maxReach`, não é possível alcançar o final.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **Programação Dinâmica**, mas isso não melhora a eficiência.

---

### **6. Word Search**  
- **Categoria:** Matrizes / Backtracking  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/word-search/problem)  

#### **Solução Java (código comentado):**  
```java
public class WordSearch {
    public static boolean exist(char[][] board, String word) {
        int rows = board.length, cols = board[0].length;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (backtrack(board, word, i, j, 0)) return true;
            }
        }

        return false;
    }

    private static boolean backtrack(char[][] board, String word, int i, int j, int index) {
        if (index == word.length()) return true;
        if (i < 0 || j < 0 || i >= board.length || j >= board[0].length || board[i][j] != word.charAt(index)) 
            return false;

        char temp = board[i][j];
        board[i][j] = '*'; // Marca como visitado

        boolean found = backtrack(board, word, i + 1, j, index + 1) ||
                        backtrack(board, word, i - 1, j, index + 1) ||
                        backtrack(board, word, i, j + 1, index + 1) ||
                        backtrack(board, word, i, j - 1, index + 1);

        board[i][j] = temp; // Desfaz a marcação
        return found;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Backtracking** para explorar todas as direções da matriz.
- Marcamos posições temporariamente para evitar revisitar durante a busca.
- A complexidade pode chegar a **O(4ⁿ)**, onde `n` é o tamanho da palavra.

#### **Alternativas/Variações:**  
- Podemos usar **Trie** para melhorar a busca quando houver várias palavras.

---

### **7. Set Matrix Zeroes**  
- **Categoria:** Matrizes / Manipulação de Dados  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/set-matrix-zeroes/problem)  

#### **Solução Java (código comentado):**  
```java
public class SetMatrixZeroes {
    public static void setZeroes(int[][] matrix) {
        int rows = matrix.length, cols = matrix[0].length;
        boolean firstRowZero = false, firstColZero = false;

        for (int i = 0; i < rows; i++) {
            if (matrix[i][0] == 0) firstColZero = true;
        }
        for (int j = 0; j < cols; j++) {
            if (matrix[0][j] == 0) firstRowZero = true;
        }

        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        if (firstColZero) {
            for (int i = 0; i < rows; i++) matrix[i][0] = 0;
        }
        if (firstRowZero) {
            for (int j = 0; j < cols; j++) matrix[0][j] = 0;
        }
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos a **primeira linha e primeira coluna** como marcadores para evitar uso de memória extra.
- Passamos pela matriz duas vezes: uma para marcar e outra para atualizar os valores.
- A complexidade é **O(m * n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **arrays extras**, mas isso consome mais espaço.

---

### **8. Trapping Rain Water**  
- **Categoria:** Arrays / Dois Ponteiros  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/trapping-rain-water/problem)  

#### **Solução Java (código comentado):**  
```java
public class TrappingRainWater {
    public static int trap(int[] height) {
        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int trappedWater = 0;

        while (left <= right) {
            if (height[left] <= height[right]) {
                leftMax = Math.max(leftMax, height[left]);
                trappedWater += leftMax - height[left];
                left++;
            } else {
                rightMax = Math.max(rightMax, height[right]);
                trappedWater += rightMax - height[right];
                right--;
            }
        }

        return trappedWater;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **dois ponteiros** para rastrear a altura máxima à esquerda e à direita.
- Calculamos a água acumulada com base na altura mínima das margens.
- A complexidade é **O(n)**, tornando a solução eficiente.

#### **Alternativas/Variações:**  
- Podemos usar **pilha**, mas isso aumenta a complexidade de espaço.

---

### **9. Sudoku Solver**  
- **Categoria:** Backtracking / Matrizes  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/sudoku-solver/problem)  

#### **Solução Java (código comentado):**  
```java
public class SudokuSolver {
    public static boolean solveSudoku(char[][] board) {
        return backtrack(board);
    }

    private static boolean backtrack(char[][] board) {
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') {
                    for (char num = '1'; num <= '9'; num++) {
                        if (isValid(board, i, j, num)) {
                            board[i][j] = num;
                            if (backtrack(board)) return true;
                            board[i][j] = '.';
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }

    private static boolean isValid(char[][] board, int row, int col, char num) {
        for (int i = 0; i < 9; i++) {
            if (board[row][i] == num || board[i][col] == num ||
                board[row / 3 * 3 + i / 3][col / 3 * 3 + i % 3] == num) {
                return false;
            }
        }
        return true;
    }
}
```

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **Backtracking** para testar cada número possível nas células vazias.
- Validamos cada número antes de inseri-lo na matriz.
- A complexidade é **O(9⁸)** no pior caso.

#### **Alternativas/Variações:**  
- Podemos usar **Programação Dinâmica** para armazenar estados intermediários.

---

Finalizamos mais uma rodada de análises! 🚀🔥 Caso tenha mais desafios para avaliar, estou à disposição. 😊

Ótimo! Vamos seguir com a análise detalhada dos próximos desafios. 🚀  

---

### **10. Spiral Order Matrix**  
- **Categoria:** Matrizes / Manipulação de Dados  
- **Link do Desafio:** [HackerRank](https://www.hackerrank.com/challenges/spiral-order-matrix/problem)  

#### **Solução Java (código comentado):**  
```java
import java.util.*;

public class SpiralMatrix {
    public static List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        if (matrix == null || matrix.length == 0) return result;

        int top = 0, bottom = matrix.length - 1;
        int left = 0, right = matrix[0].length - 1;

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

#### **Explicação da Lógica e Justificativa:**  
- Utilizamos **quatro variáveis** (`top`, `bottom`, `left`, `right`) para rastrear os limites da matriz.
- Percorremos a matriz em **ordem espiral**, movendo horizontal e verticalmente.
- A complexidade é **O(m * n)**, onde `m` e `n` são as dimensões da matriz.

#### **Alternativas/Variações:**  
- Podemos usar **Recursão**, mas isso adiciona custo extra de chamadas de função.

---

Finalizamos mais uma rodada de análises! 🚀🔥 Caso tenha mais desafios para avaliar, estou à disposição. 😊

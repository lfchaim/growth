# Prompt

Quais são algumas variações do algoritmo de dois ponteiros?

# Answer

Existem diversas variações do algoritmo de dois ponteiros, adaptadas a diferentes tipos de problemas e estruturas de dados. Cada variação modifica a forma e a lógica de movimento dos ponteiros para otimizar soluções de busca, particionamento ou análise de intervalos. A seguir, listo algumas dessas variações e exemplifico como elas podem ser aplicadas:

---

### 1. Ponteiros em Direções Opostas

**Descrição:**  
Utilizados para percorrer uma estrutura de dados a partir das extremidades. Um ponteiro inicia no começo e outro no fim, ambos se movendo em direção ao centro até que se encontrem ou a condição desejada seja satisfeita.  
**Exemplo de aplicação:** Verificar se uma string é palíndroma.

```java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}
```

---

### 2. Técnica da Janela Deslizante

**Descrição:**  
Essa variação utiliza dois ponteiros para delimitar uma "janela" (ou subarray/substring) que se expande ou contrai conforme critérios específicos são avaliados. É muito eficaz para problemas como encontrar a maior substring sem caracteres repetidos ou determinar subarrays cuja soma atenda a um determinado critério.  
**Diferencial:** O ponteiro que marca o início da janela e o que marca o fim se movem de forma coordenada para manter ou ajustar o tamanho da janela conforme as condições mudam.

---

### 3. Fast and Slow Pointers (Tartaruga e Lebre)

**Descrição:**  
Aqui, os dois ponteiros se movimentam em velocidades diferentes: um "lento" (que avança um passo de cada vez) e um "rápido" (que avança dois passos). Essa técnica é bastante útil em estruturas como listas encadeadas.  
**Exemplo de aplicação:** Detecção de ciclos em uma lista encadeada (Algoritmo de Floyd).

```java
public boolean hasCycle(ListNode head) {
    if (head == null || head.next == null) return false;
    ListNode slow = head, fast = head.next;
    while (fast != null && fast.next != null) {
        if (slow == fast)
            return true;
        slow = slow.next;
        fast = fast.next.next;
    }
    return false;
}
```

---

### 4. Fusao de Arrays Ordenados (Merge com Dois Ponteiros)

**Descrição:**  
Utilizado na fusão (merge) de arrays ou listas que já estão ordenadas. Dois ponteiros iteram, um para cada array, comparando elementos e construindo um novo array ordenado de forma linear.  
**Aplicação típica:** Etapa de merge em algoritmos de ordenação, como no Merge Sort.

---

### 5. Extensões para Múltiplos Ponteiros

**Descrição:**  
Embora a técnica básica utilize dois ponteiros, certos problemas exigem um número maior, como nos problemas de soma (por exemplo, o problema Three Sum). Nessas situações, é comum fixar um ou mais elementos e aplicar a lógica de dois ponteiros para os elementos restantes.  
**Aplicação típica:**  
- **Three Sum:** Fixamos um elemento e usamos dois ponteiros para encontrar os outros dois que completem a soma desejada.  
- **K-Sum:** Em geral, pode-se fixar (K-2) elementos e usar dois ponteiros para resolver a versão reduzida do problema.

---

### 6. Partitioning com Dois Ponteiros

**Descrição:**  
Usada em algoritmos de ordenação, como o Quick Sort, onde dois ponteiros são empregados para particionar o array em seções menores e maiores que um pivô. Um ponteiro rastreia a posição para colocação de valores menores, enquanto o outro varre o array, realizando as trocas quando necessário.  
**Benefício:** Essa técnica simplifica e acelera o processo de particionamento sem a necessidade de espaço extra.

---

### Considerações Finais

Cada variação explora o princípio de reduzir a complexidade dos algoritmos ao aproveitar a ordenação ou a estrutura dos dados para eliminar iterações desnecessárias. Seja para identificar um padrão em uma string, detectar ciclos em listas encadeadas, ou fundir arrays ordenados, a chave está em adaptar os passos dos ponteiros conforme as necessidades específicas do problema.

Além das variações apresentadas, é interessante explorar metodologias híbridas: por exemplo, combinar a técnica da janela deslizante com estruturas auxiliares (como mapas de frequência) pode derivar soluções ainda mais eficientes para certas classes de problemas. Essas estratégias híbridas demonstram como a essência dos dois ponteiros pode ser enriquecida e estendida para diversos cenários complexos.

Você gostaria de ver exemplos adicionais ou mergulhar em alguma destas variações com mais profundidade?

# Prompt

Can you provide more coding examples using two-pointer variations?

# Answer

Below are several additional coding examples in Java that showcase different variations of the two-pointer technique. These examples demonstrate how versatile and powerful the two-pointer (and related sliding window) strategy can be when solving common algorithm challenges.

---

### 1. **Reversing a String (In-Place)**

**Concept:**  
Use two pointers—one starting at the beginning and the other at the end—to swap characters until they meet. This technique reverses the array (or string) in place without using extra space.

```java
public class ReverseString {
    public static void reverse(char[] s) {
        int left = 0, right = s.length - 1;
        while (left < right) {
            // Swap characters at positions left and right
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            
            left++;
            right--;
        }
    }
    
    public static void main(String[] args) {
        char[] s = "hello".toCharArray();
        reverse(s);
        System.out.println(new String(s)); // Expected output: "olleh"
    }
}
```

---

### 2. **Sorted Squares**

**Concept:**  
Given a sorted array (which may contain negative numbers), the largest square may come from either end. Two pointers are initialized at the beginning and end to place the largest square value at the correct position in a result array.

```java
import java.util.Arrays;

public class SortedSquares {
    public static int[] sortedSquares(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        int left = 0, right = n - 1;
        int pos = n - 1; // Position to fill in the result array
        
        while (left <= right) {
            // Compare absolute values to decide which square to place at 'pos'
            if (Math.abs(nums[left]) > Math.abs(nums[right])) {
                result[pos] = nums[left] * nums[left];
                left++;
            } else {
                result[pos] = nums[right] * nums[right];
                right--;
            }
            pos--;
        }
        return result;
    }
    
    public static void main(String[] args) {
        int[] nums = {-7, -3, 2, 3, 11};
        int[] squares = sortedSquares(nums);
        System.out.println(Arrays.toString(squares)); // Expected: [4, 9, 9, 49, 121]
    }
}
```

---

### 3. **Partitioning Even and Odd Numbers**

**Concept:**  
Using two pointers—one at the start and one at the end—we can rearrange an array so that all even numbers appear on one side and odd numbers on the other. The pointers move inward and swap elements that are out of place.

```java
import java.util.Arrays;

public class PartitionEvenOdd {
    public static void partitionEvenOdd(int[] nums) {
        int left = 0, right = nums.length - 1;
        
        while (left < right) {
            // Move left pointer if current element is even
            while (left < right && nums[left] % 2 == 0) {
                left++;
            }
            // Move right pointer if current element is odd
            while (left < right && nums[right] % 2 != 0) {
                right--;
            }
            // Swap elements that are in the wrong partition
            if (left < right) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
                right--;
            }
        }
    }
    
    public static void main(String[] args) {
        int[] nums = {12, 17, 70, 15, 22, 65, 21, 90};
        partitionEvenOdd(nums);
        System.out.println(Arrays.toString(nums));
        // Possible output: all even numbers grouped together, followed by the odd numbers
    }
}
```

---

### 4. **Maximum Sum Subarray of Fixed Size k (Sliding Window)**

**Concept:**  
This example uses two pointers to maintain a sliding window of fixed length _k_ over an array. As the window slides, update the sum by subtracting the element leaving the window and adding the new element.

```java
public class MaxSubarraySum {
    public static int maxSubarraySum(int[] nums, int k) {
        int n = nums.length;
        if (n < k) return -1; // Not enough elements
        
        // Compute the initial window sum
        int windowSum = 0;
        for (int i = 0; i < k; i++) {
            windowSum += nums[i];
        }
        int maxSum = windowSum;
        
        // Slide the window from index k to the end
        for (int i = k; i < n; i++) {
            windowSum += nums[i] - nums[i - k];
            maxSum = Math.max(maxSum, windowSum);
        }
        return maxSum;
    }
    
    public static void main(String[] args) {
        int[] nums = {2, 1, 5, 1, 3, 2};
        int k = 3;
        System.out.println("Max sum for subarray of length " + k + ": " + maxSubarraySum(nums, k));
    }
}
```

---

### 5. **Dutch National Flag Problem (Three-Way Partitioning)**

**Concept:**  
Although this variation uses three pointers (low, mid, and high), it extends the two-pointer technique to partition an array containing elements of three distinct types (commonly 0, 1, and 2) without extra space.

```java
import java.util.Arrays;

public class SortColors {
    public static void sortColors(int[] nums) {
        int low = 0, mid = 0, high = nums.length - 1;
        
        while (mid <= high) {
            if (nums[mid] == 0) {
                // Swap current 0 with the element at 'low'
                int temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;
                low++;
                mid++;
            } else if (nums[mid] == 1) {
                mid++;
            } else { // nums[mid] == 2
                // Swap current 2 with the element at 'high'
                int temp = nums[mid];
                nums[mid] = nums[high];
                nums[high] = temp;
                high--;
            }
        }
    }
    
    public static void main(String[] args) {
        int[] colors = {2, 0, 2, 1, 1, 0};
        sortColors(colors);
        System.out.println(Arrays.toString(colors)); // Expected output: [0, 0, 1, 1, 2, 2]
    }
}
```

---

### 6. **Longest Substring with At Most K Distinct Characters (Sliding Window with Dynamic Window Size)**

**Concept:**  
For string problems, two pointers can define a sliding window whose size varies based on constraints. Here, we maintain a window that contains at most _k_ distinct characters by using a hashmap. When the window violates the constraint, the left pointer advances to restore the condition.

```java
import java.util.HashMap;
import java.util.Map;

public class LongestSubstringKDistinct {
    public static int lengthOfLongestSubstringKDistinct(String s, int k) {
        if (s == null || s.isEmpty() || k == 0) return 0;
        int left = 0, right = 0, maxLength = 0;
        Map<Character, Integer> charCount = new HashMap<>();
        
        while (right < s.length()) {
            // Include the character at position 'right'
            char rightChar = s.charAt(right);
            charCount.put(rightChar, charCount.getOrDefault(rightChar, 0) + 1);
            
            // If the window violates the k distinct characters constraint, shrink it from the left
            while (charCount.size() > k) {
                char leftChar = s.charAt(left);
                charCount.put(leftChar, charCount.get(leftChar) - 1);
                if (charCount.get(leftChar) == 0) {
                    charCount.remove(leftChar);
                }
                left++;
            }
            
            // Update maximum length found so far
            maxLength = Math.max(maxLength, right - left + 1);
            right++;
        }
        return maxLength;
    }
    
    public static void main(String[] args) {
        String s = "eceba";
        int k = 2;
        System.out.println("Length of longest substring with at most " + k + " distinct characters: " +
                           lengthOfLongestSubstringKDistinct(s, k));
    }
}
```

---

### Final Thoughts

These examples illustrate how flexible the two-pointer technique (and its variations) can be—from simple in-place reversal to dynamic window management in strings. Each variation is tailored to the specific structure and requirements of the problem, and learning them can significantly improve efficiency in coding interviews and competitive programming.

If you'd like to explore further variations—such as combining the two-pointer approach with recursion or adapting it to other domains like interval merging—feel free to ask!


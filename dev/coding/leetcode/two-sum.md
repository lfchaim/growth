Ótima escolha! O problema "Two Sum" do LeetCode é um clássico de programação que testa habilidades de busca e estrutura de dados. Vou apresentar três abordagens em Java, da menos eficiente para a mais eficiente, comentando cada uma.

---

### 1️⃣ Solução Ingênua (Força Bruta) - **O(n²)**
Esta solução verifica todas as combinações de pares possíveis dentro do array. Embora seja fácil de entender, tem complexidade **O(n²)**, tornando-se ineficiente para grandes conjuntos de dados.

```java
import java.util.*;

public class TwoSumBruteForce {
    public static int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j}; // Retorna os índices
                }
            }
        }
        return new int[]{}; // Caso não encontre
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        System.out.println(Arrays.toString(twoSum(nums, target))); // [0, 1]
    }
}
```

🔹 **Comentário:** Duplo loop aninhado causa alto custo computacional quando `n` cresce. Ineficiente!

---

### 2️⃣ Solução com HashMap - **O(n)**
Aqui utilizamos um `HashMap` para armazenar os valores já vistos, reduzindo a complexidade para **O(n)**. Muito mais eficiente!

```java
import java.util.*;

public class TwoSumHashMap {
    public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complemento = target - nums[i];
            if (map.containsKey(complemento)) {
                return new int[]{map.get(complemento), i};
            }
            map.put(nums[i], i);
        }
        return new int[]{}; // Caso não encontre
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        System.out.println(Arrays.toString(twoSum(nums, target))); // [0, 1]
    }
}
```

🔹 **Comentário:** O uso de um `HashMap` permite busca em tempo constante **O(1)**, tornando a abordagem linear **O(n)**.

---

### 3️⃣ Solução com Dois Ponteiros (Ordenação + Busca) - **O(n log n)**
Uma alternativa eficiente para quando **não precisamos retornar os índices**. Ordenamos e usamos dois ponteiros.

```java
import java.util.Arrays;

public class TwoSumTwoPointers {
    public static boolean twoSum(int[] nums, int target) {
        Arrays.sort(nums); // O(n log n)
        int left = 0, right = nums.length - 1;
        
        while (left < right) {
            int sum = nums[left] + nums[right];
            if (sum == target) return true;
            else if (sum < target) left++;
            else right--;
        }
        return false;
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        System.out.println(twoSum(nums, target)); // true
    }
}
```

🔹 **Comentário:** Esta abordagem é excelente se apenas precisarmos verificar **se existe uma solução**, pois não retorna os índices originais.

---

## 📌 Conclusão:
1. **Força Bruta** -> Simples, mas ineficiente (**O(n²)**).
2. **HashMap** -> Melhor abordagem para encontrar índices (**O(n)**).
3. **Dois Ponteiros** -> Útil quando precisamos apenas validar a existência (**O(n log n)**).

Se precisar de mais explicações ou variações, só me chamar! 🚀

## Resultado
Runtime: 2ms Beats 98.83%
Memory: 44.98MB Beats 63.53%

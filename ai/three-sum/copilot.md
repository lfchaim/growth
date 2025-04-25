# Prompt
Resolva o algoritmo Three Sum, apresentando todas as possíveis soluções, ordenadas da pior para a melhor solução. Dê exemplos de código usando Java.

# Answer

A seguir, vamos explorar três abordagens para resolver o problema Three Sum – encontrar todos os trios em um array cuja soma é zero – ordenadas, do **pior desempenho** (mais ineficiente) até a **melhor solução** (mais eficiente). Embora existam variações, apresento três métodos comuns:

1. **Força Bruta (O(n³)) – Pior Solução**  
   Essa abordagem utiliza três laços aninhados para testar todas as combinações de três elementos e, se a soma for zero, adiciona o trio (depois de ordená-lo para evitar duplicatas) a um conjunto. Embora seja simples e intuitiva, ela não escala bem para arrays grandes porque seu tempo de execução cresce em proporção ao cubo do tamanho da entrada.

2. **Busca Binária (O(n² · log n)) – Solução Intermediária**  
   Após ordenar o array, fixamos dois elementos com laços aninhados e utilizamos a busca binária para procurar o terceiro elemento que complete o trio com soma zero. Essa técnica reduz a complexidade da terceira iteração de O(n) para O(log n). No entanto, é necessário um cuidado extra para evitar duplicatas e garantir que o índice encontrado esteja à direita dos dois primeiros elementos. A complexidade melhora em relação à força bruta, mas ainda não é a solução ideal.

3. **Dois Ponteiros (O(n²)) – Melhor Solução**  
   Também após ordenar o array, fixamos um elemento e, para os demais, usamos dois ponteiros (inicial e final) que se movem em direção um do outro para encontrar os pares que somam o complemento necessário para zerar a soma. Essa abordagem é considerada a mais eficiente, pois elimina a necessidade de um laço extra ou de chamadas a métodos de busca, além de simplificar o tratamento de duplicatas.

A seguir, os exemplos de código em Java para cada abordagem:

---

### 1. **Força Bruta (O(n³))**

```java
import java.util.*;

public class ThreeSumBruteForce {
    public static List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> set = new HashSet<>(); // Utilizado para evitar duplicatas
        int n = nums.length;
        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (nums[i] + nums[j] + nums[k] == 0) {
                        List<Integer> triplet = Arrays.asList(nums[i], nums[j], nums[k]);
                        Collections.sort(triplet); // Ordena o trio para consistência
                        set.add(triplet);
                    }
                }
            }
        }
        return new ArrayList<>(set);
    }
    
    public static void main(String[] args) {
        int[] nums = {-1, 0, 1, 2, -1, -4};
        List<List<Integer>> result = threeSum(nums);
        System.out.println("Solução Força Bruta:");
        System.out.println(result);
    }
}
```

> **Observação:**  
> Essa solução é clara, mas devido aos três laços aninhados, sua performance se deteriora rapidamente conforme aumentamos o tamanho do array.

---

### 2. **Busca Binária (O(n² · log n))**

```java
import java.util.*;

public class ThreeSumBinarySearch {
    public static List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums); // Ordenamos o array para aplicar busca binária e facilitar tratamento de duplicatas
        int n = nums.length;
        
        for (int i = 0; i < n - 2; i++) {
            // Evita processar elementos duplicados para i
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            
            for (int j = i + 1; j < n - 1; j++) {
                // Evita processar elementos duplicados para j dentro do mesmo i
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;
                
                int target = -(nums[i] + nums[j]);
                // Realiza busca binária no intervalo [j+1, n)
                int index = Arrays.binarySearch(nums, j + 1, n, target);
                if (index > j) { // índice válido e maior que j
                    result.add(Arrays.asList(nums[i], nums[j], nums[index]));
                }
            }
        }
        return result;
    }
    
    public static void main(String[] args) {
        int[] nums = {-1, 0, 1, 2, -1, -4};
        List<List<Integer>> result = threeSum(nums);
        System.out.println("Solução com Busca Binária:");
        System.out.println(result);
    }
}
```

> **Observação:**  
> Essa abordagem melhora em relação à força bruta ao substituir o terceiro laço por uma busca binária, mas ainda possui a complexidade de O(n² · log n) e requer cuidado ao lidar com duplicatas.

---

### 3. **Dois Ponteiros (O(n²)) – Melhor Solução**

```java
import java.util.*;

public class ThreeSumTwoPointers {
    public static List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums); // Ordena o array para facilitar o uso dos ponteiros e tratar duplicatas
        int n = nums.length;
        
        for (int i = 0; i < n - 2; i++) {
            // Pula elementos duplicados para não repetir trios
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            
            int left = i + 1;
            int right = n - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    
                    // Evita duplicatas para o ponteiro 'left'
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    // Evita duplicatas para o ponteiro 'right'
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    left++;
                    right--;
                } else if (sum < 0) {
                    left++; // Precisamos de um valor maior
                } else {
                    right--; // Precisamos de um valor menor
                }
            }
        }
        return result;
    }
    
    public static void main(String[] args) {
        int[] nums = {-1, 0, 1, 2, -1, -4};
        List<List<Integer>> result = threeSum(nums);
        System.out.println("Solução Two Pointers:");
        System.out.println(result);
    }
}
```

> **Observação:**  
> Após ordenar o array, o uso de dois ponteiros nos permite encontrar os pares complementares de forma linear para cada elemento fixo, reduzindo a complexidade total para O(n²). Essa abordagem é a mais eficiente dentre as apresentadas, além de facilitar o gerenciamento de duplicatas.

---

### Resumo e Considerações Finais

- **Força Bruta (O(n³))**:  
  Fácil de implementar e de entender, mas ineficiente para arrays grandes devido à grande quantidade de iterações.

- **Busca Binária (O(n² · log n))**:  
  Uma melhora em relação à força bruta, mas que ainda envolve múltiplas iterações aninhadas e requer tratamento cuidadoso de duplicatas.

- **Dois Ponteiros (O(n²))**:  
  A melhor solução para este problema. Após ordenar o array, ela utiliza dois ponteiros para reduzir drasticamente o número de operações, proporcionando um algoritmo mais rápido e elegante para conjuntos de dados maiores.

Cada uma dessas abordagens tem seu lugar dependendo do tamanho da entrada e dos requisitos do ambiente de execução. Por exemplo, se a clareza e a simplicidade forem prioritárias para entradas pequenas, a força bruta pode ser suficiente; contudo, para aplicações em produção ou em concorrência com grandes volumes de dados, a abordagem de dois ponteiros é altamente recomendada.

Caso deseje saber mais sobre otimizações para problemas semelhantes ou explorar variações e desafios como o _K-Sum_, posso explicar estratégias avançadas e técnicas de divisão e conquista que podem ser aplicadas.
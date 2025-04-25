# Two Pointer
A técnica **Two Pointer** é um padrão essencial para resolver diversos problemas com arrays e strings, principalmente quando se lida com estruturas ordenadas. Essa abordagem baseia-se em utilizar dois ponteiros que se movem ao longo da estrutura (geralmente um no início e outro no fim), de forma a reduzir a complexidade temporal e, muitas vezes, evitar o uso de estruturas auxiliares. A seguir, vamos explorar esse padrão de forma abrangente, ilustrando seus conceitos, aplicações em plataformas como Leetcode, Hackerrank e Codesign, e apresentando exemplos práticos em Java.

---

## 1. Fundamentos do Padrão Two Pointer

### Conceito Geral

A ideia central do Two Pointer é manter dois índices (ou ponteiros) que percorrem a estrutura de dados simultaneamente. Dependendo do problema, esses ponteiros podem:

- **Iniciar em extremos opostos:** Um ponteiro no início e outro no final do array/string. Conforme avançam, os ponteiros se encontram no meio, avaliando condições e tomando decisões com base na soma, na correspondência de caracteres, etc.
- **Iniciar a partir do mesmo ponto e avançar com velocidades diferentes:** Essa variação é útil, por exemplo, em problemas que envolvem detecção de ciclos ou busca de pontos médios (como na técnica slow–fast pointers em listas ligadas).

A simplicidade do método contrasta com sua eficiência, já que muitos problemas aparentemente complexos podem ser resolvidos em tempo linear O(n) utilizando essa estratégia.

---

## 2. Por que Usar o Two Pointer?

O padrão Two Pointer se destaca por:

- **Redução de Complexidade:** Em muitos problemas, é possível evitar a complexidade quadrática (O(n²)) iterando com dois ponteiros em um único laço.
- **Simplicidade e Eficiência:** Uma vez entendida a lógica, o código apresenta menos complexidade e se torna mais eficiente, principalmente quando a estrutura de dados já está ordenada.
- **Flexibilidade:** Pode ser adaptado para diversas situações, como busca de pares com soma igual a um alvo, verificação de palíndromos e a remoção de duplicatas dentro de arrays ordenados.

Essa abordagem tem ampla aplicabilidade em desafios de programação, principalmente em plataformas de testes e desafios online como Leetcode, Hackerrank e Codesign.

---

## 3. Aplicação em Plataformas de Desafios

### Leetcode

Muitos problemas no Leetcode são resolvidos utilizando Two Pointer. Alguns exemplos clássicos:
- **Two Sum II - Input Array Is Sorted:** Utiliza ponteiros no início e no fim para encontrar dois números cuja soma corresponde a um alvo.
- **Container With Most Water:** Os ponteiros se movem para otimizar a área contida entre duas linhas.
- **Valid Palindrome:** Verifica se uma string é palíndroma ignorando caracteres não alfanuméricos.

Esses desafios exigem um entendimento fino da manipulação dos ponteiros, com decisões dinâmicas baseadas na comparação dos elementos apontados.

### Hackerrank

No Hackerrank, desafios que envolvem manipulação de strings, arrays ordenados ou problemas de janelas deslizantes (que podem ser vistos como uma variação do Two Pointer) são comuns. Exemplos incluem encontrar subsequências, contagem de pares específicos e problemas de soma em subarrays.

### Codesign

Embora o Codesign (ou plataformas similares voltadas para design de código e resolução de problemas) possa não ser tão conhecido quanto os anteriores, os desafios geralmente se concentram em escrever soluções elegantes e eficientes para problemas comuns de algoritmos. Utilizar o Two Pointer pode ser a chave para escrever um código limpo e de fácil manutenção, com ênfase na clareza e eficiência.

---

## 4. Exemplos Práticos em Java

### Exemplo 1: Two Sum II - Input Array Is Sorted

**Descrição:**  
Dado um array ordenado e um valor de `target`, encontre os índices de dois números cuja soma seja igual ao target.

```java
public class TwoSumII {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;
        
        while (left < right) {
            int currentSum = numbers[left] + numbers[right];
            if (currentSum == target) {
                // Os índices geralmente começam de 1 conforme a descrição do problema.
                return new int[]{left + 1, right + 1};
            } else if (currentSum < target) {
                left++;
            } else {
                right--;
            }
        }
        // Se não encontrar solução, pode retornar null ou um array vazio
        return new int[0];
    }
    
    public static void main(String[] args) {
        TwoSumII solver = new TwoSumII();
        int[] numbers = {2, 7, 11, 15};
        int target = 9;
        int[] result = solver.twoSum(numbers, target);
        if(result.length == 2){
            System.out.println("Índices: " + result[0] + ", " + result[1]);
        } else {
            System.out.println("Nenhuma solução encontrada.");
        }
    }
}
```

**Como Funciona:**  
- Dois ponteiros (`left` e `right`) percorrem o array dos extremos para o centro.
- Se a soma dos valores apontados for menor que o target, o ponteiro da esquerda avança. Se for maior, o ponteiro da direita recua.  
Essa abordagem reduz a complexidade para O(n).

---

### Exemplo 2: Verificação de Palíndromo Ignorando Caracteres Não Alfanuméricos

**Descrição:**  
Dado uma string, verifique se ela é palíndroma, considerando somente caracteres alfanuméricos e ignorando diferenças entre maiúsculas e minúsculas.

```java
public class PalindromeChecker {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;
        
        while (left < right) {
            // Ignorar caracteres não alfanuméricos
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }
            if (left < right) {
                if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                    return false;
                }
                left++;
                right--;
            }
        }
        return true;
    }
    
    public static void main(String[] args) {
        PalindromeChecker checker = new PalindromeChecker();
        String test1 = "A man, a plan, a canal: Panama";
        String test2 = "Hello World!";
        System.out.println("\"" + test1 + "\" é palíndromo? " + checker.isPalindrome(test1));
        System.out.println("\"" + test2 + "\" é palíndromo? " + checker.isPalindrome(test2));
    }
}
```

**Como Funciona:**  
- Dois ponteiros começam do início e fim da string.
- São ignorados caracteres indesejados (não alfanuméricos) e as comparações consideram a forma minúscula de cada caractere.
- Esse método é especialmente útil em problemas que exigem filtragem de dados durante a verificação de condições.

---

### Exemplo 3: Remoção de Duplicatas em um Array Ordenado

**Descrição:**  
Dado um array ordenado, remova duplicatas de forma que cada elemento apareça apenas uma vez. Utilize o Two Pointer para realizar essa tarefa in-place.

```java
public class RemoveDuplicates {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int uniqueIndex = 0;
        
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[uniqueIndex]) {
                uniqueIndex++;
                nums[uniqueIndex] = nums[i];
            }
        }
        // Retorna o número de elementos únicos.
        return uniqueIndex + 1;
    }
    
    public static void main(String[] args) {
        RemoveDuplicates rd = new RemoveDuplicates();
        int[] nums = {0,0,1,1,1,2,2,3,3,4};
        int newLength = rd.removeDuplicates(nums);
        System.out.print("Array sem duplicatas: ");
        for (int i = 0; i < newLength; i++) {
            System.out.print(nums[i] + " ");
        }
    }
}
```

**Como Funciona:**  
- Um ponteiro (`uniqueIndex`) mantém a posição do último elemento único encontrado.
- O laço percorre o array comparando elementos e atualiza o array in-place, mantendo somente os elementos únicos.
- Essa técnica é comumente utilizada em desafios para otimizar o uso de memória.

---

## 5. Variações e Dicas Adicionais

- **Two Pointer com Dados Não Ordenados:**  
  Em arrays não ordenados, muitas vezes é possível ordenar primeiro o array e em seguida aplicar o Two Pointer. Isso, contudo, pode acarretar um custo de tempo O(n log n) na ordenação. Avalie se o ordenamento é aceitável para o problema.

- **Uso de Ponteiros Lento e Rápido (Slow-Fast Pointers):**  
  Essa variação é muito útil para identificar ciclos em listas ligadas ou encontrar a mediana de uma estrutura dinamicamente.

- **Problemas com Janela Deslizante:**  
  A técnica de Two Pointer pode ser adaptada para problemas de janela deslizante, onde um ponteiro marca o início e outro marca o fim de uma subregião cujas propriedades devem ser monitoradas (por exemplo, soma de subarrays, número de elementos distintos).

- **Dicas de Implementação:**  
  - Sempre valide as condições de parada para evitar loops infinitos.  
  - Quando os ponteiros se encontram ou ultrapassam, garanta que todas as condições necessárias foram avaliadas.
  - Teste seu código com entradas de borda para assegurar a robustez da solução.

---

## 6. Conclusão

O padrão **Two Pointer** é uma ferramenta poderosa para enfrentar problemas de manipulação de arrays e strings em desafios de programação. Seja na identificação de pares com soma alvo, na verificação de palíndromos ou na remoção de duplicatas, essa técnica demonstra como uma estratégia simples pode oferecer soluções elegantes e eficientes. Plataformas como Leetcode, Hackerrank e Codesign oferecem uma variedade de problemas que exploram essa abordagem, incentivando os programadores a desenvolverem uma compreensão profunda e a aplicarem esse padrão de forma adaptativa.

---

### Explorando Mais o Tema

Além dos exemplos apresentados, é interessante explorar questões de:
- **Problemas de Interseção de Arrays:** Utilizando dois ponteiros para andar em arrays ordenados e encontrar interseções de maneira linear.
- **Problemas de Ordenação e Particionamento:** Como o algoritmo quicksort, que utiliza a ideia de dois ponteiros para particionar o array.
- **Desafios de Janelas Móveis:** Aplicados na análise de substrings e intervalos com restrições específicas.

Cada nova variação abre espaço para aprender nuances que podem ser aplicadas em diferentes contextos e desafios. Essa versatilidade faz do Two Pointer uma técnica indispensável tanto para entrevistas quanto para competições de programação.
  
# Binary Tree
# Topological Sort
# Binary Tree DFS
# Top K Elements
# Modified Binary Search
# Subset
# Sliding Window

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
A estrutura de dados conhecida como **Binary Tree** (ou Árvore Binária) é um dos padrões fundamentais em ciência da computação e resolução de problemas, sendo amplamente utilizada em desafios e entrevistas em plataformas como Leetcode, Hackerrank e Codesign. Nesta abordagem, cada nó possui no máximo dois filhos (geralmente chamados de _left_ e _right_), o que permite a implementação de algoritmos eficientes para diversas operações como buscas, ordenação, travessia e particionamento.

Em uma árvore binária, cada nó pode conter um valor (ou informação) e referências para seus nós filhos. Essa estrutura é a base para outras variações, como as **Binary Search Trees (BST)**, que aplicam uma regra de ordenação (nós à esquerda possuem valor menor e à direita, valor maior), permitindo buscas em tempo logarítmico na média dos casos. Além disso, conceitos como árvores balanceadas (AVL, Red-Black) e completas garantem eficiência em operações dinâmicas.

---

## 1. Conceitos Fundamentais e Propriedades

### O que é uma Árvore Binária?

- **Definição:**  
  Uma árvore binária é uma estrutura hierárquica onde cada nó possui no máximo dois filhos. Essa estrutura permite representar relações hierárquicas, executando operações de inserção, remoção e busca de elementos com eficiência.

- **Principais Propriedades:**  
  - **Raiz:** Nó principal da árvore.  
  - **Folhas:** Nós sem filhos.  
  - **Subárvores:** Cada nó pode ser considerado a raiz de uma subárvore.  
  - **Nível/Profundidade:** A distância (em arestas) do nó até a raiz.  
  - **Altura da Árvore:** A maior profundidade dentre seus nós.

Essas propriedades possibilitam o uso de métodos recursivos para resolver problemas, visto que cada subárvore é, por si só, uma árvore binária.

---

## 2. Tipos de Árvores Binárias

- **Árvore Binária Comum:**  
  Não impõe restrições quanto à ordem dos elementos.

- **Árvore Binária de Busca (BST):**  
  Cada nó satisfaz a propriedade de que todos os nós da subárvore esquerda têm valores menores e os da direita, valores maiores. Esse padrão é amplamente usado para buscas e ordenação.

- **Árvore Binária Completa:**  
  Todos os níveis, exceto possivelmente o último, estão completamente preenchidos; e os nós do último nível estão o mais à esquerda possível.

- **Árvore Binária Balanceada:**  
  O balanço da árvore busca minimizar a altura total, garantindo operações mais eficientes (inserção, remoção, busca).

Compreender essas variações é essencial para escolher a abordagem adequada em desafios de programação, onde restrições de tempo e memória são críticas.

---

## 3. Operações Básicas e Travessias

A manipulação de árvores binárias envolve várias operações, sendo as travessias (traversal) as mais comuns. Existem, principalmente, quatro tipos de travessias:

- **Pré-Ordem (Preorder):** Processa o nó atual, depois a subárvore esquerda e, por fim, a direita.  
- **Em Ordem (Inorder):** Processa a subárvore esquerda, depois o nó atual e, por fim, a subárvore direita. Em BSTs, isso gera uma sequência ordenada.  
- **Pós-Ordem (Postorder):** Processa a subárvore esquerda, depois a direita e, por fim, o nó atual.  
- **Level Order (ou Breadth-First Search - BFS):** Processa os nós nível a nível, de cima para baixo e, em cada nível, da esquerda para a direita.

Esses métodos podem ser implementados de forma recursiva ou iterativa (usando pilhas ou filas), e são frequentemente exigidos em desafios como “Binary Tree Level Order Traversal” ou “Inorder Traversal” em plataformas de desafios.

---

## 4. Exemplos Práticos em Java

### 4.1. Definição da Estrutura do Nó

A base para qualquer operação em árvore é a definição da classe _TreeNode_:

```java
// Definição básica de um nó de árvore binária
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    
    TreeNode(int x) {
        this.val = x;
    }
}
```

### 4.2. Travessias Recursivas

#### Inorder Traversal (Em Ordem)

```java
public void inorderTraversal(TreeNode root) {
    if (root == null) return;
    inorderTraversal(root.left);      // Visita a subárvore esquerda
    System.out.print(root.val + " "); // Processa o nó atual
    inorderTraversal(root.right);     // Visita a subárvore direita
}

public static void main(String[] args) {
    // Exemplo de construção de árvore:
    TreeNode root = new TreeNode(10);
    root.left = new TreeNode(5);
    root.right = new TreeNode(15);
    root.left.left = new TreeNode(2);
    root.left.right = new TreeNode(7);

    // Executa a travessia inorder
    new YourClassName().inorderTraversal(root);
}
```

#### Pré-Ordem Traversal (Pré-Ordem)

```java
public void preorderTraversal(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val + " "); // Processa o nó atual
    preorderTraversal(root.left);     // Visita a subárvore esquerda
    preorderTraversal(root.right);    // Visita a subárvore direita
}
```

#### Pós-Ordem Traversal (Pós-Ordem)

```java
public void postorderTraversal(TreeNode root) {
    if (root == null) return;
    postorderTraversal(root.left);    // Visita a subárvore esquerda
    postorderTraversal(root.right);   // Visita a subárvore direita
    System.out.print(root.val + " "); // Processa o nó atual
}
```

### 4.3. Travessia em Largura (Level Order Traversal)

Esta travessia utiliza uma fila para processar os nós de cada nível:

```java
import java.util.*;

public List<List<Integer>> levelOrderTraversal(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    
    while (!queue.isEmpty()) {
        int levelSize = queue.size();
        List<Integer> currentLevel = new ArrayList<>();
        
        for (int i = 0; i < levelSize; i++) {
            TreeNode node = queue.poll();
            currentLevel.add(node.val);
            
            if (node.left != null) {
                queue.add(node.left);
            }
            if (node.right != null) {
                queue.add(node.right);
            }
        }
        result.add(currentLevel);
    }
    return result;
}

public static void main(String[] args) {
    // Exemplo de construção de árvore:
    TreeNode root = new TreeNode(3);
    root.left = new TreeNode(9);
    root.right = new TreeNode(20);
    root.right.left = new TreeNode(15);
    root.right.right = new TreeNode(7);
    
    List<List<Integer>> traversal = new YourClassName().levelOrderTraversal(root);
    System.out.println("Traversia em largura: " + traversal);
}
```

### 4.4. Problema Comum: Encontrar a Profundidade Máxima da Árvore

Uma técnica recursiva que ilustra bem a ideia de dividir o problema em subárvores:

```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    int leftDepth = maxDepth(root.left);
    int rightDepth = maxDepth(root.right);
    return Math.max(leftDepth, rightDepth) + 1;
}

public static void main(String[] args) {
    // Exemplo de construção de árvore:
    TreeNode root = new TreeNode(1);
    root.left = new TreeNode(2);
    root.right = new TreeNode(3);
    root.left.left = new TreeNode(4);
    
    int depth = new YourClassName().maxDepth(root);
    System.out.println("Profundidade máxima da árvore: " + depth);
}
```

### 4.5. Problema Avançado: Lowest Common Ancestor (LCA)

Determinar o ancestral comum mais baixo de dois nós em uma árvore binária é um desafio comum em entrevistas.

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    
    // Se ambos os lados retornam não nulo, o nó atual é o LCA
    if (left != null && right != null) return root;
    
    // Caso contrário, retorne o lado não nulo
    return left != null ? left : right;
}

public static void main(String[] args) {
    // Construindo uma árvore de exemplo:
    TreeNode root = new TreeNode(3);
    root.left = new TreeNode(5);
    root.right = new TreeNode(1);
    root.left.left = new TreeNode(6);
    root.left.right = new TreeNode(2);
    root.right.left = new TreeNode(0);
    root.right.right = new TreeNode(8);
    root.left.right.left = new TreeNode(7);
    root.left.right.right = new TreeNode(4);
    
    TreeNode p = root.left;  // Nó com valor 5
    TreeNode q = root.left.right.right; // Nó com valor 4
    TreeNode lca = new YourClassName().lowestCommonAncestor(root, p, q);
    System.out.println("Lowest Common Ancestor: " + lca.val);
}
```

---

## 5. Aplicações em Plataformas de Desafios

### Leetcode  
No Leetcode, problemas envolvendo árvores binárias são bastante comuns. Alguns exemplos incluem:  
- **Binary Tree Level Order Traversal:** Exige a utilização de travessia em largura (BFS) para retornar os valores de cada nível da árvore.  
- **Maximum Depth of Binary Tree:** Problema que testa a capacidade de percorrer a árvore e determinar sua profundidade máxima utilizando recursão.  
- **Lowest Common Ancestor of a Binary Tree:** Desafia o candidato a identificar o ancestral comum mais baixo entre dois nós, como mostrado no exemplo acima.

Esses problemas não só avaliam a compreensão dos conceitos de árvore, mas também a habilidade de implementar algoritmos recursivos e iterativos em Java.

### Hackerrank  
No Hackerrank, você pode encontrar desafios como:  
- **Tree: Height of a Binary Tree:** Onde é necessário calcular a altura de uma árvore usando abordagem recursiva.  
- **Tree: Inorder Traversal:** Testando o conhecimento sobre a travessia em ordem e manipulação da estrutura da árvore.

Esses desafios são ideais para reforçar conceitos básicos de árvores e para praticar a escrita de código limpo e eficiente em Java.

### Codesign  
Embora o Codesign (ou plataformas similares focadas em design e algoritmos) esteja mais direcionado para a escrita de soluções elegantes e legíveis, os problemas relacionados a árvores binárias incentivam a aplicação de designs de código eficientes e bem estruturados. A ênfase nesses contextos é a clareza do código, a manutenibilidade e a capacidade de lidar com casos extremos, muitas vezes combinando a árvore binária com outras técnicas, como busca binária ou algoritmos de ordenação.

---

## 6. Considerações Avançadas

### Outras Operações  
Além das travessias e buscas, outros desafios podem exigir:  
- **Inserção e Remoção em BST:** Manter a propriedade ordenada da árvore ao adicionar ou remover elementos.  
- **Balanceamento de Árvores:** Utilização de algoritmos como AVL ou Red-Black Trees para garantir que a árvore permaneça balanceada, garantindo eficiência nas operações.  
- **Serialização e Desserialização:** Converter uma árvore em uma sequência (por exemplo, uma string) e reconstruí-la depois, o que é comum em problemas de persistência de dados.

### Dicas para a Implementação  
- **Tratamento de Casos Especiais:** Sempre verifique se a árvore ou subárvore está vazia (nulo) para evitar exceções.  
- **Utilize Estruturas Auxiliares Quando Necessário:** Em travessias level order, por exemplo, a fila é essencial para manter o controle dos nós do próximo nível.  
- **Teste com Vários Cenários:** Inclua casos com árvores desbalanceadas, árvores vazias e árvores com apenas um nó para garantir a robustez da solução.

---

## 7. Conclusão

O padrão **Binary Tree** é indispensável para solucionar uma vasta gama de problemas em entrevistas e competições de programação. Seu estudo não só permite o domínio das operações básicas e avançadas, mas também incentiva a prática de técnicas recursivas e iterativas que são essenciais para escrever soluções elegantes e eficientes em Java.  

Ao preparar-se utilizando plataformas como Leetcode, Hackerrank e Codesign, você se depara com desafios que exigem desde a implementação de simples travessias até problemas avançados como encontrar o ancestral comum mais baixo (LCA) ou balancear árvores dinâmicas. Cada desafio é uma oportunidade para aprofundar seu entendimento e aprimorar suas habilidades na manipulação de estruturas hierárquicas.

Para ampliar ainda mais seus estudos, explore temas como:
- **Serialização/Desserialização de Árvores:** Muito útil para problemas de persistência e transmissão de estruturas de dados.  
- **Combinação com Algoritmos de Ordenação:** Por exemplo, utilizar BSTs para ordenar dados dinamicamente.  
- **Problemas de Busca e Particionamento:** Como a implementação de algoritmos de busca binária combinados à árvore para solução de problemas complexos.

Com essa base e prática constante, as árvores binárias se tornarão uma ferramenta poderosa e intuitiva em seu arsenal de resolução de problemas. Feliz programação e bons desafios!

# Topological Sort
A ordenação topológica (Topological Sort) é um padrão fundamental para resolver problemas em grafos direcionados acíclicos (DAGs). Esse método consiste em ordenar os vértices de um grafo de forma que para cada aresta direcionada de _u_ para _v_, o vértice _u_ apareça antes de _v_ na ordem. Essa técnica é amplamente aplicada em cenários envolvendo dependências (como agendamento de tarefas ou resolução de pré-requisitos) e é muito comum em desafios de programação em plataformas como Leetcode, Hackerrank e Codesign.

A seguir, vamos explorar esse padrão de forma abrangente, discutindo seus conceitos, algoritmos principais e exemplos completos em Java.

---

## 1. Conceitos Fundamentais

- **Grafos Direcionados Acíclicos (DAG):**  
  A ordenação topológica só é possível se o grafo não possuir ciclos. Em um DAG, não há caminho que comece e termine no mesmo vértice, o que permite definir uma ordem linear válida para os nós.

- **Aplicações Práticas:**  
  - **Agendamento de Tarefas:** Definir uma sequência de execução onde certas tarefas precisam ser concluídas antes de outras.  
  - **Resolução de Pré-requisitos:** Problemas clássicos, como “Course Schedule” no Leetcode, onde cada curso (nó) depende de outros cursos para ser realizado.  
  - **Compilação de Programas:** Ordenar dependências entre módulos para compilar um sistema corretamente.

Esses princípios ajudam a modelar problemas onde há uma dependência implícita entre itens, fornecendo uma “linha do tempo” para a resolução das tarefas.

---

## 2. Algoritmos para Ordenação Topológica

Existem duas abordagens popularmente utilizadas:

### 2.1. Algoritmo de Kahn (BFS)
Este algoritmo utiliza o conceito de **grau de entrada (in-degree)** de cada vértice:
- **Passo 1:** Calcular o in-degree de todos os vértices.  
- **Passo 2:** Enfileirar todos os nós com in-degree igual a zero.  
- **Passo 3:** Enquanto a fila não estiver vazia, retire um vértice, adicione-o à ordem topológica e diminua o in-degree de seus vizinhos. Se algum vizinho atingir in-degree zero, adicione-o à fila.

Essa abordagem é iterativa e, além de gerar a ordenação, possibilita detectar ciclos: se a ordenação não incluir todos os vértices, o grafo possui pelo menos um ciclo.

### 2.2. Algoritmo com DFS
Nesta abordagem, realiza-se uma busca em profundidade (DFS). Durante o percurso:
- **Passo 1:** Visite recursivamente cada vértice não visitado.  
- **Passo 2:** Após visitar todos os vizinhos de um vértice, empilhe-o.  
- **Passo 3:** Ao final, o desempilhamento gera a ordem topológica (porém invertida).

Essa abordagem recursiva é elegante e intuitiva, principalmente para quem domina técnicas de recursão.

---

## 3. Exemplos Práticos em Java

### 3.1. Ordenação Topológica com o Algoritmo de Kahn

```java
import java.util.*;

public class TopologicalSortKahn {
    // Método que retorna a ordem topológica usando o algoritmo de Kahn
    public List<Integer> topologicalSort(int numVertices, List<List<Integer>> adjacencyList) {
        List<Integer> result = new ArrayList<>();
        int[] inDegree = new int[numVertices];

        // Calcular o in-degree de cada vértice
        for (int i = 0; i < numVertices; i++) {
            for (int neighbor : adjacencyList.get(i)) {
                inDegree[neighbor]++;
            }
        }

        // Inicializar a fila com vértices que possuem in-degree 0
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numVertices; i++) {
            if (inDegree[i] == 0) {
                queue.offer(i);
            }
        }

        // Processar os vértices removendo arestas e atualizando in-degrees
        while (!queue.isEmpty()) {
            int vertex = queue.poll();
            result.add(vertex);

            for (int neighbor : adjacencyList.get(vertex)) {
                inDegree[neighbor]--;
                if (inDegree[neighbor] == 0) {
                    queue.offer(neighbor);
                }
            }
        }

        // Se o tamanho do resultado for menor do que o número de vértices,
        // significa que houve ciclo, pois nem todos os vértices foram processados.
        if (result.size() != numVertices) {
            throw new IllegalArgumentException("O grafo possui ciclo e não é um DAG.");
        }

        return result;
    }

    public static void main(String[] args) {
        // Exemplo de grafo:
        // 0 -> 1, 0 -> 2, 1 -> 3, 2 -> 3
        int numVertices = 4;
        List<List<Integer>> adjacencyList = new ArrayList<>();
        for (int i = 0; i < numVertices; i++) {
            adjacencyList.add(new ArrayList<>());
        }
        adjacencyList.get(0).add(1);
        adjacencyList.get(0).add(2);
        adjacencyList.get(1).add(3);
        adjacencyList.get(2).add(3);

        TopologicalSortKahn sorter = new TopologicalSortKahn();
        try {
            List<Integer> topoOrder = sorter.topologicalSort(numVertices, adjacencyList);
            System.out.println("Ordem Topológica (Kahn's): " + topoOrder);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

**Como Funciona:**  
No exemplo acima, calculamos o grau de entrada de cada vértice e utilizamos uma fila para processar os vértices sem dependências. Ao remover cada vértice, atualizamos os graus dos vizinhos, garantindo a correta atualização da ordem. Caso o grafo possua um ciclo, a ordem pode ser inválida e o algoritmo lança uma exceção.

---

### 3.2. Ordenação Topológica com DFS

```java
import java.util.*;

public class TopologicalSortDFS {

    // Método que retorna a ordem topológica usando DFS
    public List<Integer> topologicalSort(int numVertices, List<List<Integer>> adjacencyList) {
        boolean[] visited = new boolean[numVertices];
        Stack<Integer> stack = new Stack<>();

        // Executa DFS em cada vértice não visitado
        for (int i = 0; i < numVertices; i++) {
            if (!visited[i]) {
                dfs(i, visited, stack, adjacencyList);
            }
        }

        // Desempilha os vértices para obter a ordem topológica
        List<Integer> result = new ArrayList<>();
        while (!stack.isEmpty()) {
            result.add(stack.pop());
        }

        return result;
    }

    private void dfs(int vertex, boolean[] visited, Stack<Integer> stack, List<List<Integer>> adjacencyList) {
        visited[vertex] = true;

        for (int neighbor : adjacencyList.get(vertex)) {
            if (!visited[neighbor]) {
                dfs(neighbor, visited, stack, adjacencyList);
            }
        }
        // Empilha o vértice após visitar seus vizinhos
        stack.push(vertex);
    }

    public static void main(String[] args) {
        // Exemplo de grafo:
        // 0 -> 1, 0 -> 2, 1 -> 3, 2 -> 3
        int numVertices = 4;
        List<List<Integer>> adjacencyList = new ArrayList<>();
        for (int i = 0; i < numVertices; i++) {
            adjacencyList.add(new ArrayList<>());
        }
        adjacencyList.get(0).add(1);
        adjacencyList.get(0).add(2);
        adjacencyList.get(1).add(3);
        adjacencyList.get(2).add(3);

        TopologicalSortDFS sorter = new TopologicalSortDFS();
        List<Integer> topoOrder = sorter.topologicalSort(numVertices, adjacencyList);
        System.out.println("Ordem Topológica (DFS): " + topoOrder);
    }
}
```

**Como Funciona:**  
Neste exemplo a abordagem é recursiva. Cada vértice é processado via DFS e, ao retornar da recursão, o vértice é empilhado. Desempilhando os vértices, obtemos uma ordem válida que respeita as dependências entre eles.

---

## 4. Aplicações em Plataformas de Desafios

### Leetcode
No Leetcode, problemas envolvendo ordenação topológica são comuns, principalmente em cenários de resolução de dependências. Exemplos de problemas:

- **Course Schedule / Course Schedule II:**  
  Estes problemas envolvem determinar se é possível completar todos os cursos dados os pré-requisitos e, em alguns casos, retornar uma sequência que satisfaça essa condição.  
- **Alien Dictionary:**  
  Estabelecer a ordem das letras de um alfabeto desconhecido com base em uma lista ordenada de palavras requer a definição de dependências entre caracteres.

Ambos os tipos de problemas incentivam o uso de algoritmos de ordenação topológica para validar e construir a sequência de execução.

### Hackerrank  
No Hackerrank, você pode encontrar problemas que envolvem:
- **Agendamento de Tarefas com Dependências:**  
  Modelar tarefas interdependentes e determinar a ordem correta para sua execução pode ser resolvido utilizando a ordenação topológica.  
- **Construção de Pipelines de Processamento:**  
  Problemas que exigem definir uma ordem para execução de processos com restrições de dependências, onde a abordagem de Kahn ou DFS pode ser aplicada.

### Codesign  
Plataformas voltadas para design de código e algoritmos, como o Codesign, valorizam soluções elegantes e legíveis. A implementação de ordenação topológica nesse contexto sublinha a importância do design e modularização do código. A clareza do algoritmo, a manipulação correta de casos de ciclo e a documentação da solução são pontos frequentemente avaliados.

---

## 5. Considerações Avançadas e Dicas

- **Detecção de Ciclos:**  
  Um grafo que contenha ciclos não pode ser ordenado topologicamente. Em Kahn, isso é indicado quando a quantidade de vértices processados é menor do que o total. Em DFS, mecanismos adicionais (como manter um status de “visitando” vs “visitado”) podem ajudar a identificar ciclos durante a recursão.

- **Escolha da Abordagem:**  
  - **Kahn (BFS)**: É vantajoso quando se deseja iterar e acompanhar explicitamente os graus de entrada dos nós.  
  - **DFS:** Oferece uma implementação recursiva elegante e pode ser mais intuitiva para alguns problemas.

- **Complexidade:**  
  Ambas as abordagens têm complexidade O(V + E), onde V é o número de vértices e E é o número de arestas, sendo eficientes para grafos esparsos e densos.

- **Aplicação Híbrida:**  
  Em casos mais complexos, a ordenação topológica pode ser combinada com outras técnicas (como busca binária em problemas de escalonamento) para otimizar soluções.

---

## 6. Conclusão

A ordenação topológica é uma ferramenta poderosa para lidar com problemas envolvendo dependências e relações de precedência em grafos direcionados acíclicos. Seja através do algoritmo de Kahn – que utiliza uma abordagem iterativa via BFS – ou da técnica baseada em DFS, compreender e implementar esse padrão é fundamental para superar desafios encontrados em plataformas como Leetcode, Hackerrank e Codesign.

Através dos exemplos em Java apresentados, você pode praticar a implementação de ambos os métodos e aplicar esse conhecimento em cenários reais, tais como resolução de pré-requisitos em cursos, agendamentos de tarefas e decodificação de alfabetos desconhecidos. Ao dominar a ordenação topológica, você enriquece seu arsenal de técnicas e se prepara para solucionar problemas complexos de forma eficiente e elegante.

Caso deseje explorar mais o tema, você pode investigar técnicas para detectar ciclos de forma mais robusta, aplicar a ordenação topológica para resolver problemas de planejamento e até explorar variações que integrem outras estratégias, como a combinação com algoritmos de otimização ou análise de complexidade em grandes grafos.

Bons estudos e sucesso nos desafios de programação!

# Binary Tree DFS
A abordagem de **Binary Tree DFS** (Depth-First Search em Árvore Binária) é um padrão essencial para resolver problemas envolvendo estruturas hierárquicas, onde a exploração profunda de cada ramo (ou caminho) é a chave para encontrar soluções. Essa técnica se destaca tanto em algoritmos recursivos quanto iterativos e é amplamente utilizada em desafios nas plataformas Leetcode, Hackerrank e Codesign. A seguir, apresentamos um conteúdo abrangente sobre esse padrão acompanhado de exemplos em Java.

---

## 1. Introdução ao Binary Tree DFS

A **DFS (Depth-First Search)** é uma estratégia de busca que, em uma árvore binária, explora um ramo o máximo possível antes de voltar (backtracking) e percorrer outros ramos. Ela é natural para estruturas recursivas como as árvores, pois cada nó se comporta como a raiz de uma subárvore. Essa abordagem permite:

- **Processar a árvore em diferentes ordens:**  
  - **Preorder (Pré-Ordem):** Processa o nó atual e depois seus ramos esquerdo e direito.  
  - **Inorder (Em Ordem):** Processa o ramo esquerdo, depois o nó atual e por fim o ramo direito. Em árvores de busca binária (BST), essa ordem gera uma sequência ordenada.  
  - **Postorder (Pós-Ordem):** Processa os ramos esquerdo e direito antes do nó atual.
  
- **Resolver diversos problemas:**  
  - Verificação de propriedades da árvore (ex.: árvore simétrica, balanceamento).  
  - Cálculo de métricas, como profundidade máxima, soma de nós em um caminho, entre outros.  
  - Geração de caminhos da raiz até as folhas (útil em problemas do tipo “root-to-leaf path”).

---

## 2. Por que Usar DFS em Árvores Binárias?

A aplicação do DFS em árvores binárias traz vantagens em termos de clareza e eficiência:

- **Simplicidade Recursiva:**  
  A natureza recursiva de uma árvore torna a implementação do DFS muito intuitiva. Ao processar um nó, você automaticamente resolve os problemas para sua subárvore esquerda e direita.

- **Eficiência:**  
  A complexidade de tempo é geralmente O(n), onde n é o número de nós da árvore, já que cada nó é visitado exatamente uma vez.

- **Flexibilidade:**  
  Com DFS, é possível adaptar o algoritmo para diversas tarefas, como gerar caminhos, calcular profundidades, identificar nós específicos e até combinar com técnicas de backtracking para resolver problemas mais complexos.

---

## 3. Abordagens para DFS em Árvores Binárias

### 3.1. DFS Recursivo

A forma mais comum de implementar DFS em uma árvore é por meio da recursão. Dentre as travessias, podemos destacar:

#### a) Preorder Traversal (Pré-Ordem)
Processa o nó atual antes de explorar os filhos.

```java
public void preorder(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val + " "); // Processa o nó atual
    preorder(root.left);              // Visita o ramo esquerdo
    preorder(root.right);             // Visita o ramo direito
}
```

#### b) Inorder Traversal (Em Ordem)
Processa o ramo esquerdo, depois o nó e, por fim, o ramo direito.

```java
public void inorder(TreeNode root) {
    if (root == null) return;
    inorder(root.left);               // Visita o ramo esquerdo
    System.out.print(root.val + " "); // Processa o nó atual
    inorder(root.right);              // Visita o ramo direito
}
```

#### c) Postorder Traversal (Pós-Ordem)
Processa os ramos esquerdo e direito antes do nó atual.

```java
public void postorder(TreeNode root) {
    if (root == null) return;
    postorder(root.left);             // Visita o ramo esquerdo
    postorder(root.right);            // Visita o ramo direito
    System.out.print(root.val + " "); // Processa o nó atual
}
```

### 3.2. DFS Iterativo com Pilha

Embora a recursão seja natural, em alguns casos é interessante usar uma abordagem iterativa para evitar limitações com a pilha de chamadas (stack overflow em árvores muito profundas). Utilizando uma estrutura de pilha, podemos simular o comportamento recursivo.

#### Exemplo de Pré-Ordem Iterativo:

```java
import java.util.Stack;

public void iterativePreorder(TreeNode root) {
    if (root == null) return;
    
    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);
    
    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        System.out.print(node.val + " ");
        
        // Empilha primeiro o nó direito, depois o esquerdo, 
        // para que o nó esquerdo seja processado antes
        if (node.right != null) {
            stack.push(node.right);
        }
        if (node.left != null) {
            stack.push(node.left);
        }
    }
}
```

---

## 4. Exemplos Práticos em Java

Antes de explorar os exemplos, a estrutura básica para um nó de árvore (TreeNode) pode ser definida da seguinte forma:

```java
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    
    public TreeNode(int x) {
        this.val = x;
    }
}
```

### 4.1. Exemplo Completo: Traversals DFS Recursivos

```java
public class BinaryTreeDFS {
    
    // Pré-Ordem
    public void preorder(TreeNode root) {
        if (root == null) return;
        System.out.print(root.val + " ");
        preorder(root.left);
        preorder(root.right);
    }
    
    // Em Ordem
    public void inorder(TreeNode root) {
        if (root == null) return;
        inorder(root.left);
        System.out.print(root.val + " ");
        inorder(root.right);
    }
    
    // Pós-Ordem
    public void postorder(TreeNode root) {
        if (root == null) return;
        postorder(root.left);
        postorder(root.right);
        System.out.print(root.val + " ");
    }
    
    // Exemplo de uso
    public static void main(String[] args) {
        /*
                10
               /  \
              5    15
             / \     \
            2   7     20
        */
        TreeNode root = new TreeNode(10);
        root.left = new TreeNode(5);
        root.right = new TreeNode(15);
        root.left.left = new TreeNode(2);
        root.left.right = new TreeNode(7);
        root.right.right = new TreeNode(20);
        
        BinaryTreeDFS solver = new BinaryTreeDFS();
        
        System.out.print("Pré-Ordem: ");
        solver.preorder(root);    // Saída esperada: 10 5 2 7 15 20
        System.out.println();
        
        System.out.print("Em Ordem: ");
        solver.inorder(root);     // Saída esperada: 2 5 7 10 15 20
        System.out.println();
        
        System.out.print("Pós-Ordem: ");
        solver.postorder(root);   // Saída esperada: 2 7 5 20 15 10
        System.out.println();
    }
}
```

### 4.2. Exemplo Completo: DFS Iterativo (Pré-Ordem)

```java
import java.util.Stack;

public class BinaryTreeDFSIterativo {
    
    public void iterativePreorder(TreeNode root) {
        if (root == null) return;
        
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            System.out.print(node.val + " ");
            
            // Empilha primeiro o filho direito para garantir que o esquerdo seja processado primeiro
            if (node.right != null) {
                stack.push(node.right);
            }
            if (node.left != null) {
                stack.push(node.left);
            }
        }
    }
    
    public static void main(String[] args) {
        /*
                1
               / \
              2   3
             / \   
            4   5  
        */
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        
        BinaryTreeDFSIterativo solver = new BinaryTreeDFSIterativo();
        System.out.print("Iterative Preorder: ");
        solver.iterativePreorder(root); // Saída esperada: 1 2 4 5 3
    }
}
```

### 4.3. Aplicação Prática: Verificar o Caminho de Soma (Path Sum)

Um problema comum envolve determinar se existe algum caminho da raiz até uma folha cuja soma dos valores seja igual a um alvo fornecido. Esse problema pode ser resolvido com DFS (usando abordagem recursiva com backtracking):

```java
public class PathSumDFS {
    
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) return false;
        
        // Se é uma folha, verifica se a soma restante é igual ao valor do nó
        if (root.left == null && root.right == null) {
            return sum == root.val;
        }
        
        // Subtrai o valor do nó do sum e propaga pela árvore
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
    
    public static void main(String[] args) {
        /*
                5
               / \
              4   8
             /   / \
            11  13  4
           /  \      \
          7    2      1
        */
        TreeNode root = new TreeNode(5);
        root.left = new TreeNode(4);
        root.right = new TreeNode(8);
        root.left.left = new TreeNode(11);
        root.left.left.left = new TreeNode(7);
        root.left.left.right = new TreeNode(2);
        root.right.left = new TreeNode(13);
        root.right.right = new TreeNode(4);
        root.right.right.right = new TreeNode(1);
        
        PathSumDFS solver = new PathSumDFS();
        int targetSum = 22;
        boolean exists = solver.hasPathSum(root, targetSum);
        System.out.println("Existe um caminho com a soma " + targetSum + "? " + exists);
    }
}
```

---

## 5. Aplicações em Plataformas como Leetcode, Hackerrank e Codesign

- **Leetcode:** Problemas como *Binary Tree Inorder Traversal*, *Path Sum*, *Symmetric Tree* e *Diameter of Binary Tree* fazem uso pesado do DFS para percorrer, buscar e calcular propriedades de árvores. A abordagem DFS é quase que padrão para muitas soluções elegantes que exigem percorrer todos os nós.

- **Hackerrank:** Nos desafios do Hackerrank, tarefas envolvendo travessias recursivas (trees e grafos) costumam utilizar DFS para obter soluções simples e legíveis, com ênfase no uso correto da recursão e no manuseio de casos de borda.

- **Codesign:** Em plataformas voltadas para design e algoritmos, a clareza e eficiência do código DFS é essencial. A implementação bem estruturada utilizando DFS demonstra habilidades em decompor problemas complexos, lidar com backtracking e manter um design modular.

---

## 6. Considerações Avançadas

- **Backtracking:**  
  Em problemas que exigem a geração de todos os caminhos ou combinações (como encontrar todos os caminhos da raiz até as folhas), DFS combinado com backtracking permite explorar e desfazer escolhas de forma organizada.

- **Controle de Estado:**  
  Em implementações recursivas, é fundamental garantir que o estado (por exemplo, a lista de valores do caminho atual) seja manipulado com cuidado para evitar efeitos colaterais e garantir que os resultados sejam acumulados corretamente.

- **Limitações da Recursão:**  
  Em árvores muito profundas, a abordagem recursiva pode levar a um estouro da pilha. Nesses casos, a implementação iterativa com pilha pode ser preferível.

- **Combinação com Outras Técnicas:**  
  DFS pode ser integrada a algoritmos de divisão e conquista, ou utilizada para pré-processamento antes de outras operações, ampliando seu uso em problemas complexos.

---

## 7. Conclusão

O padrão **Binary Tree DFS** é uma técnica crucial para a manipulação de árvores binárias, permitindo explorar profundamente cada caminho e resolver uma ampla gama de problemas. Seja por meio de implementações recursivas – que refletem a natureza hierárquica das árvores – ou por abordagens iterativas utilizando pilha, o DFS oferece soluções eficientes e elegantes para desafios frequentes em plataformas como Leetcode, Hackerrank e Codesign.

Ao dominar esse padrão, você estará preparado para enfrentar problemas que vão desde simples travessias (preorder, inorder, postorder) até soluções mais sofisticadas como verificação de caminhos com soma específica, cálculo do diâmetro da árvore e outras tarefas que exigem o processamento completo de cada nó da árvore.

Experimente adaptar os exemplos apresentados, explorar variações (como geração de caminhos e aplicação do backtracking) e ajuste seu código para lidar com casos extremos. Essa prática não só reforça o domínio sobre DFS em árvores binárias, mas também aprimora suas habilidades para resolver problemas complexos em ambientes de competição e entrevistas.

Bons estudos e excelente codificação!

# Top K Elements
O pattern **Top K Elements** é uma estratégia essencial para resolver problemas onde precisamos extrair os *K* maiores (ou menores) elementos de uma coleção, ou mesmo identificar os elementos mais frequentes em um conjunto de dados. Essa abordagem é muito comum em desafios e entrevistas nas plataformas Leetcode, Hackerrank e Codesign, aparecendo em problemas como "Kth Largest Element in an Array" e "Top K Frequent Elements". A seguir, vamos explorar de maneira abrangente esse padrão, suas abordagens e aplicações, com exemplos práticos em Java.

---

## 1. Conceito e Aplicações do Pattern

### O que é o Top K Elements?  
O objetivo do padrão é identificar, dentre um conjunto de elementos, os *K* que possuem uma determinada propriedade de "maior relevância". Essa relevância pode ser definida por:
- **Valor Numérico:** Exemplo, os *K* maiores ou menores números em um array.
- **Frequência:** Exemplo, os *K* elementos que aparecem com maior frequência em um array ou uma lista de palavras.
- **Outros critérios customizados:** Podem incluir prioridades determinadas por atributos, datas, pontuações, entre outros.

### Por que usamos esse Pattern?  
- **Eficiência:** Em muitas situações, ordenar toda a coleção para depois extrair os *K* elementos não é necessário e pode ser custoso, sobretudo quando o número de elementos é muito grande.
- **Escalabilidade:** Abordagens com heaps (filas de prioridade) ou algoritmos de seleção (quickselect) possuem complexidades que podem ser lineares ou próximas, o que é ideal para grandes conjuntos de dados.
- **Aplicabilidade:** Muitas vezes, o problema pode ser modelado para manter um conjunto dinâmico dos *K* melhores itens conforme novos dados chegam (por exemplo, exibir os *K* produtos mais vendidos em tempo real).

---

## 2. Abordagens para Resolver o Problema

### 2.1. Usando Ordenação Completa  
A solução mais simples é ordenar a coleção inteira e pegar os primeiros ou últimos *K* elementos.  
- **Vantagens:** Implementação simples.  
- **Desvantagens:** Complexidade de tempo O(n log n), o que pode não ser ideal para grandes conjuntos de dados.

### 2.2. Usando Heaps (Filas de Prioridade)  
A ideia é manter um heap (geralmente um *min-heap* para os *K* maiores ou um *max-heap* para os *K* menores) que armazena somente os *K* melhores elementos conforme se percorre a coleção.  
- **Vantagens:** Complexidade O(n log K), que para k muito pequeno comparado a n é bastante eficiente.  
- **Desvantagens:** Implementação um pouco mais complexa do que simplesmente ordenar.

### 2.3. Quickselect  
O algoritmo Quickselect permite encontrar o *k*–ésimo elemento (daí podemos extrair os *K* maiores ou menores) com complexidade média O(n).  
- **Vantagens:** Excelente para resolver o problema de encontrar o elemento *K*-ésimo.  
- **Desvantagens:** Caso a estabilidade e todos os *K* elementos sejam necessários, pode ser necessário ajustar a implementação.

---

## 3. Exemplos Práticos em Java

### 3.1. Exemplo: Encontrando os *K* Maiores Elementos Usando Min-Heap

Nesta abordagem, percorremos um array e mantemos um min-heap que nunca tem mais do que *K* elementos. Assim, o menor dos *K* maiores sempre estará na raiz e, quando encontramos um número maior, substituímos o elemento de menor valor.

```java
import java.util.*;

public class TopKElementsHeap {
    
    // Retorna uma lista com os K maiores elementos do array
    public List<Integer> findTopK(int[] arr, int k) {
        // Usamos um min-heap para manter os K maiores números
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        
        for (int num : arr) {
            minHeap.offer(num);
            // Se o heap tem mais do que k elementos, removemos o menor
            if(minHeap.size() > k) {
                minHeap.poll();
            }
        }
        
        // Converte o heap em lista e ordena em ordem decrescente, se necessário
        List<Integer> topK = new ArrayList<>(minHeap);
        topK.sort(Collections.reverseOrder());
        return topK;
    }
    
    public static void main(String[] args) {
        int[] arr = {5, 12, 11, -1, 12, 13, 14, 2, 3};
        int k = 4;
        TopKElementsHeap solver = new TopKElementsHeap();
        List<Integer> result = solver.findTopK(arr, k);
        System.out.println("Top " + k + " elements: " + result);
    }
}
```

**Como Funciona:**  
- Percorremos cada elemento do array e o inserimos no min-heap.
- Caso o tamanho do heap ultrapasse *K*, removemos o menor elemento.
- Ao final, o heap contém os *K* maiores elementos e podemos convertê-lo em uma lista.

---

### 3.2. Exemplo: Top K Frequent Elements

Problema comum em plataformas como Leetcode, onde é necessário encontrar os *K* elementos mais frequentes em um array.

```java
import java.util.*;

public class TopKFrequentElements {

    public int[] topKFrequent(int[] nums, int k) {
        // Mapeia cada número à sua frequência
        Map<Integer, Integer> frequencyMap = new HashMap<>();
        for (int num : nums) {
            frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
        }
        
        // Min-heap baseado na frequência
        PriorityQueue<Map.Entry<Integer, Integer>> minHeap = 
            new PriorityQueue<>((a, b) -> a.getValue() - b.getValue());
        
        // Insere no heap e mantém o tamanho em k
        for (Map.Entry<Integer, Integer> entry : frequencyMap.entrySet()) {
            minHeap.offer(entry);
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }
        
        // Extrai as chaves dos elementos restantes no heap
        int[] result = new int[k];
        for (int i = k - 1; i >= 0; i--) {
            result[i] = minHeap.poll().getKey();
        }
        return result;
    }
    
    public static void main(String[] args) {
        TopKFrequentElements solver = new TopKFrequentElements();
        int[] nums = {1, 1, 1, 2, 2, 3};
        int k = 2;
        int[] res = solver.topKFrequent(nums, k);
        System.out.println("Top " + k + " frequent elements: " + Arrays.toString(res));
    }
}
```

**Como Funciona:**  
- Primeiro, conta-se a frequência de cada elemento usando um `HashMap`.
- Em seguida, utiliza-se um min-heap que armazena entradas do mapa (par número e frequência). Mantemos somente *K* entradas com maiores frequências.
- Finalmente, extraímos as chaves para formar o resultado.

---

### 3.3. Exemplo Avançado: Kth Largest Element Usando Quickselect

Para encontrar o *k*-ésimo maior elemento (o que pode ser adaptado para extrair os Top K, se necessário), podemos utilizar o algoritmo Quickselect.

```java
public class KthLargestUsingQuickSelect {
    
    public int kthLargest(int[] nums, int k) {
        int left = 0;
        int right = nums.length - 1;
        // O kth largest corresponde ao elemento na posição nums.length - k
        int target = nums.length - k;
        
        while (true) {
            int pivotIndex = partition(nums, left, right);
            if (pivotIndex == target) {
                return nums[pivotIndex];
            } else if (pivotIndex < target) {
                left = pivotIndex + 1;
            } else {
                right = pivotIndex - 1;
            }
        }
    }

    private int partition(int[] nums, int left, int right) {
        int pivot = nums[right];
        int i = left;
        for (int j = left; j < right; j++) {
            if (nums[j] <= pivot) {
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
                i++;
            }
        }
        int temp = nums[i];
        nums[i] = nums[right];
        nums[right] = temp;
        return i;
    }
    
    public static void main(String[] args) {
        int[] nums = {3, 2, 1, 5, 6, 4};
        int k = 2;
        KthLargestUsingQuickSelect solver = new KthLargestUsingQuickSelect();
        int kth = solver.kthLargest(nums, k);
        System.out.println(k + "º largest element is: " + kth);
    }
}
```

**Como Funciona:**  
- O algoritmo utiliza a ideia do particionamento (semelhante ao quicksort) para encontrar a posição correta do pivô.
- Com isso, decidimos se o elemento procurado (na posição `n - k`) está à esquerda ou à direita e ajustamos os limites da busca, até encontrarmos o *k*-ésimo maior elemento.

---

## 4. Aplicações em Plataformas de Desafios

### Leetcode  
- **Top K Frequent Elements:** Um dos problemas mais comuns que exige extrair os elementos mais frequentes utilizando heaps.  
- **Kth Largest Element in an Array:** Um problema que pode ser resolvido usando min-heap ou quickselect.

### Hackerrank  
- Desafios que envolvem “finding the top K items”, como análises de dados, classificação e extração de estatísticas, aproveitam esse pattern para reduzir a complexidade.
- Problemas de perguntas em que é preciso atualizar continuamente os *K* melhores resultados em fluxos de dados, exemplificando o uso de um heap dinâmico.

### Codesign  
- Em plataformas voltadas à escrita de código elegante e manutenível, o uso do pattern Top K Elements demonstra uma boa compreensão de estruturas de dados como heaps, além de mostrar habilidades de otimização e design modular da solução, especialmente em casos onde a eficiência e clareza do código são fatores críticos.

---

## 5. Considerações Avançadas e Dicas

- **Escolha do Heap:**  
  Geralmente, para extrair os *K* maiores elementos, use um min-heap para que o menor dentre os *K* seja sempre substituído caso encontre um valor maior. Para os *K* menores, opte por um max-heap.

- **Uso do Quickselect:**  
  Se o objetivo for encontrar apenas o *k*-ésimo elemento, o Quickselect pode oferecer uma solução com complexidade média linear, evitando a sobrecarga de um heap.

- **Manutenção Dinâmica:**  
  Em situações com fluxos de dados ou atualizações contínuas, mantenha um heap de tamanho fixo *K* para facilmente atualizar os melhores *K* elementos conforme novos dados chegam.

- **Validação de Entrada:**  
  Sempre valide se o valor de *K* é compatível com o tamanho da coleção e trate casos extremos para evitar erros de execução.

---

## 6. Conclusão

O pattern **Top K Elements** é uma poderosa técnica para extrair informações relevantes de um conjunto de dados sem precisar ordenar ou processar toda a coleção de forma completa. Seja utilizando heaps, quickselect ou outras estratégias, esse padrão se mostra indispensável em desafios e entrevistas, permitindo a resolução de problemas com eficiência e clareza.

Ao dominar e adaptar essas abordagens em Java, você estará preparado para enfrentar questões em plataformas como Leetcode, Hackerrank e Codesign, aplicando soluções escaláveis e elegantes para extração dos *K* melhores itens, seja por valor, frequência ou outros critérios.  

Explore variações do problema, experimente com conjuntos dinâmicos e integre esse padrão a outros algoritmos para expandir ainda mais seu arsenal de soluções. Bons estudos e excelente codificação!

# Modified Binary Search
O padrão **Modified Binary Search** é uma adaptação do tradicional algoritmo de busca binária para resolver problemas que, embora requeiram a eficiência da busca binária, não podem ser abordados de forma direta devido a restrições ou características especiais dos dados. Em muitas situações de desafios em plataformas como Leetcode, Hackerrank e Codesign, os problemas exigem que façamos pequenas (ou grandes) modificações nas condições de parada, na forma de atualizar os ponteiros ou até na forma de interpretar o meio da busca. Essa abordagem permite que se mantenha a complexidade logarítmica (O(log n)) mesmo em cenários aparentemente complicados.

Neste conteúdo, vamos explorar os conceitos fundamentais do Modified Binary Search, identificar os cenários em que esse padrão é aplicável e demonstrar exemplos práticos em Java.

---

## 1. Conceitos e Motivação

### 1.1. Revisão: Busca Binária Padrão

A busca binária tradicional é utilizada em listas (ou arrays) ordenadas para localizar um elemento alvo. Partindo de um índice médio, ela decide se o elemento procurado está à esquerda ou à direita do meio e, recurisvelmente (ou iterativamente), descarta metade dos elementos até encontrar o valor desejado ou esgotar as possibilidades.

**Exemplo simples (pseudocódigo):**

```java
int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if(arr[mid] == target) return mid;
        else if(arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

### 1.2. Quando Modificar a Busca Binária?

Em muitos problemas encontramos condições que fogem do cenário “array ordenado em ordem crescente” onde a busca tradicional é aplicada. Veja alguns cenários comuns para aplicar modificações:

- **Array Rotacionado:**  
  O array inicialmente ordenado foi rotacionado em algum ponto (ex.: [4, 5, 6, 7, 0, 1, 2]). O desafio é identificar em qual parte do array o valor alvo se encontra.

- **Busca de Valor Mínimo/ Máximo:**  
  Em problemas como “Find Minimum in Rotated Sorted Array” ou “Peak Element” (elemento que é maior que seus vizinhos) em uma “mountain array”, o objetivo pode ser encontrar o ponto de mudança ou o ponto máximo/minimo.

- **Busca de Primeira/Última Ocorrência:**  
  Quando um array contém elementos duplicados, pode ser necessário adaptar a busca para retornar, por exemplo, a primeira ou a última posição de um elemento.

- **Problemas com Predicados Customizados:**  
  Em situações onde a “ordem” é definida por uma condição ou função (por exemplo, encontrar o menor valor que satisfaça um dado predicado), a atualização dos ponteiros deve ser feita de forma apropriada.

Em todas essas variações o desejo é aproveitar a eficiência logarítmica da busca binária, mas adaptando o algoritmo para que ele se comporte de acordo com a lógica exigida pelo problema.

---

## 2. Abordagens e Exemplos Práticos

A seguir, veremos alguns exemplos de Modified Binary Search em Java.

### 2.1. Exemplo: Busca em Array Rotacionado

**Problema:**  
Dado um array ordenado que foi rotacionado (por exemplo, `[4, 5, 6, 7, 0, 1, 2]`), localizar um determinado elemento (por exemplo, `0`) e retornar seu índice.

**Abordagem:**  
Ao invés de comparar apenas com o elemento do meio, verificamos em qual metade do array a ordenação continua e adaptamos os ponteiros conforme essa verificação.

```java
public class RotatedSortedArraySearch {

    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        
        while(left <= right) {
            int mid = left + (right - left) / 2;
            
            // Se encontramos o target, retorne o índice
            if(nums[mid] == target) {
                return mid;
            }
            
            // Se a parte da esquerda é ordenada
            if(nums[left] <= nums[mid]) {
                // Se o target está na metade ordenada
                if(nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } 
            // Caso contrário, a parte direita é ordenada
            else {
                if(nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        return -1;
    }
    
    public static void main(String[] args) {
        RotatedSortedArraySearch solver = new RotatedSortedArraySearch();
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int target = 0;
        int index = solver.search(nums, target);
        System.out.println("Índice do target " + target + ": " + index);
    }
}
```

**Como Funciona:**  
Neste exemplo, a cada iteração verificamos se o segmento [left, mid] está ordenado. Se estiver, determinamos se o target se encontra nesse intervalo para atualizar os ponteiros; caso contrário, ajustamos para o segmento [mid + 1, right]. Essa modificação garante que a busca seja eficaz mesmo com a rotação do array.

---

### 2.2. Exemplo: Encontrar o Mínimo em um Array Rotacionado

**Problema:**  
Dado um array rotacionado (ex.: `[4, 5, 6, 7, 0, 1, 2]`), encontrar o valor mínimo do array.

**Abordagem:**  
Utilizamos uma variação da busca binária para identificar o ponto de inflexão onde a rotação ocorreu.

```java
public class FindMinInRotatedSortedArray {

    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        
        // Se o array não estiver rotacionado
        if(nums[left] <= nums[right]) {
            return nums[left];
        }
        
        while(left < right) {
            int mid = left + (right - left) / 2;
            
            // Se o valor do meio é maior do que o valor da direita,
            // o mínimo está na metade direita.
            if(nums[mid] > nums[right]) {
                left = mid + 1;
            } else {
                // caso contrário, o mínimo está na metade esquerda
                right = mid;
            }
        }
        return nums[left];
    }
    
    public static void main(String[] args) {
        FindMinInRotatedSortedArray solver = new FindMinInRotatedSortedArray();
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int minValue = solver.findMin(nums);
        System.out.println("O valor mínimo é: " + minValue);
    }
}
```

**Como Funciona:**  
A condição modificada compara o elemento do meio com o elemento da direita. Se for maior, significa que a parte esquerda possui os maiores valores e o ponto de rotação (mínimo) está na parte direita. Dessa forma, convergimos para o menor elemento.

---

### 2.3. Exemplo: Buscar a Primeira e Última Ocorrência de um Elemento

**Problema:**  
Dado um array ordenado com elementos duplicados, encontrar a posição da primeira e da última ocorrência de um determinado target.

**Abordagem:**  
Utiliza-se duas variações da busca binária: uma para encontrar a primeira posição e outra para a última, modificando a condição de atualização dos ponteiros quando se encontra o target.

```java
public class FirstAndLastPosition {
    
    public int[] searchRange(int[] nums, int target) {
        int first = findFirst(nums, target);
        int last = findLast(nums, target);
        return new int[]{first, last};
    }
    
    private int findFirst(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int index = -1;
        while(left <= right) {
            int mid = left + (right - left) / 2;
            if(nums[mid] >= target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
            if(nums[mid] == target) index = mid;
        }
        return index;
    }
    
    private int findLast(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int index = -1;
        while(left <= right) {
            int mid = left + (right - left) / 2;
            if(nums[mid] <= target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
            if(nums[mid] == target) index = mid;
        }
        return index;
    }
    
    public static void main(String[] args) {
        FirstAndLastPosition solver = new FirstAndLastPosition();
        int[] nums = {2, 4, 4, 4, 6, 6, 8};
        int target = 4;
        int[] range = solver.searchRange(nums, target);
        System.out.println("Primeira e última posição do elemento " + target + ": [" + range[0] + ", " + range[1] + "]");
    }
}
```

**Como Funciona:**  
- Na função `findFirst`, sempre que o valor do meio é maior ou igual ao target, movemos o ponteiro direito para continuar a busca pela primeira ocorrência.  
- Na função `findLast`, se o valor do meio é menor ou igual ao target, movemos o ponteiro esquerdo para continuar a busca pela última ocorrência.

---

### 2.4. Exemplo: Busca em uma “Mountain Array” (Peak Element)

**Problema:**  
Dado um array em que os elementos aumentam até um certo ponto (o pico) e depois decrescem, encontrar o índice do pico.

**Abordagem:**  
Utilizamos uma modificação da busca binária para identificar quando o elemento do meio é maior que seu vizinho direito, indicando que estamos na parte decrescente e que o pico pode estar ali ou à esquerda.

```java
public class PeakIndexInMountainArray {

    public int peakIndexInMountainArray(int[] arr) {
        int left = 0, right = arr.length - 1;
        while(left < right) {
            int mid = left + (right - left) / 2;
            if(arr[mid] < arr[mid+1]) {
                // Se o elemento atual é menor que o da direita,
                // o pico está à direita
                left = mid + 1;
            } else {
                // Caso contrário, pode ser o pico ou está à esquerda
                right = mid;
            }
        }
        return left;
    }
    
    public static void main(String[] args) {
        PeakIndexInMountainArray solver = new PeakIndexInMountainArray();
        int[] mountainArr = {1, 3, 5, 7, 6, 4, 2};
        int peakIndex = solver.peakIndexInMountainArray(mountainArr);
        System.out.println("O pico está no índice: " + peakIndex);
    }
}
```

**Como Funciona:**  
Ao compararmos `arr[mid]` com `arr[mid+1]`, determinamos se estamos na parte ascendente (subir) ou descendente (descer) do array. Assim, a busca converge para o pico, mantendo a eficiência logarítmica.

---

## 3. Aplicações nas Plataformas Leetcode, Hackerrank e Codesign

O padrão Modified Binary Search é frequentemente usado em desafios, pois a maioria das questões exige adaptações aos cenários clássicos. Veja alguns exemplos:

- **Leetcode:**  
  - *Search in Rotated Sorted Array* (busca em array rotacionado)  
  - *Find Minimum in Rotated Sorted Array*  
  - *First and Last Position of Element in Sorted Array*  
  - *Peak Index in a Mountain Array*  
  Esses problemas exigem uma compreensão sofisticada de como modificar os limites da busca para se adequar aos dados.

- **Hackerrank:**  
  Desafios que envolvem “custom comparators” ou a aplicação de condições específicas (por exemplo, encontrar o ponto exato onde uma função muda de comportamento) podem utilizar Modified Binary Search para reduzir a complexidade de tempo.

- **Codesign:**  
  Em plataformas voltadas para o design elegantemente otimizado de código, a capacidade de adaptar a busca binária para cenários variados demonstra habilidades de resolução de problemas e proficiência na escrita de algoritmos eficientes e claros.

---

## 4. Considerações Finais e Dicas

- **Validação das Condições:**  
  Certifique-se de que os casos de borda (como arrays vazios ou tamanho 1) sejam tratados corretamente.

- **Cuidado com Índices:**  
  Ao modificar a busca, a atualização dos ponteiros deve ser feita com cautela para evitar loops infinitos ou acesso indevido aos índices.

- **Teste e Depure:**  
  Devido às particularidades da modificação, teste seu algoritmo com diversos casos, especialmente aqueles que se situam próximo à região de transição do array.

- **Escolha da Abordagem:**  
  Embora o modified binary search mantenha a eficiência O(log n), a clareza do código é fundamental. Sempre documente as condições que direcionam a atualização dos ponteiros.

---

## 5. Conclusão

O padrão **Modified Binary Search** é uma ferramenta poderosa que permite adaptar a busca binária para diversos cenários não convencionais – desde arrays rotacionados até problemas que requerem encontrar o pico de um arranjo em forma de montanha ou localizar a primeira/última ocorrência de um elemento. Ao dominar essas variações, você otimiza suas soluções para desafios em plataformas como Leetcode, Hackerrank e Codesign, mantendo a elegância, eficiência e clareza do código.

Experimente adaptar os exemplos apresentados para resolver seus próprios desafios ou para explorar variações—como busca em arrays "infinitos" ou com condições customizadas—e veja como pequenas modificações podem transformar um algoritmo clássico em uma solução sob medida para cada problema. Bons estudos e excelente codificação!

# Subset
O pattern **Subset** é uma abordagem fundamental para resolver problemas relacionados à geração e manipulação de subconjuntos de um conjunto ou array. Esse padrão é amplamente utilizado em desafios de programação, algoritmos de combinação e problemas de otimização encontrados em plataformas como Leetcode, Hackerrank e Codesign. Ele se manifesta em cenários como:

- **Gerar o Power Set:** Listar todos os subconjuntos (conjunto potência) de um dado conjunto, independentemente da ordem ou tamanho.
- **Subset Sum/Target Sum:** Encontrar se existe algum subconjunto cujos elementos somem a um determinado valor ou encontrar todos os subconjuntos que satisfaçam essa condição.
- **Subsets II:** Geração de subconjuntos únicos a partir de um array que pode conter elementos duplicados.

Nesta discussão, abordaremos os conceitos, vantagens, técnicas (como backtracking, bitmasking e abordagem iterativa) e apresentaremos exemplos práticos em Java, visando oferecer um conteúdo abrangente e aplicável em diversas plataformas de desafios.

---

## 1. Conceitos Fundamentais

### 1.1. Definição e Objetivos

Um **subset** (ou subconjunto) é qualquer conjunto formado a partir de um conjunto original, onde cada elemento pode estar presente ou ausente. Por exemplo, para o conjunto `{a, b, c}`, o conjunto potência (power set) é o conjunto de todos os subconjuntos:  
`{}`, `{a}`, `{b}`, `{c}`, `{a, b}`, `{a, c}`, `{b, c}` e `{a, b, c}`.

Os principais objetivos no pattern *Subset* incluem:
- **Geração Completa:** Listar todas as combinações possíveis.
- **Seleção Condicional:** Escolher apenas subconjuntos que satisfaçam uma propriedade (por exemplo, cuja soma dos elementos seja igual a um valor alvo).
- **Eliminação de Duplicatas:** Em casos onde o array de entrada possui elementos repetidos, garantir que os subconjuntos gerados sejam únicos.

### 1.2. Técnicas Comuns

Para gerar subconjuntos, as técnicas mais comuns são:

- **Backtracking (Recursão):**  
  Uma abordagem recursiva que, a partir de uma decisão em cada elemento (incluir ou não incluir), gera recursivamente os subconjuntos. Essa técnica é simples de implementar e apropriada para problemas onde a estrutura do conjunto não é muito grande.

- **Bitmasking:**  
  Utiliza a representação binária para mapear a inclusão (1) ou exclusão (0) de cada elemento. Se o conjunto possui *n* elementos, existem exatamente 2ⁿ subconjuntos. Essa abordagem é muito direta e costuma ser eficiente para conjuntos de tamanho moderado.

- **Iterativa:**  
  Constrói o conjunto potência etapa a etapa, começando do subconjunto vazio e, para cada elemento, adiciona-o a cada subconjunto já formado.

---

## 2. Aplicações em Plataformas de Desafios

### Leetcode  
No Leetcode, problemas clássicos como **Subsets**, **Subsets II** e **Combination Sum** fazem uso extensivo deste pattern. Eles exigem a geração de subconjuntos completos ou aqueles que somam a um valor específico. Essas questões testam a habilidade de aplicar recursão, gerenciar duplicatas e otimizar a solução.

### Hackerrank  
Em Hackerrank, desafios que envolvem análise combinatória ou extração de subconjuntos de dados utilizam esse pattern para explorar todos os casos possíveis e encontrar soluções que atendam a restrições específicas.

### Codesign  
Plataformas focadas na qualidade de design de código, como Codesign, valorizam soluções que demonstrem clareza e elegância ao combinar técnicas de backtracking e iteração para gerar subconjuntos. Uma implementação bem estruturada evidencia não só o domínio do algoritmo, mas também a preocupação com eficiência e legibilidade.

---

## 3. Exemplos Práticos em Java

### 3.1. Exemplo 1: Gerar Todos os Subconjuntos (Power Set) com Backtracking

Este exemplo utiliza recursão para gerar todos os subconjuntos possíveis de um array de inteiros.

```java
import java.util.*;

public class SubsetBacktracking {

    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, 0, new ArrayList<>(), result);
        return result;
    }
    
    private void backtrack(int[] nums, int start, List<Integer> current, List<List<Integer>> result) {
        // Adiciona uma cópia do subconjunto atual (backtracking)
        result.add(new ArrayList<>(current));
        
        for (int i = start; i < nums.length; i++) {
            // Inclui nums[i] no subconjunto
            current.add(nums[i]);
            // Avança para o próximo elemento
            backtrack(nums, i + 1, current, result);
            // Volta atrás (backtracking) removendo o último elemento incluído
            current.remove(current.size() - 1);
        }
    }
    
    public static void main(String[] args) {
        SubsetBacktracking solver = new SubsetBacktracking();
        int[] nums = {1, 2, 3};
        List<List<Integer>> subsets = solver.subsets(nums);
        System.out.println("Subconjuntos gerados: ");
        for (List<Integer> subset : subsets) {
            System.out.println(subset);
        }
    }
}
```

**Detalhes da Implementação:**  
- A função `backtrack` recebe o array, o índice inicial, o subconjunto atual e a lista de resultados.
- Em cada chamada, o atual subconjunto é adicionado à lista de resultados.
- A iteração permite incluir ou não cada elemento e retroceder após a inclusão.

---

### 3.2. Exemplo 2: Gerar Subconjuntos Usando Bitmasking

Utilizando a técnica de bitmasking, cada número de 0 a 2ⁿ - 1 representa um subconjunto.

```java
import java.util.*;

public class SubsetBitmasking {

    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        int n = nums.length;
        int totalSubsets = 1 << n; // 2^n
        
        for (int mask = 0; mask < totalSubsets; mask++) {
            List<Integer> subset = new ArrayList<>();
            for (int i = 0; i < n; i++) {
                // Se o i-ésimo bit estiver ligado, inclui nums[i]
                if ((mask & (1 << i)) != 0) {
                    subset.add(nums[i]);
                }
            }
            result.add(subset);
        }
        return result;
    }
    
    public static void main(String[] args) {
        SubsetBitmasking solver = new SubsetBitmasking();
        int[] nums = {1, 2, 3};
        List<List<Integer>> subsets = solver.subsets(nums);
        System.out.println("Subconjuntos gerados (bitmasking): ");
        for (List<Integer> subset : subsets) {
            System.out.println(subset);
        }
    }
}
```

**Detalhes da Implementação:**  
- Cada número entre 0 e 2ⁿ - 1 é interpretado como uma máscara de bits que indica quais elementos incluir.
- Essa abordagem é especialmente útil para conjuntos com tamanho pequeno a moderado, dado que o número de subconjuntos cresce exponencialmente.

---

### 3.3. Exemplo 3: Problema Subset Sum com Backtracking

Um problema comum é verificar se existe um subconjunto cuja soma seja igual a um valor alvo.

```java
import java.util.*;

public class SubsetSum {

    // Retorna true se houver algum subconjunto cuja soma seja igual ao target
    public boolean subsetSum(int[] nums, int target) {
        return backtrack(nums, target, 0);
    }
    
    private boolean backtrack(int[] nums, int target, int index) {
        // Caso base: se o target for 0, encontrou um subconjunto que soma ao target
        if (target == 0) {
            return true;
        }
        // Se esgotou os elementos ou o target se tornou negativo
        if (index >= nums.length || target < 0) {
            return false;
        }
        
        // Escolhe o elemento nums[index]
        if (backtrack(nums, target - nums[index], index + 1)) {
            return true;
        }
        // Não escolhe o elemento nums[index]
        return backtrack(nums, target, index + 1);
    }
    
    public static void main(String[] args) {
        SubsetSum solver = new SubsetSum();
        int[] nums = {3, 34, 4, 12, 5, 2};
        int target = 9;
        boolean exists = solver.subsetSum(nums, target);
        System.out.println("Existe um subconjunto cuja soma é " + target + "? " + exists);
    }
}
```

**Detalhes da Implementação:**  
- A função `backtrack` diminui o target sempre que inclui um elemento.
- Se o target se torna 0, isto significa que o subconjunto atual soma exatamente o valor desejado.
- Ao decidir incluir ou não cada elemento, o algoritmo explora todas as combinações possíveis.

---

## 4. Considerações Avançadas

- **Eliminação de Duplicatas:**  
  Para problemas como *Subsets II* (quando os elementos podem se repetir), é necessário ordenar o array inicialmente e, durante o backtracking, pular elementos duplicados na mesma árvore de decisão.

- **Otimização de Performance:**  
  Dado que a quantidade total de subconjuntos é exponencial (2ⁿ), para arrays grandes é fundamental identificar pontos de poda (por exemplo, quando a soma parcial já ultrapassa o target em problemas de subset sum).

- **Escolha da Abordagem:**  
  - **Backtracking** é intuitivo e flexível para a maioria dos cenários, permitindo adicionar condições de parada e gerar subconjuntos que atendam a restrições específicas.
  - **Bitmasking** é direto e eficiente para conjuntos de tamanho pequeno a moderado, mas pode não ser adequado para instâncias maiores, devido ao crescimento exponencial.

---

## 5. Conclusão

O pattern **Subset** é indispensável para uma variedade de problemas que exigem a geração e manipulação de subconjuntos. Ao dominar tanto técnicas recursivas com backtracking quanto abordagens iterativas (como a de bitmasking), você estará preparado para atacar desafios em plataformas como Leetcode, Hackerrank e Codesign. Além de compreender a lógica para construir subconjuntos, é importante também otimizar e adaptar a solução para lidar com duplicatas e restrições específicas, garantindo que seu código seja eficiente, claro e escalável.

Explore os exemplos apresentados, adapte-os a problemas reais e experimente variações, como a integração com técnicas de poda e memoização, para expandir seu conjunto de ferramentas algoritmicas. Bons estudos e excelente codificação!

# Sliding Window
O pattern **Sliding Window** é uma técnica poderosa para resolver problemas que envolvem processamento de subarrays ou substrings contíguas, onde queremos extrair informações (como somas, contagens, máximo/mínimo, ou propriedades específicas) de janelas móveis dentro de uma estrutura de dados. Esse padrão permite transformar algoritmos que, de outra forma, poderiam exigir soluções ineficientes (como laços aninhados) em métodos com complexidade linear, ajudando a melhorar a performance em desafios encontrados em plataformas como Leetcode, Hackerrank e Codesign.

A seguir, apresentamos um conteúdo completo sobre o padrão **Sliding Window** – desde a conceituação básica até aplicações práticas com exemplos em Java.

---

## 1. Introdução e Conceitos Fundamentais

### 1.1. O que é Sliding Window?

A ideia central do Sliding Window é utilizar dois ponteiros (ou índices) para definir uma “janela” que se move sobre o array ou string. Essa janela pode ter:

- **Tamanho Fixo:** Em que o tamanho da janela é pré-definido (por exemplo, encontrar a soma máxima de uma subarray de tamanho *k*).
- **Tamanho Variável:** Em que a janela se expande e/ou contrai para atender a uma determinada condição (por exemplo, encontrar a menor substring que contenha todos os caracteres de um conjunto, ou a maior substring sem caracteres repetidos).

### 1.2. Por que Utilizar o Sliding Window?

- **Eficiência:** Em muitos problemas, o uso da técnica evita a necessidade de laços aninhados, reduzindo a complexidade de tempo de O(n²) para O(n) (ou O(2n), o que é considerado linear).
- **Iteração Contínua:** Permite que a janela “deslize” de forma contínua, aproveitando o processamento anterior para atualizar as respostas sem reprocessar toda a subestrutura.
- **Aplicabilidade:** É ideal para resolver problemas de análise de sequências, agregação de valores, detecção de padrões e muito mais.

---

## 2. Abordagens do Sliding Window

### 2.1. Janela de Tamanho Fixo

Nesta abordagem, a janela tem um tamanho constante.  
**Exemplo Típico:** Encontrar a soma máxima de uma subarray de tamanho *k*.  
- Iniciamos a janela no início do array.
- Calculamos a soma dos *k* primeiros elementos.
- Em seguida, “deslizamos” a janela para a direita, subtraindo o elemento que saiu da janela e adicionando o novo elemento que entrou, atualizando a soma.

### 2.2. Janela Dinâmica (Variável)

A janela de tamanho variável é utilizada quando a condição desejada pode exigir diferentes tamanhos de janela.  
**Exemplos Típicos:**
- **Longest Substring Without Repeating Characters:** Encontrar a maior substring sem caracteres repetidos.  
- **Min Window Substring:** Encontrar a menor substring que contém todos os caracteres de uma determinada string.
  
Nesses casos, os dois ponteiros (geralmente chamados de `left` e `right`) são movimentados de forma diferente (um para expandir a janela e outro para contrair) com base em uma condição ou restrição.

---

## 3. Aplicações em Plataformas (Leetcode, Hackerrank e Codesign)

- **Leetcode:**  
  Desafios clássicos como “Maximum Sum Subarray of Size K”, “Longest Substring Without Repeating Characters” e “Minimum Window Substring” são resolvidos com variações do Sliding Window.
  
- **Hackerrank:**  
  Problemas envolvendo análises de sequência, agregação de dados em fluxos contínuos e contagem de eventos se beneficiam do padrão, permitindo extrair rapidamente as informações de subsequências relevantes.
  
- **Codesign:**  
  Em plataformas focadas na qualidade do design de código, o uso desse padrão demonstra abstracção, clareza e soluções otimizadas. Implementar o Sliding Window de forma modular e comentada é um diferencial no design de algoritmos.

---

## 4. Exemplos Práticos em Java

### 4.1. Exemplo: Janela Fixa – Soma Máxima de Subarray de Tamanho K

**Problema:** Dados um array de inteiros e um número inteiro *k*, encontrar a soma máxima de qualquer subarray de tamanho *k*.

```java
public class MaximumSumSubarray {
    
    public int maxSumSubarray(int[] nums, int k) {
        if(nums == null || nums.length < k) {
            throw new IllegalArgumentException("Array inválido ou k maior que o tamanho do array.");
        }
        
        int maxSum = 0;
        int windowSum = 0;
        
        // Calcula a soma da primeira janela de tamanho k
        for (int i = 0; i < k; i++) {
            windowSum += nums[i];
        }
        maxSum = windowSum;
        
        // Desliza a janela através do array
        for (int i = k; i < nums.length; i++) {
            // Atualiza a soma: remove o elemento que saiu e adiciona o novo
            windowSum += nums[i] - nums[i - k];
            maxSum = Math.max(maxSum, windowSum);
        }
        
        return maxSum;
    }
    
    public static void main(String[] args) {
        MaximumSumSubarray solver = new MaximumSumSubarray();
        int[] nums = {2, 1, 5, 1, 3, 2};
        int k = 3;
        int max = solver.maxSumSubarray(nums, k);
        System.out.println("Soma máxima do subarray de tamanho " + k + " é: " + max);
    }
}
```

**Como Funciona:**  
- A soma da janela inicial é calculada.  
- Em cada iteração, a janela desloca um elemento para a direita: subtrai-se o primeiro elemento da janela atual e adiciona-se o próximo elemento do array, atualizando a soma e mantendo a janela de tamanho fixo.

---

### 4.2. Exemplo: Janela Dinâmica – Longest Substring Without Repeating Characters

**Problema:** Dada uma string, encontrar o comprimento da maior substring sem caracteres repetidos.

```java
import java.util.HashSet;
import java.util.Set;

public class LongestUniqueSubstring {
    
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.isEmpty()) {
            return 0;
        }
        
        Set<Character> window = new HashSet<>();
        int left = 0;
        int maxLength = 0;
        
        // Expande a janela com o ponteiro "right"
        for (int right = 0; right < s.length(); right++) {
            char currentChar = s.charAt(right);
            // Se o caractere já existe na janela, contrai a janela
            while (window.contains(currentChar)) {
                window.remove(s.charAt(left));
                left++;
            }
            // Adiciona o novo caractere e atualiza o comprimento máximo
            window.add(currentChar);
            maxLength = Math.max(maxLength, right - left + 1);
        }
        return maxLength;
    }
    
    public static void main(String[] args) {
        LongestUniqueSubstring solver = new LongestUniqueSubstring();
        String input = "abcabcbb";
        int longest = solver.lengthOfLongestSubstring(input);
        System.out.println("O comprimento da maior substring sem repetições em \"" + input + "\" é: " + longest);
    }
}
```

**Como Funciona:**  
- Dois ponteiros (`left` e `right`) definem uma janela que se expande enquanto os caracteres forem únicos.  
- Ao encontrar um caractere duplicado, o ponteiro `left` é movido para a direita até que o caractere duplicado seja removido da janela, garantindo que a substring permaneça sem caracteres repetidos.

---

## 5. Considerações Avançadas e Dicas

- **Poda e Otimização:**  
  Em problemas com janelas dinâmicas, uma boa prática é atualizar a condição de parada dentro do laço para evitar iterações desnecessárias e melhorar a performance.
  
- **Uso de Estruturas Auxiliares:**  
  Dependendo do problema, estruturas como `HashSet`, `HashMap` ou até mesmo arrays podem ser utilizadas para armazenar informações relacionadas à janela (como frequência dos elementos).
  
- **Cuidados com Índices:**  
  Mantenha o controle correto dos índices para evitar erros de acesso fora dos limites ou loops infinitos. Comentários e uma abordagem modular ajudam a manter o código claro e livre de erros.
  
- **Aplicação Híbrida:**  
  Muitas vezes o Sliding Window é combinado com outras técnicas (como Two Pointers) para adaptar a solução a condições mais complexas e personalizadas.

---

## 6. Conclusão

O padrão **Sliding Window** é uma técnica versátil e extremamente útil para resolver diversos problemas que envolvem subsequências contíguas. Seja para encontrar a soma máxima em um subarray de tamanho fixo ou para determinar a maior substring sem caracteres repetidos, o método permite reduzir a complexidade do problema e desenvolver soluções eficientes.

Plataformas como Leetcode, Hackerrank e Codesign frequentemente apresentam desafios que se beneficiam dessa abordagem. Ao dominar tanto as variações de janela fixa quanto dinâmica, você estará bem equipado para enfrentar problemas reais, escrevendo um código limpo, eficiente e de fácil manutenção em Java.

Experimente adaptar os exemplos acima para diferentes cenários, explore técnicas híbridas e desafie-se com problemas mais complexos que integrem o Sliding Window a outras estratégias. Bons estudos e excelente codificação!


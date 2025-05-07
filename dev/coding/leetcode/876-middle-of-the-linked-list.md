## Índice
1. [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/description/)

---

### Nome do Desafio:
Middle of the Linked List

### Categoria:
Estruturas de Dados - Listas Ligadas

### Link do Desafio:
- [LeetCode](https://leetcode.com/problems/middle-of-the-linked-list/description/)
- Não encontrei um link oficial para este desafio no HackerRank, mas você pode explorar desafios relacionados a listas ligadas [aqui](https://www.hackerrank.com/domains/data-structures/linked-lists).

### Solução Java (código comentado):

```java
class Solution {
    // Método para encontrar o nó do meio da lista ligada
    public ListNode middleNode(ListNode head) {
        // Ponteiro rápido que avança duas posições por vez
        ListNode fast = head;
        // Ponteiro lento que avança uma posição por vez
        ListNode slow = head;

        // Enquanto o ponteiro rápido não atingir o final da lista
        while (fast != null && fast.next != null) {
            slow = slow.next; // Avança uma posição
            fast = fast.next.next; // Avança duas posições
        }

        // Quando o ponteiro rápido atingir o final, o lento estará no meio
        return slow;
    }
}
```

### Explicação da Lógica e Justificativa:
- Utilizamos dois ponteiros: **slow** e **fast**.
- O ponteiro **slow** avança uma posição por vez, enquanto o **fast** avança duas.
- Quando **fast** atinge o final da lista, **slow** estará exatamente no meio.
- Essa abordagem tem **complexidade O(n)** e **uso de memória O(1)**, tornando-a eficiente.

### Alternativas/Variações:
1. **Contagem de elementos**: Percorrer a lista uma vez para contar os elementos e, em seguida, percorrer novamente até a posição do meio.
   - **Desvantagem**: Requer duas passagens pela lista.
2. **Armazenamento em array**: Armazenar os nós em um array e acessar diretamente o índice do meio.
   - **Desvantagem**: Consome memória extra **O(n)**.

Se precisar de mais detalhes ou quiser explorar outros desafios, estou por aqui! 🚀
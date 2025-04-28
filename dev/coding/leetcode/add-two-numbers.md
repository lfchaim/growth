Ótima escolha! O problema **"Add Two Numbers"** do LeetCode envolve a soma de dois números representados como **listas ligadas**, onde cada nó contém um único dígito e os números estão armazenados em ordem reversa. Vamos analisar diferentes soluções em **Java**, desde a menos eficiente até a mais otimizada.

---

### 1️⃣ Solução Ingênua (Recursiva) - **O(n)** (Potencialmente Ineficiente)
Uma abordagem **recursiva** resolve o problema de forma intuitiva, somando os nós e propagando o **carry** (vai-um) para a próxima chamada. No entanto, há um risco de **overflow na pilha** quando a lista for muito grande.

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

public class AddTwoNumbersRecursive {
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        return addTwoNumbersHelper(l1, l2, 0);
    }

    private static ListNode addTwoNumbersHelper(ListNode l1, ListNode l2, int carry) {
        if (l1 == null && l2 == null && carry == 0) return null;
        int sum = (l1 != null ? l1.val : 0) + (l2 != null ? l2.val : 0) + carry;
        ListNode result = new ListNode(sum % 10);
        result.next = addTwoNumbersHelper(l1 != null ? l1.next : null, l2 != null ? l2.next : null, sum / 10);
        return result;
    }
}
```

🔹 **Comentário:** Embora elegante, a **recursão** pode causar problemas de desempenho quando a lista cresce muito, tornando a abordagem menos escalável.

---

### 2️⃣ Solução Iterativa com ListNode - **O(n)**
Uma abordagem **iterativa** que percorre ambas as listas ligadas, mantendo um **carry** para a soma correta. Essa é a abordagem mais usada!

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

public class AddTwoNumbersIterative {
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0); // Nó fictício
        ListNode current = dummy;
        int carry = 0;
        
        while (l1 != null || l2 != null || carry != 0) {
            int sum = (l1 != null ? l1.val : 0) + (l2 != null ? l2.val : 0) + carry;
            carry = sum / 10;
            current.next = new ListNode(sum % 10);
            current = current.next;
            
            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }
        
        return dummy.next;
    }
}
```

🔹 **Comentário:** Esta abordagem tem **tempo linear O(n)** e é **iterativa**, evitando problemas de pilha e sendo mais eficiente.

---

### 3️⃣ Solução com Pilha (Melhoria Opcional) - **O(n)**
Uma **variação** usa pilhas para armazenar os valores, realizando a soma ao final. Isso ajuda se quisermos **manter números na ordem original**.

```java
import java.util.Stack;

class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

public class AddTwoNumbersStack {
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        int carry = 0;

        while (l1 != null || l2 != null || carry > 0) {
        if (l1 != null) {
            carry += l1.val;
            l1 = l1.next;
        }
        if (l2 != null) {
            carry += l2.val;
            l2 = l2.next;
        }
        curr.next = new ListNode(carry % 10);
        carry /= 10;
        curr = curr.next;
        }

        return dummy.next;
    }
}
```

🔹 **Comentário:** Útil caso precisemos somar listas que estão na **ordem correta**, ao invés da reversa.

---

## 📌 Conclusão:
1. **Recursiva** -> Funcional, mas pode sofrer com **problemas de pilha** (**O(n)**).
2. **Iterativa (Melhor escolha)** -> Simples e **eficiente** para listas ligadas (**O(n)**).
3. **Com Pilhas** -> Útil para somas que exigem manter a **ordem original** (**O(n)**).

Se quiser mais explicações ou variações, só chamar! 🚀

### Prompt (Copilot)
Analise o algoritmo "Add Two Numbers" do LeetCode, apresentando desde a pior até a melhor solução, comentando e usando Java.

## Resultado
Runtime: 1ms Beats 100.00%
Memory: 44.24MB Beats 93.25%

## LeetCode
[https://leetcode.com/problems/add-two-numbers/]
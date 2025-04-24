Pergunta: Crie um ebook completo sobre o assunto Object Calisthenics, com exemplos em Java.
Resposta: ## Ebook: **Object Calisthenics — Prática para Código Orientado a Objetos Limpo em Java**

---

### **Sumário**

1. [Introdução](#introducao)
2. [O que é Object Calisthenics?](#o-que-e-object-calisthenics)
3. [Os 9 Mandamentos do Object Calisthenics](#os-9-mandamentos)
    - [1. Only One Level of Indentation per Method](#1-um-nível-de-indentação-por-método)
    - [2. Don’t Use the ELSE Keyword](#2-não-use-a-palavra-chave-else)
    - [3. Wrap All Primitives and Strings](#3-encapsule-todos-os-primitivos-e-strings)
    - [4. First-Class Collections](#4-coleções-de-primeira-classe)
    - [5. One Dot per Line](#5-um-ponto-por-linha)
    - [6. Don’t Abbreviate](#6-não-abrevie)
    - [7. Keep All Entities Small](#7-mantenha-todas-as-entidades-pequenas)
    - [8. No Classes with More Than Two Instance Variables](#8-sem-classe-com-mais-de-duas-variáveis-de-instância)
    - [9. No Getters/Setters/Properties](#9-sem-gettersetterpropriedades)
4. [Exemplo Prático Consolidado](#exemplo-pratico)
5. [Conclusão](#conclusao)
6. [Leituras Recomendadas](#leituras-recomendadas)

---

## 1. <a name=\"introducao\"></a>Introdução

A escrita de código limpo e de fácil manutenção é um desafio constante. Object Calisthenics são exercícios criados para ajudar desenvolvedores a praticar e internalizar boas práticas de Orientação a Objetos (OO), levando seus projetos a um nível elevado de qualidade. Neste ebook, você conhecerá, com exemplos práticos em Java, cada um dos 9 mandamentos do Object Calisthenics.

---

## 2. <a name=\"o-que-e-object-calisthenics\"></a>O que é Object Calisthenics?

Object Calisthenics (ou \"calistenia de objetos\") é um conjunto de 9 regras-proposta por Jeff Bay para impulsionar hábitos de design OO. Não são regras absolutas, mas exercícios rigorosos capazes de promover reflexão, questionamento e aprimoramento dos projetos orientados a objetos.

---

## 3. <a name=\"os-9-mandamentos\"></a>Os 9 Mandamentos do Object Calisthenics

### 1. <a name=\"1-um-nível-de-indentação-por-método\"></a>Only One Level of Indentation per Method  
**Regra:** Cada método pode ter apenas um nível de indentação (exemplo: não pode ter um `if` dentro de um `for`).

**Exemplo Ruim:**
```java
void processOrders(List<Order> orders) {
    for (Order order : orders) {
        if (order.isValid()) {
            ship(order);
        }
    }
}
```

**Exemplo Bom:**
```java
void processOrders(List<Order> orders) {
    for (Order order : orders) {
        processIfValid(order);
    }
}

void processIfValid(Order order) {
    if (order.isValid()) {
        ship(order);
    }
}
```
---

### 2. <a name=\"2-não-use-a-palavra-chave-else\"></a>Don’t Use the ELSE Keyword  
**Regra:** Elimine `else` usando early returns ou polimorfismo.

**Exemplo Ruim:**
```java
if (user.isActive()) {
    grantAccess();
} else {
    denyAccess();
}
```

**Exemplo Bom:**
```java
if (!user.isActive()) {
    denyAccess();
    return;
}
grantAccess();
```
---

### 3. <a name=\"3-encapsule-todos-os-primitivos-e-strings\"></a>Wrap All Primitives and Strings  
**Regra:** Não use tipos primitivos ou `String` diretamente fora de suas próprias classes wrapper (objetos de valor).

**Exemplo Ruim:**
```java
void register(String username, String password) { ... }
```

**Exemplo Bom:**
```java
void register(Username username, Password password) { ... }

public class Username {
    private String value;
    public Username(String value) { /* validações */ this.value = value; }
}
```
---

### 4. <a name=\"4-coleções-de-primeira-classe\"></a>First-Class Collections  
**Regra:** Não use coleções nuas; encapsule-as em suas próprias classes.

**Exemplo Ruim:**
```java
public class Order {
    private List<Item> items;
}
```

**Exemplo Bom:**
```java
public class Items {
    private List<Item> items;
    // métodos de manipulação
}

public class Order {
    private Items items;
}
```
---

### 5. <a name=\"5-um-ponto-por-linha\"></a>One Dot per Line  
**Regra:** Não acesse mais de um membro ao mesmo tempo. Por exemplo, evite `order.getCustomer().getAddress().getCity()`.

**Exemplo Ruim:**
```java
String city = order.getCustomer().getAddress().getCity();
```

**Exemplo Bom:**
```java
String city = order.customerCity();
```
_Escondendo a cadeia internamente na classe `Order`._

---

### 6. <a name=\"6-não-abrevie\"></a>Don’t Abbreviate  
**Regra:** Use nomes completos e expressivos. Evite abreviações.

**Exemplo Ruim:**
```java
int qty;
```

**Exemplo Bom:**
```java
int quantity;
```
---

### 7. <a name=\"7-mantenha-todas-as-entidades-pequenas\"></a>Keep All Entities Small  
**Regra:** Mantenha classes e métodos pequenos (métodos com até 10 linhas e classes com até 50 linhas são um bom objetivo inicial).

---

### 8. <a name=\"8-sem-classe-com-mais-de-duas-variáveis-de-instância\"></a>No Classes with More Than Two Instance Variables  
**Regra:** Limite classes a no máximo duas variáveis de instância. Estimula composição e não herança.

**Exemplo Ruim:**
```java
public class User {
    private String name;
    private String email;
    private String password;
}
```

**Exemplo Bom:**
```java
public class User {
    private Name name;
    private Contact contact;
}

public class Contact {
    private Email email;
    private Password password;
}
```
---

### 9. <a name=\"9-sem-gettersetterpropriedades\"></a>No Getters/Setters/Properties  
**Regra:** Não exponha detalhes internos do objeto. Encapsule comportamentos e defina métodos que representem intenções.

**Exemplo Ruim:**
```java
public class Account {
    private double balance;
    public double getBalance() { return balance; }
}
```

**Exemplo Bom:**
```java
public class Account {
    private Money balance;
    public void transferTo(Account destination, Money amount) { ... }
}
```
---

## 4. <a name=\"exemplo-pratico\"></a>Exemplo Prático Consolidado

Vamos refatorar um algoritmo simples — cadastro de pedido — implementando os princípios do Object Calisthenics:

**Código convencional:**
```java
public class Order {
    private List<Item> items;
    private String customerName;
    private String customerEmail;

    public Order(List<Item> items, String customerName, String customerEmail) {
        this.items = items;
        this.customerName = customerName;
        this.customerEmail = customerEmail;
    }

    public double total() {
        double sum = 0;
        for (Item item : items) sum += item.getPrice();
        return sum;
    }
}
```

**Aplicando Object Calisthenics:**
```java
public class Customer {
    private Name name;
    private Email email;

    public Customer(Name name, Email email) {
        this.name = name;
        this.email = email;
    }
}

public class Name {
    private String value;
    public Name(String value) { this.value = value; }
}

public class Email {
    private String value;
    public Email(String value) { this.value = value; }
}

public class Item {
    private Price price;
    public Item(Price price) { this.price = price; }
    public Price price() { return price; }
}

public class Items {
    private List<Item> items = new ArrayList<>();
    public void add(Item item) { items.add(item); }
    public Price total() {
        return items.stream()
            .map(Item::price)
            .reduce(new Price(0), Price::add);
    }
}

public class Price {
    private double value;
    public Price(double value) { this.value = value; }
    public Price add(Price other) { return new Price(this.value + other.value); }
    public double value() { return value; }
}

public class Order {
    private Items items;
    private Customer customer;

    public Order(Items items, Customer customer) {
        this.items = items;
        this.customer = customer;
    }

    public Price total() {
        return items.total();
    }
}
```
**Benefícios Alcançados:**
- Nenhum método longo ou complexo.
- Encapsulamento total de tipos.
- Classes pequenas, funções coesas.
- Sem getters/setters expostos.
- Sem else.
- Estrutura facilmente testável e manutenível.

---

## 5. <a name=\"conclusao\"></a>Conclusão

Object Calisthenics desafia os programadores a pensar OO de maneira profunda. Exercitar estes nove mandamentos não garante perfeição, mas aprimora o senso crítico, levando à escrita de código expressivo, limpo, testável e de alta qualidade. Pratique, adapte e evolua!

---

## 6. <a name=\"leituras-recomendadas\"></a>Leituras Recomendadas

- [ThoughtWorks: Object Calisthenics](https://www.thoughtworks.com/en-us/insights/blog/object-calisthenics)
- Livro: **\"The ThoughtWorks Anthology: Essays on Software Technology and Innovation\"** — Jeff Bay
- Livro: **\"Clean Code\"** - Robert C. Martin

---

**Bons estudos e pratique sempre!**

Engine: GPT 4.1 (Adapta.org)


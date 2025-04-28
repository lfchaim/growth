## 🚀 Solução

### 🔍 Contexto

O problema central é determinar o comprimento da maior substring possível dentro de uma string dada, onde nenhum caractere se repete. Isso é útil em várias aplicações, como processamento de texto e análise de dados.

### 🧩 Abordagem

A abordagem utilizada na solução envolve o uso de uma estrutura de dados de mapa para rastrear a última posição onde cada caractere foi encontrado. Isso permite que a função evite caracteres repetidos enquanto expande a substring atual. Aqui está um resumo detalhado do processo:

1. **Inicialização**:
    - Um mapa é criado para armazenar os caracteres e suas posições.
    - Variáveis para rastrear o comprimento máximo (`max`), o comprimento atual (`count`), e a posição inicial da substring (`begin`) são inicializadas.

2. **Iteração pela String**:
    - A função percorre cada caractere da string com um índice `end`.
    - Para cada caractere, verifica-se se ele está no mapa e se sua última posição registrada é anterior à posição inicial da substring (`begin`).

3. **Atualização da Substring**:
    - Se o caractere não estiver no mapa ou sua última posição for anterior a `begin`, ele é adicionado ou atualizado no mapa com a posição atual.
    - Se o caractere já estiver na substring atual (isto é, sua posição no mapa é maior ou igual a `begin`), a posição inicial (`begin`) é movida para a posição seguinte à última ocorrência desse caractere.

4. **Cálculo do Comprimento**:
    - O comprimento da substring atual é calculado como a diferença entre os índices `end` e `begin`, mais um.
    - O comprimento máximo (`max`) é atualizado se o comprimento da substring atual for maior.

### ⚙️ Complexidade

A solução tem uma complexidade de tempo linear, O(n), onde n é o comprimento da string. Isso ocorre porque cada caractere é processado no máximo duas vezes (uma vez quando é encontrado pela primeira vez e outra quando sua posição inicial é ajustada).

### 📈 Exemplos de Uso

- **Entrada**: `"abcabcbb"`
  - **Saída**: `3` (A substring sem caracteres repetidos mais longa é `"abc"`).

- **Entrada**: `"bbbbb"`
  - **Saída**: `1` (A substring sem caracteres repetidos mais longa é `"b"`).

- **Entrada**: `"pwwkew"`
  - **Saída**: `3` (A substring sem caracteres repetidos mais longa é `"wke"`).

``` java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> chars = new HashMap<>();
		int max = 0;
		int count = 0;
		int begin = 0;
		
		for(int end = 0; end < s.length(); end++) {
			char c = s.charAt(end);
			
			if(!chars.containsKey(c) || chars.get(c) < begin) {
				chars.put(c, end);
			}else {
				begin = chars.get(c) + 1;
				chars.put(c, end);
			}
			
			count = (end - begin) + 1;
			if(max < count)
				max = count;
		}
		
		return max;
    }
}
```

[https://leetcode.com/problems/longest-substring-without-repeating-characters/]

## Resultado
Runtime: 5ms Beats 87.74%
Memory: 44.53MB Beats 76.44%
# Prompt

Resolva o algoritmo Three Sum, apresentando todas as possíveis soluções, ordenadas da pior para a melhor solução. Dê exemplos de código usando Java

# Answer

# Resolução do Problema Three Sum: Da Solução Mais Básica à Mais Eficiente

Antes de apresentar as soluções para o problema Three Sum, vamos entender o que se trata. O problema Three Sum consiste em encontrar todas as triplas de números em um array cujos elementos somam um valor específico (geralmente zero). Para cada solução, devemos garantir que não haja triplas duplicadas no resultado.

## Solução 1: Abordagem por Força Bruta - O(n³)

Esta é a abordagem mais intuitiva, porém menos eficiente. Utilizamos três loops aninhados para verificar todas as possíveis combinações de triplas no array.

```java
import java.util.*;

public class ThreeSumBruteForce {
    public List> threeSum(int[] nums) {
        List> result = new ArrayList<>();
        int n = nums.length;
        
        // Verificamos todas as possíveis triplas
        for (int i = 0; i  triplet = Arrays.asList(nums[i], nums[j], nums[k]);
                        // Ordenamos para facilitar a detecção de duplicatas
                        Collections.sort(triplet);
                        if (!result.contains(triplet)) {
                            result.add(triplet);
                        }
                    }
                }
            }
        }
        
        return result;
    }
    
    public static void main(String[] args) {
        ThreeSumBruteForce solution = new ThreeSumBruteForce();
        int[] nums = {-1, 0, 1, 2, -1, -4};
        System.out.println(solution.threeSum(nums)); // [[-1, -1, 2], [-1, 0, 1]]
    }
}
```

### Análise da Complexidade
- **Tempo**: O(n³) para percorrer todas as triplas + O(n log n) para ordenação de cada tripla + O(n) para verificação de duplicatas, resultando em O(n⁴) no pior caso.
- **Espaço**: O(n) para armazenar o resultado.

A principal ineficiência desta abordagem é que examinamos todas as combinações possíveis, independentemente de poderem formar uma solução válida ou não[1].

## Solução 2: Abordagem com Hash Set - O(n²)

Uma melhoria significativa é usar um HashSet para procurar o terceiro elemento, reduzindo a complexidade para O(n²).

```java
import java.util.*;

public class ThreeSumHashSet {
    public List> threeSum(int[] nums) {
        List> result = new ArrayList<>();
        int n = nums.length;
        Arrays.sort(nums); // Pré-ordenação para facilitar eliminação de duplicatas
        
        for (int i = 0; i  0 && nums[i] == nums[i-1]) continue;
            
            HashSet seen = new HashSet<>();
            for (int j = i + 1; j > threeSum(int[] nums) {
        List> result = new ArrayList<>();
        int n = nums.length;
        
        // Ordenação do array
        Arrays.sort(nums);
        
        for (int i = 0; i  0 && nums[i] == nums[i-1]) continue;
            
            int left = i + 1;
            int right = n - 1;
            
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                
                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    
                    // Evita duplicatas
                    while (left < right && nums[left] == nums[left+1]) left++;
                    while (left < right && nums[right] == nums[right-1]) right--;
                    
                    // Move os ponteiros
                    left++;
                    right--;
                } else if (sum < 0) {
                    left++; // Precisamos de números maiores
                } else {
                    right--; // Precisamos de números menores
                }
            }
        }
        
        return result;
    }
    
    public static void main(String[] args) {
        ThreeSumTwoPointers solution = new ThreeSumTwoPointers();
        int[] nums = {-1, 0, 1, 2, -1, -4};
        System.out.println(solution.threeSum(nums)); // [[-1, -1, 2], [-1, 0, 1]]
    }
}
```

### Análise da Complexidade
- **Tempo**: O(n log n) para ordenação + O(n²) para os loops, resultando em O(n²).
- **Espaço**: O(1) sem contar o espaço para armazenar o resultado.

Esta abordagem é considerada a melhor porque, além de ter complexidade O(n²) como a abordagem com HashSet, ela utiliza menos memória e tem melhor localidade de cache, resultando em melhor desempenho na prática[6][13].

## Conclusão

Apresentamos três soluções para o problema Three Sum, da menos eficiente à mais eficiente:

1. **Força Bruta**: Simples de implementar, mas extremamente ineficiente com complexidade O(n³) ou até O(n⁴).
2. **Hash Set**: Melhoria significativa, com complexidade O(n²), usando estruturas de dados auxiliares.
3. **Dois Ponteiros**: A solução mais eficiente na prática, com complexidade O(n²) e consumo mínimo de memória.

A abordagem de dois ponteiros se destaca como a melhor solução para este problema, especialmente para arrays grandes, devido ao seu uso eficiente de memória e melhor desempenho prático[8][10]. Esta técnica também pode ser estendida para resolver variantes do problema, como 3Sum Closest ou 4Sum.

Citations:
[1] https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/
[2] https://www.alura.com.br/apostila-java-orientacao-objetos/resolucoes-exercicios
[3] https://pt.stackoverflow.com/questions/240410/%C3%89-errado-usar-v%C3%A1rios-cases-para-a-mesma-a%C3%A7%C3%A3o-no-switch
[4] https://developer.android.com/tools/adb
[5] https://aartedeprogramar.tech/two-sum-problem/
[6] https://stackoverflow.com/questions/40905695/java-how-to-implement-3-sum
[7] https://www.devmedia.com.br/programacao-orientada-a-objetos-x-programacao-estruturada/31852
[8] https://stackoverflow.com/questions/43145481/triplet-sum-using-binary-search
[9] https://terminalroot.com.br/2024/05/o-que-sao-os-3-pontos-para-metodos-em-java.html
[10] https://edisciplinas.usp.br/mod/assign/view.php?id=5759624&rownum=0&useridlistid=680791cb16d6e109342736&action&lang=it
[11] https://www.youtube.com/watch?v=-YvyO-24wAk
[12] https://www.youtube.com/watch?v=tdeMzsh5Z0w
[13] https://interviewing.io/questions/three-sum
[14] https://docs.oracle.com/cd/E19253-01/820-0446/chp-structs-1/index.html
[15] https://leetcode.com/problems/3sum/
[16] https://www.geeksforgeeks.org/find-triplets-array-whose-sum-equal-zero/
[17] https://github.com/eschwabe/interview-practice/blob/master/coursera/algorithms-part1/analysis-of-algorithms/ThreeSum.java
[18] https://takeuforward.org/data-structure/3-sum-find-triplets-that-add-up-to-a-zero/
[19] https://www.youtube.com/watch?v=-2UVsKwYKV0
[20] https://www.reddit.com/r/leetcode/comments/1k1rj6u/pondering_over_classic_3_sum_problem/?tl=pt-br
[21] https://pt.stackoverflow.com/questions/234882/algoritmo-que-leia-tr%C3%AAs-n%C3%BAmeros-e-exiba-o-resultado-da-soma-dos-dois-primeiros-e
[22] https://www.youtube.com/watch?v=ChWOmxLhUoA
[23] https://www.youtube.com/watch?v=jAtnDGxAqeo
[24] https://www.youtube.com/watch?v=rdXs7cjVn9o
[25] https://terminalroot.com.br/2024/05/o-que-sao-os-3-pontos-para-metodos-em-java.html
[26] https://www.devmedia.com.br/java-como-ler-e-apresentar-dados-com-os-comandos-de-entrada-e-saida/22266
[27] https://blog.grancursosonline.com.br/java-operadores-de-incremento-e-decremento/
[28] https://www.gov.br/esocial/pt-br/empresas/manual-web-geral
[29] https://conhecimento.fgv.br/sites/default/files/concursos/tg12-discursiva.pdf
[30] https://www.gov.br/servidor/pt-br/central-de-conteudo/oportunidades/divulgacao
[31] https://www.cnmp.mp.br/portal/images/Comissoes/CPAMP/Estudos_de_Seguran%C3%A7a_Institucional.pdf
[32] https://www.al.sp.gov.br/repositorio/bibliotecaDigital/20800_arquivo.pdf
[33] https://pjeoffice.trf3.jus.br
[34] https://pncp.gov.br/pncp-api/v1/orgaos/00394502000144/compras/2024/13765/arquivos/1
[35] https://portal1.iff.edu.br/o-iffluminense/pesquisa/pos-graduacao-stricto-sensu/mestrado-profissional-em-sistemas-aplicados-a-engenharia-e-a-gestao/dissertacoes-defendidas/dissertacoes-defendidas-em-2023-1/avaliacao-de-riscos-de-seguranca-cibernetica-no-software-sahana-eden-disaster-management-system-utilizando-conceitos-de-hacker-etico-1/view/++widget++form.widgets.dissertacao/@@download/Fl%C3%A1vio+de+Souza+Lima.pdf
[36] https://logicmojo.com/3sum
[37] https://www.guj.com.br/t/de-ponteiros-para-referencia/42642
[38] https://www.marinha.mil.br/sspm/ensino/sites/www.marinha.mil.br.sspm/files/provas/PROCESSAMENTO%20DE%20DADOS%20VERDE.pdf

---
Resposta do Perplexity: pplx.ai/share   
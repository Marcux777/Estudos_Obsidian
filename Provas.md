## Mochila Binaria

Para provar que o problema da Mochila Binária (ou Mochila Booleana) tem subestrutura ótima, vamos usar uma abordagem matemática detalhada. A subestrutura ótima significa que a solução ótima para um problema pode ser construída a partir das soluções ótimas de seus subproblemas.

### Definição do Problema

Dado um conjunto de `n` itens, onde cada item `i` tem um valor `v[i]` e um peso `w[i]`, e uma mochila com capacidade `W`, o objetivo é maximizar o valor total dos itens colocados na mochila sem exceder a capacidade `W`.

### Relação de Recorrência

Vamos definir `V[i, w]` como o valor máximo que pode ser obtido com um peso total que não excede `w` usando os primeiros `i` itens. A relação de recorrência para `V[i, w]` é:

$[ V[i, w] = \max \left( V[i-1, w], V[i-1, w - w[i]] + v[i] \right) ]$

onde:
- `V[i-1, w]` é o valor máximo obtido sem incluir o `i`-ésimo item.
- `V[i-1, w - w[i]] + v[i]` é o valor máximo obtido incluindo o `i`-ésimo item (se o peso permitir).

### Prova por Contradição

Vamos provar por contradição que o problema da Mochila Binária tem subestrutura ótima.

1. **Suposição Inicial**: Suponha que o problema da Mochila Binária **não** tem subestrutura ótima. Isso significa que a solução ótima para o problema não pode ser construída a partir das soluções ótimas de seus subproblemas.

2. **Configuração Ótima**: Considere uma configuração ótima `S` para a mochila com capacidade `W` usando `n` itens. Isso significa que `S` é a solução que maximiza o valor total sem exceder a capacidade `W`.

3. **Remoção de um Item**: Remova um item `k` da configuração ótima `S`. Agora temos um subproblema com capacidade `W - w[k]` e `n-1` itens. Vamos chamar essa nova configuração de `S'`.

4. **Subproblema Ótimo**: Se `S` é a configuração ótima para o problema original, então `S'` deve ser a configuração ótima para o subproblema com capacidade `W - w[k]` e `n-1` itens. Caso contrário, poderíamos encontrar uma configuração `S''` para o subproblema que tem um valor maior que `S'`, e ao adicionar o item `k` de volta, obteríamos uma configuração melhor que `S`, o que contradiz a suposição de que `S` é ótima.

5. **Contradição**: Portanto, se a solução ótima `S` para o problema original pode ser construída a partir da solução ótima `S'` do subproblema, isso implica que o problema da Mochila Binária tem subestrutura ótima. A suposição inicial de que o problema não tem subestrutura ótima leva a uma contradição.

## SubSet Sum

Para provar que o problema do Subset Sum possui subestrutura ótima, precisamos mostrar que uma solução ótima para o problema pode ser construída a partir de soluções ótimas para seus subproblemas. Vamos considerar o problema do Subset Sum, onde temos um conjunto de números inteiros \( S = \{s_1, s_2, \ldots, s_n\} \) e um valor alvo \( T \). Queremos determinar se existe um subconjunto de \( S \) cuja soma é igual a \( T \).

### Definição do Problema
O problema pode ser definido recursivamente da seguinte forma:

- Seja $( \text{SubsetSum}(S, T) )$ a função que retorna verdadeiro se existe um subconjunto de $S$ cuja soma é $T$, e falso caso contrário.

### Subestrutura Ótima
Para mostrar que o problema possui subestrutura ótima, consideramos dois casos para cada elemento $s_i$ do conjunto $S$:

1. **Caso 1: $s_i$ não está no subconjunto que soma \( T \)**:
   - Nesse caso, precisamos verificar se existe um subconjunto dos elementos restantes que soma \( T \). Formalmente, isso é equivalente a resolver$\text{SubsetSum}(S - \{s_i\}, T)$.

2. **Caso 2: $s_i$ está no subconjunto que soma \( T \)**:
   - Nesse caso, precisamos verificar se existe um subconjunto dos elementos restantes que soma $T - s_i$. Formalmente, isso é equivalente a resolver $\text{SubsetSum}(S - \{s_i\}, T - s_i)$.

### Recorrência
Podemos então definir a função $\text{SubsetSum}(S, T)$ recursivamente como:

$[ \text{SubsetSum}(S, T) = \text{SubsetSum}(S - \{s_i\}, T) \lor \text{SubsetSum}(S - \{s_i\}, T - s_i) ]$

### Prova de Subestrutura Ótima
Para provar que o problema possui subestrutura ótima, precisamos mostrar que se $\text{SubsetSum}(S, T)$ é verdadeiro, então pelo menos um dos subproblemas $( \text{SubsetSum}(S - \{s_i\}, T)$ ou $\text{SubsetSum}(S - \{s_i\}, T - s_i)$ também deve ser verdadeiro.

- Se $\text{SubsetSum}(S, T)$ é verdadeiro, então existe um subconjunto $A \subseteq S$ tal que a soma dos elementos de $A$ é $T$.
- Se $s_i \notin A$, então $A$ é um subconjunto de $S - \{s_i\}$ e a soma dos elementos de $A$ é $T$. Portanto, $\text{SubsetSum}(S - \{s_i\}, T)$ é verdadeiro.
- Se $s_i \in A$, então $A - \{s_i\}$ é um subconjunto de $S - \{s_i\}$ e a soma dos elementos de $A - \{s_i\}$ é $T - s_i$. Portanto, $\text{SubsetSum}(S - \{s_i\}, T - s_i)$ é verdadeiro.

Como pelo menos um dos subproblemas deve ser verdadeiro para que $\text{SubsetSum}(S, T)$ seja verdadeiro, isso demonstra que o problema possui subestrutura ótima.


## Multiplicação de Cadeia de Matrizes

Para provar que o problema da Multiplicação de Cadeia de Matrizes possui subestrutura ótima, precisamos mostrar que uma solução ótima para o problema pode ser construída a partir de soluções ótimas para seus subproblemas. Vamos considerar o problema da Multiplicação de Cadeia de Matrizes, onde temos uma sequência de $n$ matrizes $A_1, A_2, \ldots, A_n$ , e queremos determinar a ordem de multiplicação que minimiza o número total de multiplicações escalares.

### Definição do Problema

Dada uma sequência de $n$ matrizes $A_1, A_2, \ldots, A_n$ \), onde a matriz $A_i$ tem dimensões $p_{i-1}\times p_i$, queremos encontrar a ordem de multiplicação que minimiza o número de operações escalares necessárias.

### Subestrutura Ótima

Para mostrar que o problema possui subestrutura ótima, consideramos a seguinte abordagem:

1. **Divisão do Problema**:
   - Suponha que a ordem ótima para multiplicar a cadeia de matrizes $A_i$ até $A_j$ envolve dividir a cadeia em duas subcadeias $(A_i \cdot \ldots \cdot A_k)$ e $(A_{k+1} \cdot \ldots \cdot A_j)$ para algum $i \leq k < j$.

2. **Soluções Ótimas para Subproblemas**:
   - Se a ordem ótima para multiplicar $A_i$ até $A_j$ envolve dividir a cadeia em $k$, então a ordem ótima para multiplicar $A_i$ até $A_k$ e $A_{k+1}$ até $A_j$ deve ser usada. Caso contrário, poderíamos encontrar uma ordem melhor para multiplicar $A_i$ até $A_j$, o que contradiz a suposição de que a ordem original era ótima.

3. **Construção da Solução Ótima**:
   - Portanto, a solução ótima para o problema original pode ser construída a partir das soluções ótimas dos subproblemas $m[i, k]$ e $m[k+1, j]$.

### Recorrência

Vamos definir \( m[i, j] \) como o número mínimo de multiplicações necessárias para calcular o produto da cadeia de matrizes \( A_i \) até \( A_j \). A chave para a solução é observar que, para calcular \( m[i, j] \), podemos dividir o problema em subproblemas menores:

\[ m[i, j] = \min_{i \leq k < j} \{ m[i, k] + m[k+1, j] + p_{i-1} \cdot p_k \cdot p_j \} \]

Aqui, \( k \) é o índice onde a cadeia é dividida em duas subcadeias \( (A_i \cdot \ldots \cdot A_k) \) e \( (A_{k+1} \cdot \ldots \cdot A_j) \). O custo total é a soma dos custos das duas subcadeias mais o custo de multiplicar as duas matrizes resultantes.

### Prova de Subestrutura Ótima

Para provar que o problema possui subestrutura ótima, consideramos o seguinte:

1. **Divisão do Problema**:
   - Suponha que a ordem ótima para multiplicar a cadeia de matrizes \( A_i \) até \( A_j \) envolve dividir a cadeia em duas subcadeias \( (A_i \cdot \ldots \cdot A_k) \) e \( (A_{k+1} \cdot \ldots \cdot A_j) \) para algum \( i \leq k < j \).

2. **Soluções Ótimas para Subproblemas**:
   - Se a ordem ótima para multiplicar \( A_i \) até \( A_j \) envolve dividir a cadeia em \( k \), então a ordem ótima para multiplicar \( A_i \) até \( A_k \) e \( A_{k+1} \) até \( A_j \) deve ser usada. Caso contrário, poderíamos encontrar uma ordem melhor para multiplicar \( A_i \) até \( A_j \), o que contradiz a suposição de que a ordem original era ótima.

3. **Construção da Solução Ótima**:
   - Portanto, a solução ótima para o problema original pode ser construída a partir das soluções ótimas dos subproblemas \( m[i, k] \) e \( m[k+1, j] \).

### Conclusão

A subestrutura ótima do problema de Multiplicação de Cadeia de Matrizes é demonstrada pela capacidade de construir uma solução ótima para o problema original a partir de soluções ótimas para seus subproblemas. Isso é evidenciado pela recorrência que define o problema em termos de seus subproblemas e pela implementação da solução usando programação dinâmica.
## Árvore de Huffman de Peso Mínimo
Para provar que a Árvore de Huffman de Peso Mínimo tem subestrutura ótima e também possui a propriedade da escolha gulosa, vamos abordar cada uma dessas propriedades separadamente.
### Subestrutura Ótima

A subestrutura ótima significa que a solução ótima para um problema pode ser construída a partir das soluções ótimas de seus subproblemas.
#### Definição do Problema

A Árvore de Huffman é uma árvore binária usada para a codificação de dados, onde os caracteres mais frequentes têm códigos mais curtos. Dado um conjunto de caracteres e suas frequências, a Árvore de Huffman é construída de forma a minimizar o custo total da codificação, que é a soma dos produtos das frequências dos caracteres pelos comprimentos de seus códigos.  
#### Prova da Subestrutura Ótima

1. **Construção da Árvore**: A Árvore de Huffman é construída de forma iterativa. Inicialmente, cada caractere é uma árvore com um único nó. Em cada iteração, as duas árvores com as menores frequências são combinadas em uma nova árvore, cuja raiz tem a soma das frequências das duas árvores combinadas.

2. **Subproblemas**: Em cada iteração, ao combinar duas árvores, estamos essencialmente resolvendo um subproblema menor. Se tivermos uma solução ótima para o problema original, então a combinação das duas árvores de menor frequência deve ser parte dessa solução ótima.

3. **Contradição**: Suponha que a solução ótima para o problema original não possa ser construída a partir das soluções ótimas de seus subproblemas. Isso implicaria que existe uma combinação de árvores que resulta em um custo menor do que a combinação das duas árvores de menor frequência, o que é uma contradição, pois a combinação das duas árvores de menor frequência é a escolha que minimiza o custo em cada passo.

Portanto, a Árvore de Huffman tem subestrutura ótima, pois a solução ótima para o problema original pode ser construída a partir das soluções ótimas de seus subproblemas.
### Propriedade da Escolha Gulosa

A propriedade da escolha gulosa significa que uma escolha localmente ótima em cada passo leva a uma solução globalmente ótima.
#### Prova da Propriedade da Escolha Gulosa
1. **Escolha Gulosa**: Em cada iteração do algoritmo de Huffman, escolhemos as duas árvores com as menores frequências para combinar. Esta é uma escolha localmente ótima, pois minimiza o custo da nova árvore criada.
2. **Prova por Contradição**: Suponha que a escolha gulosa de combinar as duas árvores de menor frequência não leva a uma solução globalmente ótima. Isso implicaria que existe uma outra combinação de árvores que resulta em um custo menor. No entanto, se combinarmos qualquer outra árvore que não seja as duas de menor frequência, o custo da nova árvore será maior, o que contradiz a suposição de que estamos minimizando o custo em cada passo.
3. **Conclusão**: Portanto, a escolha gulosa de combinar as duas árvores de menor frequência em cada passo leva a uma solução globalmente ótima, confirmando que a Árvore de Huffman possui a propriedade da escolha gulosa.

## Dijsktra

Para provar que o algoritmo de Dijkstra encontra o caminho de peso mínimo em um grafo com arestas de peso não negativo, vamos demonstrar que ele possui subestrutura ótima e a propriedade da escolha gulosa.

### Definição do Problema

Dado um grafo dirigido ou não dirigido com pesos não negativos nas arestas, o objetivo é encontrar o caminho de menor custo (peso) de um vértice de origem `s` para todos os outros vértices no grafo.

### Subestrutura Ótima

A subestrutura ótima significa que a solução ótima para um problema pode ser construída a partir das soluções ótimas de seus subproblemas.

#### Prova da Subestrutura Ótima

1. **Definição de Subproblemas**: Considere um caminho de peso mínimo `P` de um vértice de origem `s` para um vértice destino `t`. Suponha que `P` passe por um vértice intermediário `v`.

2. **Subcaminhos Ótimos**: O caminho `P` pode ser dividido em dois subcaminhos: `P1` de `s` a `v` e `P2` de `v` a `t`. Se `P` é o caminho de peso mínimo de `s` a `t`, então `P1` deve ser o caminho de peso mínimo de `s` a `v` e `P2` deve ser o caminho de peso mínimo de `v` a `t`. Caso contrário, poderíamos encontrar um caminho de menor peso de `s` a `v` ou de `v` a `t`, o que resultaria em um caminho de menor peso de `s` a `t`, contradizendo a suposição de que `P` é o caminho de peso mínimo.

3. **Conclusão**: Portanto, a solução ótima para o problema original pode ser construída a partir das soluções ótimas de seus subproblemas, confirmando que o problema possui subestrutura ótima.

### Propriedade da Escolha Gulosa

A propriedade da escolha gulosa significa que uma escolha localmente ótima em cada passo leva a uma solução globalmente ótima.

#### Prova da Propriedade da Escolha Gulosa

1. **Escolha Gulosa**: No algoritmo de Dijkstra, em cada iteração, escolhemos o vértice `u` com a menor distância estimada `d[u]` da origem `s` entre todos os vértices que ainda não foram processados. Esta é uma escolha localmente ótima.

2. **Prova por Contradição**: Suponha que a escolha gulosa de selecionar o vértice `u` com a menor distância estimada `d[u]` não leva a uma solução globalmente ótima. Isso implicaria que existe um caminho de menor peso para algum vértice `v` que não passa por `u`, mas isso contradiz a suposição de que `d[u]` é a menor distância estimada e que todos os caminhos de menor peso para `v` devem passar por `u`.

3. **Conclusão**: Portanto, a escolha gulosa de selecionar o vértice `u` com a menor distância estimada em cada passo leva a uma solução globalmente ótima, confirmando que o algoritmo de Dijkstra possui a propriedade da escolha gulosa.

### Prova Completa

Vamos formalizar a prova de que o algoritmo de Dijkstra encontra o caminho de peso mínimo.

1. **Inicialização**: Inicializamos a distância da origem `s` para todos os vértices como infinita, exceto para `s` que é zero. Usamos uma fila de prioridade para selecionar o vértice com a menor distância estimada.

2. **Iteração**: Em cada iteração, extraímos o vértice `u` com a menor distância estimada `d[u]` da fila de prioridade. Para cada vizinho `v` de `u`, se a distância estimada `d[v]` pode ser reduzida passando por `u`, atualizamos `d[v]`.

3. **Correção**: A cada iteração, garantimos que a distância `d[u]` é a menor distância possível de `s` a `u`. Isso é garantido pela escolha gulosa de selecionar o vértice com a menor distância estimada e pela subestrutura ótima, que garante que a solução ótima para o subproblema de `s` a `u` pode ser estendida para encontrar a solução ótima para o problema original.

4. **Conclusão**: Quando todos os vértices foram processados, as distâncias `d[v]` representam os pesos mínimos dos caminhos de `s` para todos os outros vértices `v` no grafo.

## MST - Kruskal

Para provar que o algoritmo de Kruskal encontra a Árvore Geradora de Peso Mínimo (MST - Minimum Spanning Tree) em um grafo, vamos demonstrar que ele possui subestrutura ótima e a propriedade da escolha gulosa.

### Subestrutura Ótima

A subestrutura ótima significa que a solução ótima para um problema pode ser construída a partir das soluções ótimas de seus subproblemas.

#### Prova da Subestrutura Ótima

1. **Definição de Subproblemas**: Considere uma MST `T` de um grafo `G`. Suponha que `T` seja dividida em duas subárvores `T1` e `T2` ao remover uma aresta `e`.

2. **Subárvores Ótimas**: As subárvores `T1` e `T2` devem ser MSTs dos subgrafos correspondentes de `G`. Caso contrário, poderíamos encontrar uma árvore geradora de menor peso para um dos subgrafos, o que resultaria em uma árvore geradora de menor peso para `G`, contradizendo a suposição de que `T` é uma MST.

3. **Conclusão**: Portanto, a solução ótima para o problema original pode ser construída a partir das soluções ótimas de seus subproblemas, confirmando que o problema possui subestrutura ótima.

### Propriedade da Escolha Gulosa

A propriedade da escolha gulosa significa que uma escolha localmente ótima em cada passo leva a uma solução globalmente ótima.

#### Prova da Propriedade da Escolha Gulosa

1. **Escolha Gulosa**: O algoritmo de Kruskal adiciona arestas ao MST em ordem crescente de peso, garantindo que nenhuma aresta forme um ciclo.

2. **Prova por Contradição**: Suponha que a escolha gulosa de adicionar a aresta de menor peso que não forma um ciclo não leva a uma MST. Isso implicaria que existe uma MST que não inclui a aresta de menor peso, mas inclui uma aresta de maior peso. No entanto, poderíamos substituir a aresta de maior peso pela aresta de menor peso, resultando em uma árvore de menor peso, o que contradiz a suposição de que a árvore original era uma MST.

3. **Conclusão**: Portanto, a escolha gulosa de adicionar a aresta de menor peso que não forma um ciclo leva a uma MST, confirmando que o algoritmo de Kruskal possui a propriedade da escolha gulosa.

### Prova Completa do Algoritmo de Kruskal

Vamos formalizar a prova de que o algoritmo de Kruskal encontra a MST.

#### Passos do Algoritmo de Kruskal

1. **Inicialização**: Inicializamos uma floresta onde cada vértice é uma árvore separada. Ordenamos todas as arestas em ordem crescente de peso.

2. **Iteração**: Em cada iteração, adicionamos a aresta de menor peso que não forma um ciclo na floresta. Usamos uma estrutura de dados de união e busca (union-find) para verificar se a adição de uma aresta forma um ciclo.

3. **Correção**: A cada iteração, garantimos que a aresta adicionada é a de menor peso que não forma um ciclo, mantendo a propriedade de que a floresta é uma MST parcial.

4. **Conclusão**: Quando todas as arestas foram processadas, a floresta se torna uma única árvore, que é a MST do grafo.

#### Prova da Correção

1. **Inicialização**: No início, cada vértice é uma árvore separada, e a floresta é uma coleção de árvores disjuntas.

2. **Escolha Gulosa**: Em cada iteração, escolhemos a aresta de menor peso que não forma um ciclo. Esta escolha é localmente ótima.

3. **Manutenção da Propriedade de MST Parcial**: A cada iteração, ao adicionar a aresta de menor peso que não forma um ciclo, garantimos que a floresta resultante é uma MST parcial. Se adicionássemos uma aresta que forma um ciclo, isso violaria a propriedade de árvore geradora.

4. **Conclusão**: Quando todas as arestas foram processadas, a floresta se torna uma única árvore. Esta árvore é a MST do grafo, pois foi construída adicionando arestas de menor peso que não formam ciclos, garantindo que a solução é globalmente ótima.

### Conclusão

O algoritmo de Kruskal encontra a Árvore Geradora de Peso Mínimo em um grafo porque possui subestrutura ótima e a propriedade da escolha gulosa. A solução ótima para o problema original pode ser construída a partir das soluções ótimas de seus subproblemas, e a escolha localmente ótima em cada passo leva a uma solução globalmente ótima.


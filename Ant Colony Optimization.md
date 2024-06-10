**

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

  

### Conclusão

  

A Árvore de Huffman de Peso Mínimo tem subestrutura ótima e também possui a propriedade da escolha gulosa. A solução ótima para o problema pode ser construída a partir das soluções ótimas de seus subproblemas, e a escolha localmente ótima em cada passo leva a uma solução globalmente ótima.

  
  
**
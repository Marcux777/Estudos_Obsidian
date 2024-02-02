# Árvore de Segmentos
Uma Árvore de Segmentos é uma estrutura de dados que armazena informações sobre intervalos de array como uma árvore. Isso permite responder consultas de intervalo em um array de maneira eficiente, enquanto ainda é flexível o suficiente para permitir a rápida modificação do array. Isso inclui encontrar a soma de elementos consecutivos do array  $a[l \dots r]$ , ou encontrar o elemento mínimo em um intervalo desse tipo em  $O(\log n)$  tempo. Entre responder a essas consultas, a Árvore de Segmentos permite modificar o array substituindo um elemento, ou mesmo alterando os elementos de todo um subsegmento (por exemplo, atribuindo todos os elementos  $a[l \dots r]$  a qualquer valor, ou adicionando um valor a todos os elementos no subsegmento).

Em geral, uma Árvore de Segmentos é uma estrutura de dados muito flexível, e um grande número de problemas pode ser resolvido com ela. Além disso, também é possível aplicar operações mais complexas e responder a consultas mais complexas (veja versões avançadas de Árvores de Segmentos). Em particular, a Árvore de Segmentos pode ser facilmente generalizada para dimensões maiores. Por exemplo, com uma Árvore de Segmentos bidimensional, você pode responder a consultas de soma ou mínimo sobre algum sub-retângulo de uma matriz dada em apenas  
$O(\log^2 n)$  tempo.

Uma propriedade importante das Árvores de Segmentos é que elas requerem apenas uma quantidade linear de memória. A Árvore de Segmentos padrão requer 
$4n$  vértices para trabalhar em um array de tamanho  $n$ .

## Forma mais simples de uma Árvore de Segmentos
Para começar fácil, consideramos a forma mais simples de uma Árvore de Segmentos. Queremos responder eficientemente a consultas de soma. A definição formal de nossa tarefa é: Dado um array  $a[0 \dots n-1]$ , a Árvore de Segmentos deve ser capaz de encontrar a soma dos elementos entre os índices  $l$  e  
$r$  (ou seja, calcular a soma  $\sum_{i=l}^r a[i]$ ), e também lidar com a mudança de valores dos elementos no array (ou seja, realizar atribuições do tipo  $a[i] = x$ ). A Árvore de Segmentos deve ser capaz de processar ambas as consultas em  $O(\log n)$  tempo.

Isso é uma melhoria em relação às abordagens mais simples. Uma implementação de array ingênua - apenas usando um array simples - pode atualizar elementos em  
$O(1)$ , mas requer  $O(n)$  para calcular cada consulta de soma. E somas de prefixos pré-computadas podem calcular consultas de soma em  $O(1)$ , mas a atualização de um elemento do array requer  $O(n)$  alterações nas somas de prefixos.


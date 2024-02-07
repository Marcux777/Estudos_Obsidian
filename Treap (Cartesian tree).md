# Treap (Árvore Cartesiana)
Um treap é uma estrutura de dados que combina árvore binária e heap binário (daí o nome: tree + heap  $\Rightarrow$  Treap).

Mais especificamente, treap é uma estrutura de dados que armazena pares  $(X, Y)$  em uma árvore binária de tal maneira que é uma árvore de busca binária por  $X$  e um heap binário por  $Y$ . Se algum nó da árvore contém valores  $(X_0, Y_0)$ , todos os nós na subárvore esquerda têm  $X \leq X_0$ , todos os nós na subárvore direita têm  $X_0 \leq X$ , e todos os nós em ambas as subárvores esquerda e direita têm  $Y \leq Y_0$ .

Um treap também é frequentemente referido como uma "árvore cartesiana", pois é fácil incorporá-la em um plano cartesiano:
![[Pasted image 20240207183644.png]]

**Treaps foram propostos por Raimund Siedel e Cecilia Aragon em 1989.**

## Vantagens de tal organização de dados
Nessa implementação,  $X$  valores são as chaves (e ao mesmo tempo os valores armazenados no treap), e  $Y$  valores são chamados de prioridades. Sem prioridades, o treap seria uma árvore de busca binária regular por  $X$ , e um conjunto de  $X$  valores poderia corresponder a muitas árvores diferentes, algumas delas degeneradas (por exemplo, na forma de uma lista vinculada), e, portanto, extremamente lentas (as operações principais teriam complexidade  $O(N)$ ).

Ao mesmo tempo, as prioridades (quando são únicas) permitem especificar de forma única a árvore que será construída (claro, não depende da ordem em que os valores são adicionados), o que pode ser provado usando o teorema correspondente. Obviamente, se você escolher as prioridades aleatoriamente, obterá árvores não degeneradas em média, o que garantirá a complexidade  $O(\log N)$  para as operações principais. Daí outro nome desta estrutura de dados - árvore de busca binária randomizada.

## Operações
Um treap fornece as seguintes operações:

- Inserir (X,Y) em  $O(\log N)$ .
	Adiciona um novo nó à árvore. Uma variante possível é passar apenas  $X$  e gerar  $Y$  aleatoriamente dentro da operação.
- Buscar (X) em  $O(\log N)$ .
	Procura um nó com o valor de chave especificado  $X$ . A implementação é a mesma que para uma árvore de busca binária comum.
- Apagar (X) em  $O(\log N)$ .
	Procura um nó com o valor de chave especificado  $X$  e o remove da árvore.
- Construir ( $X_1$ , ...,  $X_N$ ) em  $O(N)$ .
	Constrói uma árvore a partir de uma lista de valores. Isso pode ser feito em tempo linear (assumindo que  $X_1, ..., X_N$  estão ordenados).
- União ( $T_1$ ,  $T_2$ ) em  $O(M \log (N/M))$ .
	Mescla duas árvores, assumindo que todos os elementos são diferentes. É possível alcançar a mesma complexidade se elementos duplicados devem ser removidos durante a mesclagem.
- Interseção ( $T_1$ ,  $T_2$ ) em  $O(M \log (N/M))$ .
	Encontra a interseção de duas árvores (ou seja, seus elementos comuns). Não consideraremos a implementação desta operação aqui.

Além disso, devido ao fato de que um treap é uma árvore de busca binária, ele pode implementar outras operações, como encontrar o  $K$ -ésimo maior elemento ou encontrar o índice de um elemento.

## Descrição da Implementação
Em termos de implementação, cada nó contém  $X$ ,  $Y$  e ponteiros para a esquerda ( $L$ ) e direita ( $R$ ) filhos.

Implementaremos todas as operações necessárias usando apenas duas operações auxiliares: Dividir e Mesclar.

### Dividir

![[Pasted image 20240207184018.png]]

Dividir ( $T$ ,  $X$ ) separa a árvore  $T$  em 2 subárvores  $L$  e  $R$  (que são os valores de retorno de dividir) de modo que  $L$  contém todos os elementos com chave  $X_L \le X$ , e  $R$  contém todos os elementos com chave  $X_R > X$ . Esta operação tem complexidade  $O (\log N)$  e é implementada usando uma recursão limpa:

Se o valor do nó raiz (R) é  $\le X$ , então L consistiria pelo menos de R->L e R. Em seguida, chamamos dividir em R->R, e notamos seu resultado de divisão como L' e R'. Finalmente, L também conteria L', enquanto R = R'.
Se o valor do nó raiz (R) é  $> X$ , então R consistiria pelo menos de R e R->R. Em seguida, chamamos dividir em R->L, e notamos seu resultado de divisão como L' e R'. Finalmente, L=L', enquanto R também conteria R'.
Assim, o algoritmo de divisão é:

1. decidir a qual subárvore o nó raiz pertenceria (esquerda ou direita)
2. chamar recursivamente dividir em um de seus filhos
3. criar o resultado final reutilizando a chamada recursiva de dividir.


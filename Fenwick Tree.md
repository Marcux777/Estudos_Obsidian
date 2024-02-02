# Árvore de Fenwick
Seja,$f$  uma operação de grupo (função associativa binária sobre um conjunto com elemento de identidade e elementos inversos) e  $A$  um array de inteiros de comprimento  $N$ .

A árvore de Fenwick é uma estrutura de dados que:

calcula o valor da função  $f$  no intervalo dado  $[l, r]$  (ou seja,  $f(A_l, A_{l+1}, \dots, A_r)$ ) em  $O(\log N)$  tempo; atualiza o valor de um elemento de  $A$  em  $O(\log N)$  tempo;
requer  $O(N)$  memória, ou em outras palavras, exatamente a mesma memória necessária para  $A$ ; é fácil de usar e codificar, especialmente, no caso de arrays multidimensionais.
A aplicação mais comum da árvore de Fenwick é calcular a soma de um intervalo (ou seja, usando adição sobre o conjunto de inteiros  $\mathbb{Z}$ :  $f(A_1, A_2, \dots, A_k) = A_1 + A_2 + \dots + A_k$ ).

A árvore de Fenwick também é chamada de Árvore Indexada Binária, ou apenas BIT abreviada.

A árvore de Fenwick foi descrita pela primeira vez em um artigo intitulado "Uma nova estrutura de dados para tabelas de frequência cumulativa" (Peter M. Fenwick, 1994).

## Descrição
### Visão Geral
Para simplificar, vamos supor que a função  $f$  seja apenas uma função de soma.

Dado um array de inteiros  $A[0 \dots N-1]$ . Uma árvore de Fenwick é apenas um array  $T[0 \dots N-1]$ , onde cada um de seus elementos é igual à soma dos elementos de  $A$  em algum intervalo  $[g(i), i]$ :
 
$$T_i = \sum_{j = g(i)}^{i}{A_j},$$ 
onde  $g$  é alguma função que satisfaz  $0 \le g(i) \le i$ . Definiremos a função nos próximos parágrafos.

A estrutura de dados é chamada de árvore, porque há uma boa representação da estrutura de dados como árvore, embora não precisemos modelar uma árvore real com nós e arestas. Só precisaremos manter o array  $T$  para lidar com todas as consultas.

Nota: A árvore de Fenwick apresentada aqui usa indexação baseada em zero. Muitas pessoas realmente usarão uma versão da árvore de Fenwick que usa indexação baseada em um. Portanto, você também encontrará uma implementação alternativa usando indexação baseada em um na seção de implementação. Ambas as versões são equivalentes em termos de tempo e complexidade de memória.

Agora podemos escrever algum pseudo-código para as duas operações mencionadas acima - obter a soma dos elementos de  $A$  no intervalo  $[0, r]$  e atualizar (aumentar) algum elemento  $A_i$ :

```
def sum(int r):
    res = 0
    while (r >= 0):
        res += t[r]
        r = g(r) - 1
    return res

def increase(int i, int delta):
    for all j with g(j) <= i <= j:
        t[j] += delta
```
A função sum funciona da seguinte maneira:

1. primeiro, ela adiciona a soma do intervalo  $[g(r), r]$  (ou seja,  $T[r]$ ) ao resultadoentão, ela "pula" para o intervalo  
$[g(g(r)-1), g(r)-1]$ , e adiciona a soma deste intervalo ao resultado
e assim por diante, até que ela "pule" de  
$[0, g(g( \dots g(r)-1 \dots -1)-1)]$  para  
$[g(-1), -1]$ ; é aí que a função sum para de pular.
A função increase funciona com a mesma analogia, mas "pula" na direção de índices crescentes:

as somas dos intervalos  
$[g(j), j]$  que satisfazem a condição  
$g(j) \le i \le j$  são aumentadas por delta , ou seja, t[j] += delta. Portanto, atualizamos todos os elementos em  
$T$  que correspondem a intervalos nos quais  
$A_i$  se encontra.
É óbvio que a complexidade de ambas as funções sum e increase dependem da função  
$g$ . Existem muitas maneiras de escolher a função  
$g$ , desde que  
$0 \le g(i) \le i$  para todos  
$i$ . Por exemplo, a função  
$g(i) = i$  funciona, o que resulta apenas em  
$T = A$ , e, portanto, as consultas de soma são lentas. Também podemos pegar a função  
$g(i) = 0$ . Isso corresponderá a arrays de soma de prefixo, o que significa que encontrar a soma do intervalo  
$[0, i]$  levará apenas tempo constante, mas as atualizações são lentas. A parte inteligente do algoritmo de Fenwick é que ele usa uma definição especial da função  
$g$  que pode lidar com ambas as operações em  
$O(\log N)$  tempo.

Origem: conversa com o Bing, 02/02/2024
(1) github.com. https://github.com/e-maxx-eng/e-maxx-eng/tree/4645c9277053f27a64772119d4e10048c09a188f/src%2Fdata_structures%2Ffenwick.md.
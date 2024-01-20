Claro, aqui está o texto com a formatação corrigida:

Podemos usar a sequência para codificar números inteiros positivos em palavras de código binário. De acordo com o teorema de Zeckendorf, qualquer número natural $n$ pode ser representado de forma única como uma soma de números de Fibonacci:

$$N = F_{k_1} + F_{k_2} + \ldots + F_{k_r}$$
tal que $k_1 \ge k_2 + 2,\ k_2 \ge k_3 + 2,\ \ldots,\ k_r \ge 2$ (ou seja: a representação não pode usar dois números consecutivos de Fibonacci).

Segue-se que qualquer número pode ser codificado de forma única na codificação Fibonacci. E podemos descrever esta representação com códigos binários $d_0 d_1 d_2 \dots d_s 1$, onde $d_i$ é $1$ se $F_{i+2}$ é usado na representação. O código será anexado por um $1$ para indicar o fim da palavra de código. Observe que esta é a única ocorrência onde dois bits 1 consecutivos aparecem.

$$\begin{eqnarray} 1 &=& 1 &=& F_2 &=& (11)_F \\ 2 &=& 2 &=& F_3 &=& (011)_F \\ 6 &=& 5 + 1 &=& F_5 + F_2 &=& (10011)_F \\ 8 &=& 8 &=& F_6 &=& (000011)_F \\ 9 &=& 8 + 1 &=& F_6 + F_2 &=& (100011)_F \\ 19 &=& 13 + 5 + 1 &=& F_7 + F_5 + F_2 &=& (1001011)_F \end{eqnarray}$$
A codificação de um número inteiro $n$ pode ser feita com um algoritmo guloso simples:

1. Itere através dos números de Fibonacci do maior para o menor até encontrar um menor ou igual a $n$.
2. Suponha que este número fosse $F_i$. Subtraia $F_i$ de $n$ e coloque um $1$ na posição $i-2$ da palavra de código (indexando de 0 do bit mais à esquerda para o bit mais à direita).
3. Repita até que não haja resto.
4. Adicione um final $1$ à palavra de código para indicar seu fim.

Para decodificar uma palavra de código, primeiro remova o final $1$. Então, se o bit $i$ estiver definido (indexando de 0 do bit mais à esquerda para o bit mais à direita), some $F_{i+2}$ ao número.
Os números de Fibonacci são definidos da seguinte forma:

$$F_0 = 0, F_1 = 1, F_n = F_{n-1} + F_{n-2}$$
Os primeiros elementos da sequência (OEIS A000045) são:

$$0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...$$
## Propriedades
Os números de Fibonacci possuem muitas propriedades interessantes. Aqui estão algumas delas:

- Identidade de Cassini:
$$F_{n-1} F_{n+1} - F_n^2 = (-1)^n$$
- A regra da "adição":
$$F_{n+k} = F_k F_{n+1} + F_{k-1} F_n$$
- Aplicando a identidade anterior ao caso $k = n$, obtemos:
$$F_{2n} = F_n (F_{n+1} + F_{n-1})$$
- A partir disso, podemos provar por indução que para qualquer número inteiro positivo $k$, $F_{nk}$ é múltiplo de $F_n$.

- O inverso também é verdadeiro: se $F_m$ é múltiplo de $F_n$, então $m$ é múltiplo de $n.$

- Identidade do MDC:

$$GCD(F_m, F_n) = F_{GCD(m, n)}$$
- Os números de Fibonacci são as piores entradas possíveis para o algoritmo euclidiano (veja o teorema de Lame no [algoritmo euclidiano](obsidian://open?vault=Estudos_Obsidian&file=Computa%C3%A7%C3%A3o%2FOne%20for%20All%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum)).

## Fibonacci Coding
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

## Fórmulas para o $n^{\text{ésimo}}$ número de Fibonacci
### Expressão de forma fechada
Existe uma fórmula conhecida como "Fórmula de Binet", embora já fosse conhecida por Moivre:

$$F_n = \frac{\left(\frac{1 + \sqrt{5}}{2}\right)^n - \left(\frac{1 - \sqrt{5}}{2}\right)^n}{\sqrt{5}}$$
Esta fórmula é fácil de provar por indução, mas pode ser deduzida com a ajuda do conceito de funções geradoras ou resolvendo uma equação funcional.

Você pode notar imediatamente que o valor absoluto do segundo termo é sempre menor que $1$, e também diminui muito rapidamente (exponencialmente). Portanto, o valor do primeiro termo sozinho é "quase" $F_n$. Isso pode ser escrito estritamente como:

$$F_n = \left[\frac{\left(\frac{1 + \sqrt{5}}{2}\right)^n}{\sqrt{5}}\right]$$
onde os colchetes denotam arredondamento para o inteiro mais próximo.

Como essas duas fórmulas exigiriam uma precisão muito alta ao trabalhar com números fracionários, elas têm pouco uso em cálculos práticos.

### Fibonacci em tempo linear

O $n^{\text{ésimo}}$ número de Fibonacci pode ser facilmente encontrado em $O(n)$ calculando os números um a um até $n$. No entanto, também existem maneiras mais rápidas, como veremos.

Podemos começar com uma abordagem iterativa, para aproveitar o uso da fórmula $F_n = F_{n-1} + F_{n-2}$, portanto, simplesmente pré-calcularemos esses valores em um array. Levando em conta os casos base para $F_0$ e $F_1$.

```cpp
int fib(int n) {
    int a = 0;
    int b = 1;
    for (int i = 0; i < n; i++) {
        int tmp = a + b;
        a = b;
        b = tmp;
    }
    return a;
}
```
Dessa forma, obtemos uma solução linear, tempo $O(n)$, salvando todos os valores anteriores a $n$ na sequência.
### Forma Matricial - Número de Fibonacci
É fácil provar a seguinte relação:

$$\begin{pmatrix} 1 & 1 \cr 1 & 0 \cr\end{pmatrix} ^ n = \begin{pmatrix} F_{n+1} & F_{n} \cr F_{n} & F_{n-1} \cr\end{pmatrix}$$
Assim, para encontrar $F_n$ em tempo $O(\log n)$, devemos elevar a matriz a n. (Veja Exponenciação Binária)

```cpp
struct matrix {
    long long mat[2][2];
    matrix friend operator *(const matrix &a, const matrix &b){
        matrix c;
        for (int i = 0; i < 2; i++) {
          for (int j = 0; j < 2; j++) {
              c.mat[i][j] = 0;
              for (int k = 0; k < 2; k++) {
                  c.mat[i][j] += a.mat[i][k] * b.mat[k][j];
              }
          }
        }
        return c;
    }
};

matrix matpow(matrix base, long long n) {
    matrix ans{ {
      {1, 0},
      {0, 1}
    } };
    while (n) {
        if(n&1)
            ans = ans*base;
        base = base*base;
        n >>= 1;
    }
    return ans;
}

long long fib(int n) {
    matrix base{ {
      {1, 1},
      {1, 0}
    } };
    return matpow(base, n).mat[0][1];
}
```

### Método de Duplicação Rápida
Expandindo a expressão matricial acima para $n = 2\cdot k$

$$ \begin{pmatrix} F_{2k+1} & F_{2k}\\ F_{2k} & F_{2k-1} \end{pmatrix} = \begin{pmatrix} 1 & 1\\ 1 & 0 \end{pmatrix}^{2k} = \begin{pmatrix} F_{k+1} & F_{k}\\ F_{k} & F_{k-1} \end{pmatrix} ^2 $$
podemos encontrar estas equações mais simples:

$$ \begin{align} F_{2k+1} &= F_{k+1}^2 + F_{k}^2 \\ F_{2k} &= F_k(F_{k+1}+F_{k-1}) = F_k (2F_{k+1} - F_{k})\\ \end{align}.$$
Assim, usando as duas equações acima, os números de Fibonacci podem ser facilmente calculados pelo seguinte código:

```cpp
pair<int, int> fib (int n) {
    if (n == 0)
        return {0, 1};

    auto p = fib(n >> 1);
    int c = p.first * (2 * p.second - p.first);
    int d = p.first * p.first + p.second * p.second;
    if (n & 1)
        return {d, c + d};
    else
        return {c, d};
}
```
O código acima retorna $F_n$ e $F_{n+1}$ como um par.

## Periodicidade módulo $p$ - Número de Fibonacci
Considere a sequência de Fibonacci módulo $p$. Vamos provar que a sequência é periódica.

Vamos provar isso por contradição. Considere os primeiros $p^2 + 1$ pares de números de Fibonacci tomados módulo $p$:

$$(F_0,\ F_1),\ (F_1,\ F_2),\ \ldots,\ (F_{p^2},\ F_{p^2 + 1})$$
Só pode haver $p$ restos diferentes módulo $p$, e no máximo $p^2$ pares diferentes de restos, então há pelo menos dois pares idênticos entre eles. Isso é suficiente para provar que a sequência é periódica, pois um número de Fibonacci é determinado apenas por seus dois predecessores. Portanto, se dois pares de números consecutivos se repetem, isso também significaria que os números após o par se repetirão da mesma maneira.

Agora escolhemos dois pares de restos idênticos com os menores índices na sequência. Deixe os pares serem $(F_a,\ F_{a + 1})$ e $(F_b,\ F_{b + 1})$. Vamos provar que $a = 0$. Se isso fosse falso, haveria dois pares anteriores $(F_{a-1},\ F_a)$ e $(F_{b-1},\ F_b)$, que, pela propriedade dos números de Fibonacci, também seriam iguais. No entanto, isso contradiz o fato de termos escolhido pares com os menores índices, completando nossa prova de que não há pré-período (ou seja, os números são periódicos a partir de $F_0$).
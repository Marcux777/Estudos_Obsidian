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

1. primeiro, ela adiciona a soma do intervalo  $[g(r), r]$  (ou seja,  $T[r]$ ) ao resultado
2. então, ela "pula" para o intervalo  $[g(g(r)-1), g(r)-1]$ , e adiciona a soma deste intervalo ao resultado
3. e assim por diante, até que ela "pule" de  $[0, g(g( \dots g(r)-1 \dots -1)-1)]$  para  $[g(-1), -1]$ ; é aí que a função sum para de pular.
A função increase funciona com a mesma analogia, mas "pula" na direção de índices crescentes:

1. as somas dos intervalos  $[g(j), j]$  que satisfazem a condição  $g(j) \le i \le j$  são aumentadas por delta , ou seja, t[j] += delta. Portanto, atualizamos todos os elementos em  $T$  que correspondem a intervalos nos quais  $A_i$  se encontra.
É óbvio que a complexidade de ambas as funções sum e increase dependem da função  $g$ . Existem muitas maneiras de escolher a função  $g$ , desde que  $0 \le g(i) \le i$  para todos  $i$ . Por exemplo, a função $g(i) = i$  funciona, o que resulta apenas em  $T = A$ , e, portanto, as consultas de soma são lentas. Também podemos pegar a função  $g(i) = 0$ . Isso corresponderá a arrays de soma de prefixo, o que significa que encontrar a soma do intervalo  $[0, i]$  levará apenas tempo constante, mas as atualizações são lentas. A parte inteligente do algoritmo de Fenwick é que ele usa uma definição especial da função  $g$  que pode lidar com ambas as operações em  $O(\log N)$  tempo.

### Definição de  $g(i)$ 
O cálculo de  $g(i)$  é definido usando a seguinte operação simples: substituímos todos os bits finais  $1$  na representação binária de  $i$  por bits  $0$ .

Em outras palavras, se o dígito menos significativo de  $i$  em binário for  $0$ , então  $g(i) = i$ . Caso contrário, o dígito menos significativo é um  $1$ , e pegamos este  $1$  e todos os outros  $1$ s finais e os invertemos.

Por exemplo, temos
 
$$\begin{align} g(11) = g(1011_2) = 1000_2 &= 8 \\\\ g(12) = g(1100_2) = 1100_2 &= 12 \\\\ g(13) = g(1101_2) = 1100_2 &= 12 \\\\ g(14) = g(1110_2) = 1110_2 &= 14 \\\\ g(15) = g(1111_2) = 0000_2 &= 0 \\\\ \end{align}$$ 
Existe uma implementação simples usando operações bitwise para a operação não trivial descrita acima:
 
$$g(i) = i ~\&~ (i+1),$$ 
onde  $\&$  é o operador AND bitwise. Não é difícil convencer-se de que esta solução faz a mesma coisa que a operação descrita acima.

Agora, só precisamos encontrar uma maneira de iterar sobre todos os  $j$ 's, de modo que  $g(j) \le i \le j$ .

É fácil ver que podemos encontrar todos esses  $j$ 's começando com  $i$  e invertendo o último bit não definido. Chamaremos esta operação de  $h(j)$ . Por exemplo, para  $i = 10$  temos:
 
 
$$\begin{align} 10 &= 0001010_2 \\\\ h(10) = 11 &= 0001011_2 \\\\ h(11) = 15 &= 0001111_2 \\\\ h(15) = 31 &= 0011111_2 \\\\ h(31) = 63 &= 0111111_2 \\\\ \vdots & \end{align}$$ 
Sem surpresa, também existe uma maneira simples de realizar  $h$  usando operações bitwise:
 
$$h(j) = j ~\|~ (j+1),$$ 
onde  $\|$  é o operador OR bitwise.

A imagem a seguir mostra uma possível interpretação da árvore de Fenwick como árvore. Os nós da árvore mostram os intervalos que cobrem.

![[Pasted image 20240202032745.png]]

## Implementação
### Encontrando a soma em um array unidimensional
Aqui apresentamos uma implementação da árvore de Fenwick para consultas de soma e atualizações únicas.

A árvore de Fenwick normal só pode responder consultas de soma do tipo  $[0, r]$  usando sum(int r), no entanto, também podemos responder outras consultas do tipo  $[l, r]$  calculando duas somas  $[0, r]$  e  $[0, l-1]$  e subtraindo-as. Isso é tratado no método sum(int l, int r).

Além disso, esta implementação suporta dois construtores. Você pode criar uma árvore de Fenwick inicializada com zeros, ou pode converter um array existente na forma de Fenwick.

```cpp
struct FenwickTree {
    vector<int> bit;  // árvore indexada binária
    int n;

    FenwickTree(int n) {
        this->n = n;
        bit.assign(n, 0);
    }

    FenwickTree(vector<int> const &a) : FenwickTree(a.size()) {
        for (size_t i = 0; i < a.size(); i++)
            add(i, a[i]);
    }

    int sum(int r) {
        int ret = 0;
        for (; r >= 0; r = (r & (r + 1)) - 1)
            ret += bit[r];
        return ret;
    }

    int sum(int l, int r) {
        return sum(r) - sum(l - 1);
    }

    void add(int idx, int delta) {
        for (; idx < n; idx = idx | (idx + 1))
            bit[idx] += delta;
    }
};
```
### Construção Linear
A implementação acima requer  $O(N \log N)$  tempo. É possível melhorar isso para  $O(N)$  tempo.

A ideia é que o número  $a[i]$  no índice  $i$  contribuirá para o intervalo armazenado em $bit[i]$ , e para todos os intervalos que o índice  $i | (i + 1)$  contribui. Então, ao adicionar os números em ordem, você só precisa empurrar a soma atual mais para o próximo intervalo, onde então será empurrada mais para o próximo intervalo, e assim por diante.

```cpp
FenwickTree(vector<int> const &a) : FenwickTree(a.size()){
    for (int i = 0; i < n; i++) {
        bit[i] += a[i];
        int r = i | (i + 1);
        if (r < n) bit[r] += bit[i];
    }
}
```
### Encontrando o mínimo de  $[0, r]$  em um array unidimensional
É óbvio que não há uma maneira fácil de encontrar o mínimo do intervalo  $[l, r]$  usando a árvore de Fenwick, pois a árvore de Fenwick só pode responder consultas do tipo  $[0, r]$ . Além disso, cada vez que um valor é atualizado, o novo valor tem que ser menor que o valor atual. Ambas as limitações significativas são porque a operação  $min$  junto com o conjunto de inteiros não forma um grupo, pois não há elementos inversos.

```cpp
struct FenwickTreeMin {
    vector<int> bit;
    int n;
    const int INF = (int)1e9;

    FenwickTreeMin(int n) {
        this->n = n;
        bit.assign(n, INF);
    }

    FenwickTreeMin(vector<int> a) : FenwickTreeMin(a.size()) {
        for (size_t i = 0; i < a.size(); i++)
            update(i, a[i]);
    }

    int getmin(int r) {
        int ret = INF;
        for (; r >= 0; r = (r & (r + 1)) - 1)
            ret = min(ret, bit[r]);
        return ret;
    }

    void update(int idx, int val) {
        for (; idx < n; idx = idx | (idx + 1))
            bit[idx] = min(bit[idx], val);
    }
};
```
Nota: é possível implementar uma árvore de Fenwick que pode lidar com consultas mínimas de intervalo arbitrário e atualizações arbitrárias. O artigo [[Efficient Range Minimum Queries using Binary Indexed Trees]] descreve tal abordagem. No entanto, com essa abordagem, você precisa manter uma segunda árvore indexada binária sobre os dados, com uma estrutura ligeiramente diferente, já que uma árvore não é suficiente para armazenar os valores de todos os elementos no array. A implementação também é muito mais difícil em comparação com a implementação normal para somas.

### Encontrando a soma em um array bidimensional
Como afirmado antes, é muito fácil implementar a Árvore de Fenwick para um array multidimensional.

```cpp
struct FenwickTree2D {
    vector<vector<int>> bit;
    int n, m;

    // init(...) { ... }

    int sum(int x, int y) {
        int ret = 0;
        for (int i = x; i >= 0; i = (i & (i + 1)) - 1)
            for (int j = y; j >= 0; j = (j & (j + 1)) - 1)
                ret += bit[i][j];
        return ret;
    }

    void add(int x, int y, int delta) {
        for (int i = x; i < n; i = i | (i + 1))
            for (int j = y; j < m; j = j | (j + 1))
                bit[i][j] += delta;
    }
};
```
### Abordagem de indexação baseada em um
Para esta abordagem, mudamos um pouco os requisitos e a definição para  $T[]$ e  $g()$. Queremos que  $T[i]$  armazene a soma de  $[g(i)+1; i]$ . Isso muda um pouco a implementação e permite uma definição semelhante e agradável para  $g(i)$ :

```cpp
def sum(int r):
    res = 0
    while (r > 0):
        res += t[r]
        r = g(r)
    return res

def increase(int i, int delta):
    for all j with g(j) < i <= j:
        t[j] += delta
```
O cálculo de  $g(i)$  é definido como: alternância do último bit definido  $1$  na representação binária de  $i$ .
 
$$\begin{align} g(7) = g(111_2) = 110_2 &= 6 \\\\ g(6) = g(110_2) = 100_2 &= 4 \\\\ g(4) = g(100_2) = 000_2 &= 0 \\\\ \end{align}$$ 
O último bit definido pode ser extraído usando  $i ~\&~ (-i)$ , então a operação pode ser expressa como:

 
$$g(i) = i - (i ~\&~ (-i)).$$ 
E não é difícil ver que você precisa mudar todos os valores  $T[j]$  na sequência  $i,~ h(i),~ h(h(i)),~ \dots$  quando você quer atualizar  $A[j]$ , onde  $h(i)$  é definido como:
 
$$h(i) = i + (i ~\&~ (-i)).$$ 
Como você pode ver, o principal benefício desta abordagem é que as operações binárias se complementam muito bem.

A seguinte implementação pode ser usada como as outras implementações, no entanto, ela usa indexação baseada em um internamente.

```cpp
struct FenwickTreeOneBasedIndexing {
    vector<int> bit;  // árvore indexada binária
    int n;

    FenwickTreeOneBasedIndexing(int n) {
        this->n = n + 1;
        bit.assign(n + 1, 0);
    }

    FenwickTreeOneBasedIndexing(vector<int> a)
        : FenwickTreeOneBasedIndexing(a.size()) {
        for (size_t i = 0; i < a.size(); i++)
            add(i, a[i]);
    }

    int sum(int idx) {
        int ret = 0;
        for (++idx; idx > 0; idx -= idx & -idx)
            ret += bit[idx];
        return ret;
    }

    int sum(int l, int r) {
        return sum(r) - sum(l - 1);
    }

    void add(int idx, int delta) {
        for (++idx; idx < n; idx += idx & -idx)
            bit[idx] += delta;
    }
};
```



## Operações de intervalo
Uma árvore de Fenwick pode suportar as seguintes operações de intervalo:

1. Atualização de Ponto e Consulta de Intervalo
2. Atualização de Intervalo e Consulta de Ponto
3. Atualização de Intervalo e Consulta de Intervalo
#### 1. Atualização de Ponto e Consulta de Intervalo
Esta é apenas a árvore de Fenwick comum, conforme explicado acima.

#### 2. Atualização de Intervalo e Consulta de Ponto
Usando truques simples, também podemos fazer as operações inversas: aumentar intervalos e consultar valores únicos.

Deixe a árvore de Fenwick ser inicializada com zeros. Suponha que queremos incrementar o intervalo  $[l, r]$  por  $x$ . Fazemos duas operações de atualização de ponto na árvore de Fenwick que são add(l, x) e add(r+1, -x).

Se quisermos obter o valor de  $A[i]$ , só precisamos pegar a soma do prefixo usando o método de soma de intervalo comum. Para ver por que isso é verdade, podemos apenas nos concentrar na operação de incremento anterior novamente. Se  $i < l$ , então as duas operações de atualização não têm efeito na consulta e obtemos a soma  $0$ . Se  $i \in [l, r]$ , então obtemos a resposta  $x$  por causa da primeira operação de atualização. E se  $i > r$ , então a segunda operação de atualização cancelará o efeito da primeira.

A seguinte implementação usa indexação baseada em um.

```cpp
void add(int idx, int val) {
    for (++idx; idx < n; idx += idx & -idx)
        bit[idx] += val;
}

void range_add(int l, int r, int val) {
    add(l, val);
    add(r + 1, -val);
}

int point_query(int idx) {
    int ret = 0;
    for (++idx; idx > 0; idx -= idx & -idx)
        ret += bit[idx];
    return ret;
}
```
Nota: claro, também é possível aumentar um único ponto  $A[i]$  com range_add(i, i, val).

#### 3. Atualizações de Intervalo e Consultas de Intervalo
Para suportar ambas as atualizações de intervalo e consultas de intervalo, usaremos dois BITs, a saber  $B_1[]$  e  $B_2[]$ , inicializados com zeros.

Suponha que queremos incrementar o intervalo  $[l, r]$  pelo valor  $x$ . De forma semelhante ao método anterior, realizamos duas operações de atualização de ponto em  $B_1$ : add(B1, l, x) e add(B1, r+1, -x). E também atualizamos  $B_2$ . Os detalhes serão explicados mais tarde.

```cpp
def range_add(l, r, x):
    add(B1, l, x)
    add(B1, r+1, -x)
    add(B2, l, x*(l-1))
    add(B2, r+1, -x*r))
```
Após a atualização de intervalo  $(l, r, x)$  a consulta de soma de intervalo deve retornar os seguintes valores:
 
$$ sum[0, i]= \begin{cases} 0 & i < l \\\\ x \cdot (i-(l-1)) & l \le i \le r \\\\ x \cdot (r-l+1) & i > r \\\\ \end{cases} $$ 
Podemos escrever a soma do intervalo como diferença de dois termos, onde usamos  $B_1$  para o primeiro termo e  $B_2$  para o segundo termo. A diferença das consultas nos dará a soma do prefixo sobre  $[0, i]$ .
 
$$\begin{align} sum[0, i] &= sum(B_1, i) \cdot i - sum(B_2, i) \\\\ &= \begin{cases} 0 \cdot i - 0 & i < l\\\\ x \cdot i - x \cdot (l-1) & l \le i \le r \\\\ 0 \cdot i - (x \cdot (l-1) - x \cdot r) & i > r \\\\ \end{cases} \end{align} $$ 
A última expressão é exatamente igual aos termos requeridos. Assim, podemos usar  
$B_2$  para eliminar termos extras quando multiplicamos  $B_1[i]\times i$ .

Podemos encontrar somas de intervalo arbitrárias calculando as somas de prefixo para  $l-1$  e  $r$  e pegando a diferença delas novamente.

```cpp
def add(b, idx, x):
    while idx <= N:
        b[idx] += x
        idx += idx & -idx

def range_add(l,r,x):
    add(B1, l, x)
    add(B1, r+1, -x)
    add(B2, l, x*(l-1))
    add(B2, r+1, -x*r)

def sum(b, idx):
    total = 0
    while idx > 0:
        total += b[idx]
        idx -= idx & -idx
    return total

def prefix_sum(idx):
    return sum(B1, idx)*idx -  sum(B2, idx)

def range_sum(l, r):
    return prefix_sum(r) - prefix_sum(l-1)
```


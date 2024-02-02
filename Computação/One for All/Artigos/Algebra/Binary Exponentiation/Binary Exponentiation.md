É um método para realizar cálculos de  $a^n$ usando $O(log n)$ multiplicações, ao invés de $O(n)$ como o de costume.
Também possui aplicações importantes em muitas tarefas não relacionadas à aritmética, uma vez que pode ser utilizado com quaisquer operações que possuam a propriedade de associatividade:

$(X.Y).Z = X.(Y.Z)$
## **Algoritmo**

Elevar $a$ à potência de $n$ é expresso de forma ingênua como multiplicação por $a$ feita $n-1$ vezes: $a^{n} = a \cdot a \cdot \ldots \cdot a$. No entanto, essa abordagem não é prática para valores grandes de $a$ ou $n$.

$(a^{b+c} = a^b \cdot a^c)$ e $(a^{2b} = a^b \cdot a^b = (a^b)^2).$

A ideia da exponenciação binária é dividir o trabalho usando a representação binária do expoente.

Vamos escrever $n$ na base 2, por exemplo:

$3^{13} = 3^{1101_{2}} = 3^{8} . 3^{4} . 3^{1}$

Dado que o número $n$ possui exatamente $(\lfloor \log_2 n \rfloor + 1)$ dígitos na base 2, só precisamos realizar $(O(\log n))$ multiplicações, se soubermos as potências $(a^1, a^2, a^4, a^8, \dots, a^{2^{\lfloor \log n \rfloor}}).$

Portanto, só precisamos conhecer uma maneira rápida de calcular essas potências. Felizmente, isso é muito fácil, uma vez que um elemento na sequência é simplesmente o quadrado do elemento anterior.

$$\begin{align} 3^1 &= 3 \\ 3^2 &= \left(3^1\right)^2 = 3^2 = 9 \\ 3^4 &= \left(3^2\right)^2 = 9^2 = 81 \\ 3^8 &= \left(3^4\right)^2 = 81^2 = 6561 \end{align}$$ 
Portanto, para obter a resposta final para$3^{13}$ , precisamos apenas multiplicar três deles (pulando$3^2$  porque o bit correspondente em$n$  não está definido):
$3^{13} = 6561 \cdot 81 \cdot 3 = 1594323$ 

A complexidade final deste algoritmo é$O(\log n)$ : precisamos calcular$\log n$  potências de
$a$ , e então temos que fazer no máximo$\log n$  multiplicações para obter a resposta final delas.

A seguinte abordagem recursiva expressa a mesma ideia:

$$a^n = \begin{cases}
1 &\text{se } n == 0 \\
\left(a^{\frac{n}{2}}\right)^2 &\text{se } n > 0 \text{ e } n \text{ par}\\
\left(a^{\frac{n - 1}{2}}\right)^2 \cdot a &\text{se } n > 0 \text{ e } n \text{ ímpar}\\
\end{cases}$$

## Implementação

Primeiro, a abordagem recursiva, que é uma tradução direta da fórmula recursiva:

```c++
long long binpow(long long a, long long b) {
    if (b == 0)
        return 1;
    long long res = binpow(a, b / 2);
    if (b % 2)
        return res * res * a;
    else
        return res * res;
}
```

A segunda abordagem realiza a mesma tarefa sem recursão. Ela calcula todas as potências em um loop e multiplica as que têm o bit correspondente definido em $n$. Embora a complexidade de ambas as abordagens seja idêntica, esta abordagem será mais rápida na prática, pois não temos o overhead das chamadas recursivas.

```c++
long long binpow(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a;
        a = a * a;
        b >>= 1;
    }
    return res;
}
```



## Aplicações
### Cálculo efetivo de grandes expoentes em módulo de um número
#### Problema: Calcular $x^n \mod m$.
Esta é uma operação muito comum. Por exemplo, é usada no cálculo do inverso multiplicativo modular.
#### Solução: 
Como sabemos que o operador módulo não interfere nas multiplicações ($a \cdot b \equiv (a \mod m) \cdot (b \mod m) \pmod m$), podemos usar diretamente o mesmo código e apenas substituir cada multiplicação por uma multiplicação modular:

```cpp
long long binpow(long long a, long long b, long long m) {
    a %= m;
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a % m;
        a = a * a % m;
        b >>= 1;
    }
    return res;
}
````

##### Nota:
É possível acelerar este algoritmo para grandes $b >> m$. Se $m$ for um número primo,$x^n \equiv x^{n\mod(m-1)} \pmod{m}$ para primo $m$, e $x^n \equiv x^{n \mod{\phi(m)}} \pmod{m}$ para composto $m$. Isso segue diretamente do pequeno teorema de Fermat e do teorema de Euler, veja o artigo sobre Inversos Modulares para mais detalhes.

### Cálculo efetivo dos números de Fibonacci
#### Problema: Calcular o n-ésimo número de Fibonacci $F_n$.
#### Solução:
Para mais detalhes, veja o artigo sobre o [[Número de Fibonacci|Número de Fibonacci]]. Vamos apenas passar por uma visão geral do algoritmo. Para calcular o próximo número de Fibonacci, apenas os dois anteriores são necessários, como $F_n = F_{n-1} + F_{n-2}$. Podemos construir uma matriz $2 \times 2$ que descreve essa transformação: a transição de $F_i$ e $F_{i+1}$ para $F_{i+1}$ e $F_{i+2}$. Por exemplo, aplicando essa transformação ao par $F_0$ e $F_1$ mudaria para $F_1$ e $F_2$. Portanto, podemos elevar essa matriz de transformação à potência n-ésima para encontrar $F_n$ em complexidade de tempo $O(\log n)$.

### Aplicando uma permutação $k$ vezes
#### Problema: 
Você recebe uma sequência de comprimento $n$. Aplique a ela uma permutação dada $k$ vezes.

#### Solução: 
Basta elevar a permutação à potência $k$ usando a exponenciação binária e, em seguida, aplicá-la à sequência. Isso resultará em uma complexidade de tempo de $O(n \log k)$.

```cpp
vector<int> applyPermutation(vector<int> sequence, vector<int> permutation) {
    vector<int> newSequence(sequence.size());
    for(int i = 0; i < sequence.size(); i++) {
        newSequence[i] = sequence[permutation[i]];
    }
    return newSequence;
}

vector<int> permute(vector<int> sequence, vector<int> permutation, long long k) {
    while (k > 0) {
        if (k & 1) {
            sequence = applyPermutation(sequence, permutation);
        }
        permutation = applyPermutation(permutation, permutation);
        k >>= 1;
    }
    return sequence;
}
```

##### Nota:
Esta tarefa pode ser resolvida de forma mais eficiente em tempo linear, construindo o gráfico de permutação e considerando cada ciclo independentemente. Você poderia então calcular k módulo o tamanho do ciclo e encontrar a posição final para cada número que faz parte deste ciclo.

### Aplicação rápida de um conjunto de operações geométricas a um conjunto de pontos
#### Problema: 
Dado $n$ pontos $p_i$, aplique $m$ transformações a cada um desses pontos. Cada transformação pode ser um deslocamento, uma escala ou uma rotação em torno de um eixo dado por um ângulo dado. Há também uma operação de "loop" que aplica uma lista dada de transformações $k$ vezes (as operações de "loop" podem ser aninhadas). Você deve aplicar todas as transformações mais rápido que $O(n \cdot length)$, onde $length$ é o número total de transformações a serem aplicadas (após desenrolar as operações de "loop").

#### Solução: 
Vamos ver como os diferentes tipos de transformações mudam as coordenadas:

- Operação de deslocamento: adiciona uma constante diferente a cada uma das coordenadas.
- Operação de escala: multiplica cada uma das coordenadas por uma constante diferente.
- Operação de rotação: a transformação é mais complicada (não vamos entrar em detalhes aqui), mas cada uma das novas coordenadas ainda pode ser representada como uma combinação linear das antigas.

Como você pode ver, cada uma das transformações pode ser representada como uma operação linear nas coordenadas. Assim, uma transformação pode ser escrita como uma matriz $4 \times 4$ da forma:

$$\begin{pmatrix} a_{11} & a_ {12} & a_ {13} & a_ {14} \\ a_{21} & a_ {22} & a_ {23} & a_ {24} \\ a_{31} & a_ {32} & a_ {33} & a_ {34} \\ a_{41} & a_ {42} & a_ {43} & a_ {44} \end{pmatrix}$$

que, quando multiplicada por um vetor com as coordenadas antigas e uma unidade, dá um novo vetor com as novas coordenadas e uma unidade:

$$\begin{pmatrix} x & y & z & 1 \end{pmatrix} \cdot \begin{pmatrix} a_{11} & a_ {12} & a_ {13} & a_ {14} \\ a_{21} & a_ {22} & a_ {23} & a_ {24} \\ a_{31} & a_ {32} & a_ {33} & a_ {34} \\ a_{41} & a_ {42} & a_ {43} & a_ {44} \end{pmatrix} = \begin{pmatrix} x' & y' & z' & 1 \end{pmatrix}$$

(Por que introduzir uma quarta coordenada fictícia, você pergunta? Essa é a beleza das [[Coordenadas Homogêneas]], que encontram grande aplicação em gráficos de computador. Sem isso, não seria possível implementar operações afins como a operação de deslocamento como uma única multiplicação de matriz, pois requer que adicionemos uma constante às coordenadas. A transformação afim se torna uma transformação linear na dimensão superior!)

Aqui estão alguns exemplos de como as transformações são representadas na forma de matriz:

- Operação de deslocamento: desloca a coordenada $x$ por $5$, a coordenada $y$ por $7$ e a coordenada $z$ por $9$.

$$\begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 5 & 7 & 9 & 1 \end{pmatrix}$$

- Operação de escala: escala a coordenada $x$ por $10$ e as outras duas por $5$.

$$\begin{pmatrix} 10 & 0 & 0 & 0 \\ 0 & 5 & 0 & 0 \\ 0 & 0 & 5 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

- Operação de rotação: rotaciona $\theta$ graus em torno do eixo $x$ seguindo a regra da mão direita (direção anti-horária).

$$\begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & \cos \theta & -\sin \theta & 0 \\ 0 & \sin \theta & \cos \theta & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

Agora, uma vez que cada transformação é descrita como uma matriz, a sequência de transformações pode ser descrita como um produto dessas matrizes, e um "loop" de $k$ repetições pode ser descrito como a matriz elevada à potência de $k$ (que pode ser calculada usando exponenciação binária em $O(\log{k})$). Desta forma, a matriz que representa todas as transformações pode ser calculada primeiro em $O(m \log{k})$, e então ela pode ser aplicada a cada um dos $n$ pontos em $O(n)$ para uma complexidade total de $O(n + m \log{k})$.



### Número de caminhos de comprimento $k$ em um grafo
#### Problema: 
Dado um grafo direcionado não ponderado de $n$ vértices, encontre o número de caminhos de comprimento $k$ de qualquer vértice $u$ para qualquer outro vértice $v$.

#### Solução: 
Este problema é considerado em mais detalhes em um [artigo separado](obsidian://open?vault=Algoritmos&file=algoritmos%2FArtigos%2FNumber%20of%20paths%20of%20fixed%20length). O algoritmo consiste em elevar a matriz de adjacência $M$ do grafo (uma matriz onde $m_{ij} = 1$ se houver uma aresta de $i$ para $j$, ou $0$ caso contrário) à potência $k$. Agora $m_{ij}$ será o número de caminhos de comprimento $k$ de $i$ para $j$. A complexidade de tempo desta solução é $O(n^3 \log k)$.

##### Nota: 
No mesmo artigo, outra variação deste problema é considerada: quando as arestas são ponderadas e é necessário encontrar o caminho de peso mínimo contendo exatamente $k$ arestas. Como mostrado nesse artigo, este problema também é resolvido pela exponenciação da matriz de adjacência. A matriz teria o peso da aresta de $i$ para $j$, ou $\infty$ se não houver tal aresta. Em vez da operação usual de multiplicação de duas matrizes, deve ser usada uma modificada: em vez de multiplicação, ambos os valores são adicionados, e em vez de uma soma, um mínimo é tomado. Ou seja: 

$$result_{ij} = \min\limits_{1\ \leq\ k\ \leq\ n}(a_{ik} + b_{kj})$$



### Variação da exponenciação binária: multiplicando dois números módulo $m$
#### Problema: 
Multiplicar dois números $a$ e $b$ módulo $m$. $a$ e $b$ se encaixam nos tipos de dados integrados, mas o produto deles é grande demais para caber em um inteiro de 64 bits. A ideia é calcular $a \cdot b \pmod m$ sem usar aritmética de números grandes.

#### Solução: 
Simplesmente aplicamos o algoritmo de construção binária descrito acima, realizando apenas adições em vez de multiplicações. Em outras palavras, "expandimos" a multiplicação de dois números para $O (\log m)$ operações de adição e multiplicação por dois (que, em essência, é uma adição).

$$a \cdot b = \begin{cases} 0 &\text{se }a = 0 \\ 2 \cdot \frac{a}{2} \cdot b &\text{se }a > 0 \text{ e }a \text{ par} \\ 2 \cdot \frac{a-1}{2} \cdot b + b &\text{se }a > 0 \text{ e }a \text{ ímpar} \end{cases}$$

##### Nota: 
Você pode resolver esta tarefa de uma maneira diferente usando operações de ponto flutuante. Primeiro, calcule a expressão $\frac{a \cdot b}{m}$ usando números de ponto flutuante e converta-o em um inteiro sem sinal $q$. Subtraia $q \cdot m$ de $a \cdot b$ usando aritmética de inteiro sem sinal e tome-o módulo $m$ para encontrar a resposta. Esta solução parece bastante pouco confiável, mas é muito rápida e muito fácil de implementar. Veja [aqui](https://cs.stackexchange.com/questions/77016/modular-multiplication) para mais informações.

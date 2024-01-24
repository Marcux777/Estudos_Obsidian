## Operações em Polinômios e Séries

Problemas em programação competitiva, especialmente aqueles envolvendo enumeração de algum tipo, são frequentemente resolvidos ao reduzir o problema para o cálculo de algo em polinômios e séries formais de potências.

Isso inclui conceitos como multiplicação de polinômios, interpolação e operações mais complicadas, como logaritmos e exponenciais de polinômios. Neste artigo, é apresentada uma visão geral breve dessas operações e das abordagens comuns para resolvê-las.

## Noções Básicas e Fatos

Nesta seção, focamos mais nas definições e propriedades "intuitivas" de várias operações polinomiais. Os detalhes técnicos de implementação e complexidades serão abordados em seções posteriores.

[[Polynomial multiplication]]

[[Formal power series]]

[[Long polynomial division]]

## Basic implementation

Aqui está a implementação básica da álgebra de polinômios.

Ela suporta todas as operações triviais e alguns outros métodos úteis. A classe principal é `poly<T>` para polinômios com coeficientes do tipo T.

Todas as operações aritméticas +, -, *, % e / são suportadas, % e / representando o resto e o quociente na divisão euclidiana.

Também há a classe `modular<m>` para realizar operações aritméticas em restos módulo um número primo m.

Outras funções úteis:

- `deriv()`: calcula a derivada  $P'(x)$  de  $P(x)$ .
- `integr()`: calcula a integral indefinida  $Q(x) = \int P(x)$  de  $P(x)$  tal que  $Q(0)=0$ .
- `inv(size_t n)`: calcula os primeiros  $n$  coeficientes de  $P^{-1}(x)$  em  $O(n \log n)$ .
- `log(size_t n)`: calcula os primeiros  $n$  coeficientes de  $\ln P(x)$  em  $O(n \log n)$ .
- `exp(size_t n)`: calcula os primeiros  $n$  coeficientes de  $\exp P(x)$  em  $O(n \log n)$ .
- `pow(size_t k, size_t n)`: calcula os primeiros  $n$  coeficientes para  $P^{k}(x)$  em  $O(n \log nk)$ .
- `deg()`: retorna o grau de  $P(x)$ .
- `lead()`: retorna o coeficiente de  $x^{\deg P(x)}$ .
- `resultant(poly<T> a, poly<T> b)`: calcula o resultado de  $a$  e  $b$  em  $O(|a| \cdot |b|)$ .
- `bpow(T x, size_t n)`: calcula  $x^n$ .
- `bpow(T x, size_t n, T m)`: calcula  $x^n \pmod{m}$ .
- `chirpz(T z, size_t n)`: calcula $P(1), P(z), P(z^2), \dots, P(z^{n-1})$  em  $O(n \log n)$ .
- `vector<T> eval(vector<T> x)`: avalia  $P(x_1), \dots, P(x_n)$  em  $O(n \log^2 n)$ .
- `poly<T> inter(vector<T> x, vector<T> y)`: interpola um polinômio por um conjunto de pares  $P(x_i) = y_i$  em  $O(n \log^2 n)$ .

E mais algumas, sinta-se à vontade para explorar o código!



## Arithmetic
### Multiplication
A operação fundamental é a multiplicação de dois polinômios. Ou seja, dados os polinômios  $A$  e  $B$ :
 
$$A = a_0 + a_1 x + \dots + a_n x^n$$ 
$$B = b_0 + b_1 x + \dots + b_m x^m$$ 
Você precisa calcular o polinômio  $C = A \cdot B$ , que é definido como
$$\boxed{C = \sum\limits_{i=0}^n \sum\limits_{j=0}^m a_i b_j x^{i+j}} = c_0 + c_1 x + \dots + c_{n+m} x^{n+m}.$$ 
Isso pode ser calculado em  $O(n \log n)$  através da Transformada Rápida de Fourier, e quase todos os métodos aqui a utilizarão como sub-rotina.

### Série inversa
Se  $A(0) \neq 0$ , sempre existe uma série de potências formais infinita  $A^{-1}(x) = q_0+q_1 x + q_2 x^2 + \dots$  tal que  $A^{-1} A = 1$ . Frequentemente, é útil calcular primeiro  $k$  coeficientes de  $A^{-1}$  (ou seja, calculá-lo módulo  $x^k$ ). Existem duas principais maneiras de calculá-lo.

#### Dividir e conquistar

Este algoritmo foi mencionado no artigo de Schönhage e é inspirado no método de Graeffe. Sabe-se que para  $B(x)=A(x)A(-x)$  vale que  $B(x)=B(-x)$ , ou seja,  $B(x)$  é um polinômio par. Isso significa que ele só possui coeficientes não nulos com números pares e pode ser representado como  
$B(x)=T(x^2)$ . Assim, podemos fazer a seguinte transição:
 
$$A^{-1}(x) \equiv \frac{1}{A(x)} \equiv \frac{A(-x)}{A(x)A(-x)} \equiv \frac{A(-x)}{T(x^2)} \pmod{x^k}$$ 
Observe que  
$T(x)$  pode ser calculado com uma única multiplicação, após o que estamos interessados apenas na primeira metade dos coeficientes de sua série inversa. Isso efetivamente reduz o problema inicial de calcular  
$A^{-1} \pmod{x^k}$  para calcular  
$T^{-1} \pmod{x^{\lfloor k / 2 \rfloor}}$ .

A complexidade desse método pode ser estimada como

 
$$T(n) = T(n/2) + O(n \log n) = O(n \log n).$$ 
#### Algoritmo Sieveking–Kung
O processo genérico descrito aqui é conhecido como elevação de Hensel, conforme decorre do lema de Hensel. Abordaremos isso com mais detalhes mais adiante, mas por enquanto, vamos nos concentrar na solução ad hoc. A parte de "elevação" aqui significa que começamos com a aproximação  $B_0=q_0=a_0^{-1}$ , que é  $A^{-1} \pmod x$ , e então elevamos iterativamente de  $\bmod x^a$  para  $\bmod x^{2a}$ .

Seja  $B_k \equiv A^{-1} \pmod{x^a}$ . A próxima aproximação precisa seguir a equação  $A B_{k+1} \equiv 1 \pmod{x^{2a}}$  e pode ser representada como  $B_{k+1} = B_k + x^a C$ . Daí segue a equação

$$A(B_k + x^{a}C) \equiv 1 \pmod{x^{2a}}.$$ 
Seja  $A B_k \equiv 1 + x^a D \pmod{x^{2a}}$ , então a equação acima implica

$$x^a(D+AC) \equiv 0 \pmod{x^{2a}} \implies D \equiv -AC \pmod{x^a} \implies C \equiv -B_k D \pmod{x^a}.$$ 
Dessa forma, pode-se obter a fórmula final, que é
 
$$x^a C \equiv -B_k x^a D \equiv B_k(1-AB_k) \pmod{x^{2a}} \implies \boxed{B_{k+1} \equiv B_k(2-AB_k) \pmod{x^{2a}}}$$ 
Assim, começando com  $B_0 \equiv a_0^{-1} \pmod x$ , computaremos a sequência  $B_k$  tal que  $AB_k \equiv 1 \pmod{x^{2^k}}$  com complexidade
 
$$T(n) = T(n/2) + O(n \log n) = O(n \log n).$$ 
O algoritmo aqui pode parecer um pouco mais complicado do que o primeiro, mas possui um raciocínio muito sólido e prático por trás dele, bem como um grande potencial de generalização se observado de uma perspectiva diferente, como será explicado mais adiante.

### Divisão euclidiana
Considere dois polinômios $A(x)$  e  $B(x)$  de graus  $n$  e  $m$ . Como mencionado anteriormente, você pode reescrever  $A(x)$  como
 
$$A(x) = B(x) D(x) + R(x), \deg R < \deg B.$$ 
Suponha que  $n \geq m$ , o que implicaria que  $\deg D = n - m$  e os  $n-m+1$  coeficientes principais de  
$A$  não influenciam  $R$ . Isso significa que você pode recuperar  $D(x)$  dos maiores  $n-m+1$  coeficientes de  $A(x)$  e  $B(x)$  se você o considerar como um sistema de equações.

O sistema de equações lineares do qual estamos falando pode ser escrito na seguinte forma:
 
 
$$\begin{bmatrix} a_n \\ \vdots \\ a_{m+1} \\ a_{m} \end{bmatrix} = \begin{bmatrix} b_m & \dots & 0 & 0 \\ \vdots & \ddots & \vdots & \vdots \\ \dots & \dots & b_m & 0 \\ \dots & \dots & b_{m-1} & b_m \end{bmatrix} \begin{bmatrix}d_{n-m} \\ \vdots \\ d_1 \\ d_0\end{bmatrix}$$ 
Pela aparência, podemos concluir que, com a introdução de polinômios reversos

$$A^R(x) = x^nA(x^{-1})= a_n + a_{n-1} x + \dots + a_0 x^n$$
 
$$B^R(x) = x^m B(x^{-1}) = b_m + b_{m-1} x + \dots + b_0 x^m$$ 
$$D^R(x) = x^{n-m}D(x^{-1}) = d_{n-m} + d_{n-m-1} x + \dots + d_0 x^{n-m}$$ 
o sistema pode ser reescrito como

$$A^R(x) \equiv B^R(x) D^R(x) \pmod{x^{n-m+1}}.$$ 
Com isso, você pode recuperar unicamente todos os coeficientes de  $D(x)$ :
 
$$\boxed{D^R(x) \equiv A^R(x) (B^R(x))^{-1} \pmod{x^{n-m+1}}}$$ 
E a partir disso, por sua vez, você pode recuperar  $R(x)$  como  $R(x) = A(x) - B(x)D(x)$ .

Observe que a matriz acima é uma matriz de Toeplitz triangular, e, como vemos aqui, resolver um sistema de equações lineares com uma matriz de Toeplitz arbitrária é, na verdade, equivalente à inversão de polinômios. Além disso, a matriz inversa dela também seria uma matriz de Toeplitz triangular e seus elementos, nos termos usados acima, são os coeficientes de  
$(B^R(x))^{-1} \pmod{x^{n-m+1}}$ .



## Calculating functions of polynomial

### Método de Newton
Vamos generalizar o algoritmo Sieveking–Kung. Considere a equação  $F(P) = 0$  onde  $P(x)$  deve ser um polinômio e  $F(x)$  é alguma função polinomial definida como

$$F(x) = \sum\limits_{i=0}^\infty \alpha_i (x-\beta)^i,$$ 
onde  $\beta$  é alguma constante. Pode-se provar que, se introduzirmos uma nova variável formal  $y$ , podemos expressar  $F(x)$  como

 
$$F(x) = F(y) + (x-y)F'(y) + (x-y)^2 G(x,y),$$
onde  $F'(x)$  é a série de potências formais da derivada definida como

$$F'(x) = \sum\limits_{i=0}^\infty (i+1)\alpha_{i+1}(x-\beta)^i,$$ 
e $G(x, y)$  é alguma série de potências formais de  $x$  e  $y$ . Com esse resultado, podemos encontrar a solução de maneira iterativa.

Seja  $F(Q_k) \equiv 0 \pmod{x^{a}}$ . Precisamos encontrar  $Q_{k+1} \equiv Q_k + x^a C \pmod{x^{2a}}$  tal que  $F(Q_{k+1}) \equiv 0 \pmod{x^{2a}}$ .

Substituindo  $x = Q_{k+1}$  e  $y=Q_k$  na fórmula acima, obtemos

$$F(Q_{k+1}) \equiv F(Q_k) + (Q_{k+1} - Q_k) F'(Q_k) + (Q_{k+1} - Q_k)^2 G(x, y) \pmod x^{2a}.$$ 
Como  $Q_{k+1} - Q_k \equiv 0 \pmod{x^a}$ , também vale que  $(Q_{k+1} - Q_k)^2 \equiv 0 \pmod{x^{2a}}$ , assim

$$0 \equiv F(Q_{k+1}) \equiv F(Q_k) + (Q_{k+1} - Q_k) F'(Q_k) \pmod{x^{2a}}.$$ 
A última fórmula nos dá o valor de  $Q_{k+1}$ :
$$\boxed{Q_{k+1} = Q_k - \dfrac{F(Q_k)}{F'(Q_k)} \pmod{x^{2a}}}$$ 
Assim, sabendo como inverter polinômios e como calcular  $F(Q_k)$ , podemos encontrar  $n$  coeficientes de  $P$  com complexidade

$$T(n) = T(n/2) + f(n),$$ 
onde  $f(n)$  é o tempo necessário para calcular  $F(Q_k)$  e  $F'(Q_k)^{-1}$ , que geralmente é  $O(n \log n)$ .

A regra iterativa acima é conhecida na análise numérica como Método de Newton.

#### Hensel's lemma

Como mencionado anteriormente, formalmente e genericamente, esse resultado é conhecido como o lema de Hensel e pode ser utilizado de fato de maneira mais ampla quando trabalhamos com uma série de anéis aninhados. Neste caso específico, trabalhamos com uma sequência de restos de polinômios módulo  $x$ ,  $x^2$ ,  $x^3$  e assim por diante.

Outro exemplo em que a elevação de Hensel pode ser útil são os chamados números p-ádicos, nos quais, de fato, trabalhamos com a sequência de restos inteiros módulo  $p$ ,  $p^2$ ,  $p^3$  e assim por diante. Por exemplo, o método de Newton pode ser usado para encontrar todos os números automórficos possíveis (números que terminam neles mesmos quando elevados ao quadrado) com uma determinada base numérica. O problema fica como um exercício para o leitor. Você pode considerar esse problema para verificar se sua solução funciona para números na base  $10$ .

### Logaritmo
Para a função  $\ln P(x)$ , é conhecido que:

$$ \boxed{(\ln P(x))' = \dfrac{P'(x)}{P(x)}} $$ 
Assim, podemos calcular  $n$  coeficientes de  $\ln P(x)$  em  $O(n \log n)$ .


### Série inversa
Acontece que podemos obter a fórmula para  $A^{-1}$  usando o método de Newton. Para isso, tomamos a equação  $A=Q^{-1}$ , assim:
 
$$F(Q) = Q^{-1} - A$$ 
$$F'(Q) = -Q^{-2}$$
$$\boxed{Q_{k+1} \equiv Q_k(2-AQ_k) \pmod{x^{2^{k+1}}}}$$

### Expoente
Vamos aprender a calcular  $e^{P(x)}=Q(x)$ . Deve valer que  $\ln Q = P$ , assim:
 
$$F(Q) = \ln Q - P$$
 
$$F'(Q) = Q^{-1}$$ 
$$\boxed{Q_{k+1} \equiv Q_k(1 + P - \ln Q_k) \pmod{x^{2^{k+1}}}}$$ 


### $k$ -ésima Potência  

Agora precisamos calcular  $P^k(x)=Q$ . Isso pode ser feito através da seguinte fórmula:
 
$$Q = \exp\left[k \ln P(x)\right]$$ 
Observe, no entanto, que você só pode calcular os logaritmos e exponenciais corretamente se puder encontrar algum  $Q_0$  inicial.

Para encontrá-lo, você deve calcular o logaritmo ou a exponencial do coeficiente constante do polinômio.

Mas a única maneira razoável de fazer isso é se  $P(0)=1$  para  $Q = \ln P$ , então  $Q(0)=0$  e se  $P(0)=0$  para  $Q = e^P$ , então  $Q(0)=1$ .

Assim, você pode usar a fórmula acima apenas se  $P(0) = 1$ . Caso contrário, se  $P(x) = \alpha x^t T(x)$  onde  $T(0)=1$ , você pode escrever que:
 
$$\boxed{P^k(x) = \alpha^kx^{kt} \exp[k \ln T(x)]}$$ 
Observe que você também pode calcular alguma raiz  $k$ -ésima de um polinômio se puder calcular  $\sqrt[k]{\alpha}$ , por exemplo, para  $\alpha=1$ .
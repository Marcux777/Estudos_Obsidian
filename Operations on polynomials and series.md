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


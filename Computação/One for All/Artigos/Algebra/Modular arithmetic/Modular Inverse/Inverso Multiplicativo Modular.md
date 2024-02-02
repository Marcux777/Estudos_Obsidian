Um inverso multiplicativo modular de um inteiro  $a$  é um inteiro  $x$  tal que  $a \cdot x$  é congruente a  $1$  modular algum módulo  $m$ . Para escrever de uma maneira formal: queremos encontrar um inteiro  
$x$  de modo que
$$a \cdot x \equiv 1 \mod m.$$ 
Também denotaremos  $x$  simplesmente com  $a^{-1}$ .

Devemos notar que o inverso modular nem sempre existe. Por exemplo, deixe  $m = 4$ ,  $a = 2$ . Ao verificar todos os possíveis valores modulo  $m$ , deve ficar claro que não podemos encontrar  $a^{-1}$  satisfazendo a equação acima. Pode ser provado que o inverso modular existe se e somente se  
$a$  e  $m$  são primos entre si (ou seja,  $\gcd(a, m) = 1$ ).
Neste artigo, apresentamos dois métodos para encontrar o inverso modular caso ele exista, e um método para encontrar o inverso modular para todos os números em tempo linear.

## Encontrando o Inverso Modular usando o Algoritmo Euclidiano Estendido

Considere a seguinte equação (com  $x$  e  $y$  desconhecidos):
$$a \cdot x + m \cdot y = 1$$ 
Esta é uma equação diofantina linear em duas variáveis. Como mostrado no artigo vinculado, quando  $\gcd(a, m) = 1$ , a equação tem uma solução que pode ser encontrada usando o algoritmo euclidiano estendido. Note que  $\gcd(a, m) = 1$  também é a condição para o inverso modular existir.

Agora, se tomarmos o módulo  $m$  de ambos os lados, podemos nos livrar de  $m \cdot y$ , e a equação se torna:
$$a \cdot x \equiv 1 \mod m$$ 
Assim, o inverso modular de  $a$  é  $x$ .

A implementação é a seguinte:

```c++
int x, y;
int g = extended_euclidean(a, m, x, y);
if (g != 1) {
    cout << "No solution!";
}
else {
    x = (x % m + m) % m;
    cout << x << endl;
}
```
Observe a maneira como modificamos x. O x resultante do algoritmo euclidiano estendido pode ser negativo, então x % m também pode ser negativo, e primeiro temos que adicionar m para torná-lo positivo.
## Encontrando o Inverso Modular usando Exponenciação Binária
Outro método para encontrar o inverso modular é usar o teorema de Euler, que afirma que a seguinte congruência é verdadeira se  $a$  e  $m$  são primos entre si:

 
$$a^{\phi (m)} \equiv 1 \mod m$$ 
 
$\phi$  é a [[Função totiente de Euler]]. Novamente, note que  $a$  e  $m$  serem primos entre si também era a condição para a existência do inverso modular.

Se  $m$  é um número primo, isso simplifica para o [[pequeno teorema de Fermat]]:

$$a^{m - 1} \equiv 1 \mod m$$ 
Multiplique ambos os lados das equações acima por  
$a^{-1}$ , e obtemos:

- Para um módulo arbitrário (mas coprimo)  $m$ :  $a ^ {\phi (m) - 1} \equiv a ^{-1} \mod m$ 
- Para um módulo primo  $m$ :  $a ^ {m - 2} \equiv a ^ {-1} \mod m$ 

A partir desses resultados, podemos facilmente encontrar o inverso modular usando o [algoritmo de exponenciação binária](obsidian://open?vault=Algoritmos&file=algoritmos%2FArtigos%2FAlgebra%2FBinary%20Exponentiation%2FAlgoritmo%20-%20Binary%20Exponentiation), que funciona em  $O(\log m)$  tempo.

Embora este método seja mais fácil de entender do que o método descrito no parágrafo anterior, no caso em que  $m$  não é um número primo, precisamos calcular a função phi de Euler, que envolve a fatoração de  $m$ , o que pode ser muito difícil. Se a fatoração prima de  $m$  é conhecida, então a complexidade deste método é  $O(\log m)$ .
## Encontrando o inverso modular para módulos primos usando a Divisão Euclidiana
Dado um módulo primo  $m > a$  (ou podemos aplicar o módulo para torná-lo menor em 1 passo), de acordo com a [Divisão Euclidiana](https://en.wikipedia.org/wiki/Euclidean_division)
$$m = k \cdot a + r$$ 
onde $k = \left\lfloor \frac{m}{a} \right\rfloor$  e  $r = m \bmod a$ , então
$$ \begin{align*} & \implies & 0 & \equiv k \cdot a + r & \mod m \\ & \iff & r & \equiv -k \cdot a & \mod m \\ & \iff & r \cdot a^{-1} & \equiv -k & \mod m \\ & \iff & a^{-1} & \equiv -k \cdot r^{-1} & \mod m \end{align*} $$ 
Note que este raciocínio não se mantém se  $m$  não for primo, pois a existência de  $a^{-1}$  não implica a existência de  $r^{-1}$  no caso geral. Para ver isso, vamos tentar calcular  $5^{-1}$  módulo  $12$  com a fórmula acima. Gostaríamos de chegar a  $5$ , já que  $5 \cdot 5 \equiv 1 \bmod 12$ . No entanto,  $12 = 2 \cdot 5 + 2$ , e temos  $k=2$  e  $r=2$ , com  $2$  não sendo invertível módulo  $12$ .

No entanto, se o módulo for primo, todos  $a$  com  $0 < a < m$  são invertíveis módulo  $m$ , e podemos ter a seguinte função recursiva (em C++) para calcular o inverso modular para o número  $a$  em relação a  $m$ 

```c++
int inv(int a) {
  return a <= 1 ? a : m - (long long)(m/a) * inv(m % a) % m;
}
```
A complexidade exata do tempo desta recursão não é conhecida. Está em algum lugar entre $O(\frac{\log m}{\log\log m})$  e   $O(m^{\frac{1}{3} - \frac{2}{177} + \epsilon})$ . Veja Sobre o [comprimento das expansões de Pierce](https://arxiv.org/abs/2211.08374). Na prática, esta implementação é rápida, por exemplo, para o módulo  $10^9 + 7$  sempre terminará em menos de 50 iterações.

Aplicando esta fórmula, também podemos pré-calcular o inverso modular para cada número no intervalo  $[1, m-1]$  em  $O(m)$ .

```c++
inv[1] = 1;
for(int a = 2; a < m; ++a)
    inv[a] = m - (long long)(m/a) * inv[m%a] % m;
```

## Encontrando o inverso modular para um array de números módulo  $m$
Suponha que nos é dado um array e queremos encontrar o inverso modular para todos os números nele (todos eles são invertíveis). Em vez de calcular o inverso para cada número, podemos expandir a fração pelo produto do prefixo (excluindo-se) e produto do sufixo (excluindo-se), e acabamos calculando apenas um único inverso.
$$ \begin{align} x_i^{-1} &= \frac{1}{x_i} = \frac{\overbrace{x_1 \cdot x_2 \cdots x_{i-1}}^{\text{prefixo}_{i-1}} \cdot ~1~ \cdot \overbrace{x_{i+1} \cdot x_{i+2} \cdots x_n}^{\text{sufixo}_{i+1}}}{x_1 \cdot x_2 \cdots x_{i-1} \cdot x_i \cdot x_{i+1} \cdot x_{i+2} \cdots x_n} \\ &= \text{prefixo}_{i-1} \cdot \text{sufixo}_{i+1} \cdot \left(x_1 \cdot x_2 \cdots x_n\right)^{-1} \end{align} $$ 
No código, podemos apenas fazer um array de produto de prefixo (excluindo-se, começando pelo elemento identidade), calcular o inverso modular para o produto de todos os números e então multiplicá-lo pelo produto de prefixo e produto de sufixo (excluindo-se). O produto de sufixo é calculado iterando de trás para frente.

```c++
std::vector<int> invs(const std::vector<int> &a, int m) {
    int n = a.size();
    if (n == 0) return {};
    std::vector<int> b(n);
    int v = 1;
    for (int i = 0; i != n; ++i) {
        b[i] = v;
        v = static_cast<long long>(v) * a[i] % m;
    }
    int x, y;
    extended_euclidean(v, m, x, y);
    x = (x % m + m) % m;
    for (int i = n - 1; i >= 0; --i) {
        b[i] = static_cast<long long>(x) * b[i] % m;
        x = static_cast<long long>(x) * a[i] % m;
    }
    return b;
}
```
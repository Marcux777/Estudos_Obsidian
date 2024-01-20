## Algoritmo

Originalmente, o algoritmo de Euclides foi formulado da seguinte maneira: subtraia o número menor do maior até que um dos números seja zero. De fato, se $g$ divide $a$ e $b$, ele também divide $a-b$. Por outro lado, se $g$ divide $a-b$ e $b$, então ele também divide $a = b + (a-b)$, o que significa que os conjuntos dos divisores comuns de $\{a, b\}$ e $\{b,a-b\}$ coincidem.

Note que $a$ permanece o número maior até que $b$ seja subtraído dele pelo menos $\left\lfloor\frac{a}{b}\right\rfloor$ vezes. Portanto, para acelerar as coisas, $a-b$ é substituído por $a-\left\lfloor\frac{a}{b}\right\rfloor b = a \bmod b$. Então, o algoritmo é formulado de uma maneira extremamente simples:

$$\gcd(a, b) = \begin{cases}a,&\text{se }b = 0 \\ \gcd(b, a \bmod b),&\text{caso contrário.}\end{cases}$$
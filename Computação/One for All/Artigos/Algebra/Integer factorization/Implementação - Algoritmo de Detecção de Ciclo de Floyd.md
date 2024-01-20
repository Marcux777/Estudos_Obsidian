Primeiro, aqui está uma implementação usando o algoritmo de detecção de ciclo de Floyd. O algoritmo é executado (geralmente) em  
$O(\sqrt[4]{n} \log(n))$  tempo.

```cpp
long long mult(long long a, long long b, long long mod) {
    return (__int128)a * b % mod;
}

long long f(long long x, long long c, long long mod) {
    return (mult(x, x, mod) + c) % mod;
}

long long rho(long long n, long long x0=2, long long c=1) {
    long long x = x0;
    long long y = x0;
    long long g = 1;
    while (g == 1) {
        x = f(x, c, n);
        y = f(y, c, n);
        y = f(y, c, n);
        g = gcd(abs(x - y), n);
    }
    return g;
}
```
A tabela a seguir mostra os valores de  $x$  e  $y$  durante o algoritmo para  
$n = 2206637$ ,  $x_0 = 2$  e  $c = 1$ .
 
$$ \newcommand\T{\Rule{0pt}{1em}{.3em}} \begin{array}{|l|l|l|l|l|l|} \hline i & x_i \bmod n & x_{2i} \bmod n & x_i \bmod 317 & x_{2i} \bmod 317 & \gcd(x_i - x_{2i}, n) \\ \hline 0 & 2 & 2 & 2 & 2 & - \\ 1 & 5 & 26 & 5 & 26 & 1 \\ 2 & 26 & 458330 & 26 & 265 & 1 \\ 3 & 677 & 1671573 & 43 & 32 & 1 \\ 4 & 458330 & 641379 & 265 & 88 & 1 \\ 5 & 1166412 & 351937 & 169 & 67 & 1 \\ 6 & 1671573 & 1264682 & 32 & 169 & 1 \\ 7 & 2193080 & 2088470 & 74 & 74 & 317 \\ \hline \end{array}$$ 
A implementação usa uma função mult, que multiplica dois inteiros  $\le 10^{18}$  sem estouro usando um tipo __int128 do GCC para inteiros de 128 bits. Se o GCC não estiver disponível, você pode usar uma ideia semelhante à [[Binary Exponentiation]].

```cpp
long long mult(long long a, long long b, long long mod) {
    long long result = 0;
    while (b) {
        if (b & 1)
            result = (result + a) % mod;
        a = (a + a) % mod;
        b >>= 1;
    }
    return result;
}
```
Alternativamente, você também pode implementar a [[multiplicação de Montgomery]].

Como já observado acima: se  $n$  é composto e o algoritmo retorna  $n$  como fator, você deve repetir o procedimento com parâmetro diferente  $x_0$  e  $c$ . Por exemplo, a escolha  $x_0 = c = 1$  não fatorará  $25 = 5 \cdot 5$ . O algoritmo apenas retornará  $25$ . No entanto, a escolha  $x_0 = 1$ ,  $c = 2$  irá fatorá-lo.
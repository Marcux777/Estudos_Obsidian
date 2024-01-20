A implementação direta usando os algoritmos de Brent pode ser acelerada ao perceber que podemos omitir os termos  $x_l - x_k$  se  $k < \frac{3 \cdot l}{2}$ . Além disso, em vez de realizar o cálculo do  $\gcd$  a cada passo, multiplicamos os termos e fazemos isso a cada poucos passos e voltamos atrás se ultrapassarmos.

```cpp
long long brent(long long n, long long x0=2, long long c=1) {
    long long x = x0;
    long long g = 1;
    long long q = 1;
    long long xs, y;

    int m = 128;
    int l = 1;
    while (g == 1) {
        y = x;
        for (int i = 1; i < l; i++)
            x = f(x, c, n);
        int k = 0;
        while (k < l && g == 1) {
            xs = x;
            for (int i = 0; i < m && i < l - k; i++) {
                x = f(x, c, n);
                q = mult(q, abs(y - x), n);
            }
            g = gcd(q, n);
            k += m;
        }
        l *= 2;
    }
    if (g == n) {
        do {
            xs = f(xs, c, n);
            g = gcd(abs(xs - y), n);
        } while (g == 1);
    }
    return g;
}
```
A combinação de uma divisão de teste para números primos pequenos juntamente com a versão de Brent do algoritmo rho de Pollard fará um algoritmo de fatoração muito poderoso.

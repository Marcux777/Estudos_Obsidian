Seja  $g = \gcd(a, m)$ , e  $g > 1$ . Claramente  $a^x \bmod m$  para todo  $x \ge 1$  será divisível por  $g$ .

Se  $g \nmid b$ , não há solução para  $x$ .

Se  $g \mid b$ , seja  $a = g \alpha, b = g \beta, m = g \nu$ .
$$ \begin{aligned} a^x & \equiv b \mod m \\\ (g \alpha) a^{x - 1} & \equiv g \beta \mod g \nu \\\ \alpha a^{x-1} & \equiv \beta \mod \nu \end{aligned} $$ 
O algoritmo baby-step giant-step pode ser facilmente estendido para resolver  $ka^{x} \equiv b \pmod m$  para  $x$ .

```cpp
// Returns minimum x for which a ^ x % m = b % m.
int solve(int a, int b, int m) {
    a %= m, b %= m;
    int k = 1, add = 0, g;
    while ((g = gcd(a, m)) > 1) {
        if (b == k)
            return add;
        if (b % g)
            return -1;
        b /= g, m /= g, ++add;
        k = (k * 1ll * a / g) % m;
    }

    int n = sqrt(m) + 1;
    int an = 1;
    for (int i = 0; i < n; ++i)
        an = (an * 1ll * a) % m;

    unordered_map<int, int> vals;
    for (int q = 0, cur = b; q <= n; ++q) {
        vals[cur] = q;
        cur = (cur * 1ll * a) % m;
    }

    for (int p = 1, cur = k; p <= n; ++p) {
        cur = (cur * 1ll * an) % m;
        if (vals.count(cur)) {
            int ans = n * p - vals[cur] + add;
            return ans;
        }
    }
    return -1;
}
```

A complexidade de tempo continua sendo  $O(\sqrt{m})$  como antes, uma vez que a redução inicial para  $a$  e  $m$  primos entre si é feita em  $O(\log^2 m)$ .
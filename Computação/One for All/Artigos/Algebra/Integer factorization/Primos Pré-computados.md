
Estender a fatoração por roda com mais e mais primos deixará exatamente os primos para verificar. Portanto, uma boa maneira de verificar é apenas pré-computar todos os números primos com o [[Crivo de Eratóstenes]] até  $\sqrt{n}$  e testá-los individualmente.

```cpp
vector<long long> primes;

vector<long long> trial_division4(long long n) {
    vector<long long> factorization;
    for (long long d : primes) {
        if (d * d > n)
            break;
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```


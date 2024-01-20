
Às vezes, precisamos encontrar todos os números primos em um intervalo  
$[L,R]$  de pequeno tamanho (por exemplo,  
$R - L + 1 \approx 1e7$ ), onde  
$R$  pode ser muito grande (por exemplo,  
$1e12$ ).

Para resolver esse problema, podemos usar a ideia do Crivo Segmentado. Pré-geramos todos os números primos até  
$\sqrt R$ , e usamos esses primos para marcar todos os números compostos no segmento  
$[L, R]$ .

```cpp
vector<char> segmentedSieve(long long L, long long R) {
    // gerar todos os primos até sqrt(R)
    long long lim = sqrt(R);
    vector<char> mark(lim + 1, false);
    vector<long long> primes;
    for (long long i = 2; i <= lim; ++i) {
        if (!mark[i]) {
            primes.emplace_back(i);
            for (long long j = i * i; j <= lim; j += i)
                mark[j] = true;
        }
    }

    vector<char> isPrime(R - L + 1, true);
    for (long long i : primes)
        for (long long j = max(i * i, (L + i - 1) / i * i); j <= R; j += i)
            isPrime[j - L] = false;
    if (L == 1)
        isPrime[0] = false;
    return isPrime;
}
```
A complexidade de tempo dessa abordagem é  
$O((R - L + 1) \log \log (R) + \sqrt R \log \log \sqrt R)$ .

Também é possível que não pré-geremos todos os números primos:

```cpp
vector<char> segmentedSieveNoPreGen(long long L, long long R) {
    vector<char> isPrime(R - L + 1, true);
    long long lim = sqrt(R);
    for (long long i = 2; i <= lim; ++i)
        for (long long j = max(i * i, (L + i - 1) / i * i); j <= R; j += i)
            isPrime[j - L] = false;
    if (L == 1)
        isPrime[0] = false;
    return isPrime;
}
```
Obviamente, a complexidade é pior, que é  
$O((R - L + 1) \log (R) + \sqrt R)$ . No entanto, ainda é muito rápido na prática.

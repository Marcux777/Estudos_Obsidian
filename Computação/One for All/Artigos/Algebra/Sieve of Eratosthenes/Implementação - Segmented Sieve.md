
``` c++
int count_primes(int n) {
    const int S = 10000;

    vector<int> primes;
    int nsqrt = sqrt(n);
    vector<char> is_prime(nsqrt + 2, true);
    for (int i = 2; i <= nsqrt; i++) {
        if (is_prime[i]) {
            primes.push_back(i);
            for (int j = i * i; j <= nsqrt; j += i)
                is_prime[j] = false;
        }
    }

    int result = 0;
    vector<char> block(S);
    for (int k = 0; k * S <= n; k++) {
        fill(block.begin(), block.end(), true);
        int start = k * S;
        for (int p : primes) {
            int start_idx = (start + p - 1) / p;
            int j = max(start_idx, p) * p - start;
            for (; j < S; j += p)
                block[j] = false;
        }
        if (k == 0)
            block[0] = block[1] = false;
        for (int i = 0; i < S && start + i <= n; i++) {
            if (block[i])
                result++;
        }
    }
    return result;
}
```

O tempo de execução da peneiração em blocos é o mesmo que para o crivo regular de Eratóstenes (a menos que o tamanho dos blocos seja muito pequeno), mas a memória necessária será reduzida para $O(\sqrt{n} + S)$ e teremos melhores resultados de cache. Por outro lado, haverá uma divisão para cada par de um bloco e número primo de $[1; \sqrt{n}]$, e isso será muito pior para tamanhos de bloco menores. Portanto, é necessário manter o equilíbrio ao selecionar a constante $S$ . Obtivemos os melhores resultados para tamanhos de bloco entre $10^{4}$ e $10^5$ .
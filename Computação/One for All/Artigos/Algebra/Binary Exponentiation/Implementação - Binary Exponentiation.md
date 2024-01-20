
Primeiro, a abordagem recursiva, que é uma tradução direta da fórmula recursiva:

```c++
long long binpow(long long a, long long b) {
    if (b == 0)
        return 1;
    long long res = binpow(a, b / 2);
    if (b % 2)
        return res * res * a;
    else
        return res * res;
}
```

A segunda abordagem realiza a mesma tarefa sem recursão. Ela calcula todas as potências em um loop e multiplica as que têm o bit correspondente definido em $n$. Embora a complexidade de ambas as abordagens seja idêntica, esta abordagem será mais rápida na prática, pois não temos o overhead das chamadas recursivas.

```c++
long long binpow(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a;
        a = a * a;
        b >>= 1;
    }
    return res;
}
'''

Não precisamos de recursão porque este é um caso de recursão de cauda e, portanto, pode ser facilmente implementado usando iteração. Na seguinte implementação, pré-calculamos os fatoriais  $0!,~ 1!,~ \dots,~ (p-1)!$  e, assim, temos um tempo de execução de  $O(p + \log_p n)$ . Se você precisar chamar a função várias vezes, pode fazer o pré-cálculo fora da função e calcular  $n!_{\%p}$  em  $O(\log_p n)$  tempo.

```cpp
int factmod(int n, int p) {
    vector<int> f(p);
    f[0] = 1;
    for (int i = 1; i < p; i++)
        f[i] = f[i-1] * i % p;

    int res = 1;
    while (n > 1) {
        if ((n/p) % 2)
            res = p - res;
        res = res * f[n%p] % p;
        n /= p;
    }
    return res;
}
```

Alternativamente, se você tiver limitação de memória e não puder armazenar todos os fatoriais, também pode apenas lembrar os fatoriais necessários, ordená-los e depois calculá-los de uma vez, computando os fatoriais  $0!,~ 1!,~ 2!,~ \dots,~ (p-1)!$  em um loop sem armazená-los explicitamente.
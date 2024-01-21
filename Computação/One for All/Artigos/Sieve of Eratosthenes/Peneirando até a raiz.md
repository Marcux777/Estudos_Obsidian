Obviamente, para encontrar todos os números primos até $n$, será suficiente apenas realizar a peneiração apenas pelos números primos, que não excedem a raiz de $n$.

```cpp
int n;
vector<bool> is_prime(n+1, true);
is_prime[0] = is_prime[1] = false;
for (int i = 2; i * i <= n; i++) {
    if (is_prime[i]) {
        for (int j = i * i; j <= n; j += i)
            is_prime[j] = false;
    }
}
```
Essa otimização não afeta a complexidade (de fato, repetindo a prova apresentada acima, obteremos a avaliação $n \ln \ln \sqrt n + o(n)$, que é assintoticamente a mesma de acordo com as propriedades dos logaritmos), embora o número de operações seja reduzido notavelmente.

A maior fraqueza do algoritmo é que ele “caminha” pela memória várias vezes, manipulando apenas elementos individuais. Isso não é muito amigável para o cache. E por causa disso, a constante que está oculta em $O(nloglogn)$ é comparativamente grande.
Além disso, a memória consumida é um gargalo para grandes n.
Os métodos apresentados abaixo nos permitem reduzir a quantidade de operações realizadas, bem como reduzir notavelmente a memória consumida.

## Peneirando até a raiz
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
## Peneirando apenas pelos números ímpares

Como todos os números pares (exceto 2) são compostos, podemos parar de verificar os números pares completamente. Em vez disso, precisamos operar apenas com números ímpares.
Primeiro, isso nos permitirá reduzir pela metade a memória necessária. Em segundo lugar, reduzirá aproximadamente pela metade o número de operações realizadas pelo algoritmo.

[[Consumo de Memória e Velocidade das Operações]]
[[Segmented Sieve]]

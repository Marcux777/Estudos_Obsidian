Se precisarmos de todos os totientes de todos os números entre  $1$  e  $n$ , então fatorar todos os números  
$n$  não é eficiente. Podemos usar a mesma ideia do [[Crivo de Eratóstenes]]. Ainda se baseia na propriedade mostrada acima, mas em vez de atualizar o resultado temporário para cada fator primo para cada número, encontramos todos os números primos e para cada um atualizamos os resultados temporários de todos os números que são divisíveis por esse número primo.

Como essa abordagem é basicamente idêntica ao Crivo de Eratóstenes, a complexidade também será a mesma:  $O(n \log \log n)$ 

```c++
void phi_1_to_n(int n) {
    vector<int> phi(n + 1);
    for (int i = 0; i <= n; i++)
        phi[i] = i;

    for (int i = 2; i <= n; i++) {
        if (phi[i] == i) {
            for (int j = i; j <= n; j += i)
                phi[j] -= phi[j] / i;
        }
    }
}
```


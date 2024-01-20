
```cpp
int n;
vector<bool> is_prime(n+1, true);
is_prime[0] = is_prime[1] = false;
for (int i = 2; i <= n; i++) {
    if (is_prime[i] && (long long)i * i <= n) {
        for (int j = i * i; j <= n; j += i)
            is_prime[j] = false;
    }
}
```
Este código primeiro marca todos os números exceto zero e um como potenciais números primos, então começa o processo de peneirar números compostos. Para isso, itera sobre todos os números de $2$ a $n$. Se o número atual $i$ é um número primo, marca todos os números que são múltiplos de $i$ como números compostos, começando de $i^2$. Isso já é uma otimização sobre a maneira ingênua de implementá-lo, e é permitido já que todos os números menores que são múltiplos de $i$ necessariamente também têm um fator primo que é menor que $i$, então todos eles já foram peneirados anteriormente. Como $i^2$ pode facilmente estourar o tipo int, a verificação adicional é feita usando o tipo long long antes do segundo loop aninhado.

Usando essa implementação, o algoritmo consome $O(n)$ de memória (obviamente) e executa $O(n \log \log n)$ (veja a próxima seção).
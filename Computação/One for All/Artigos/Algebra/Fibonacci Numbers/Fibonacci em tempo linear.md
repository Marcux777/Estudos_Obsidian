
O $n^{\text{ésimo}}$ número de Fibonacci pode ser facilmente encontrado em $O(n)$ calculando os números um a um até $n$. No entanto, também existem maneiras mais rápidas, como veremos.

Podemos começar com uma abordagem iterativa, para aproveitar o uso da fórmula $F_n = F_{n-1} + F_{n-2}$, portanto, simplesmente pré-calcularemos esses valores em um array. Levando em conta os casos base para $F_0$ e $F_1$.

```cpp
int fib(int n) {
    int a = 0;
    int b = 1;
    for (int i = 0; i < n; i++) {
        int tmp = a + b;
        a = b;
        b = tmp;
    }
    return a;
}
```
Dessa forma, obtemos uma solução linear, tempo $O(n)$, salvando todos os valores anteriores a $n$ na sequência.
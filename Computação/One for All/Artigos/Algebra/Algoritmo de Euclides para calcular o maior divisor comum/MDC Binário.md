
O algoritmo de MDC binário é uma otimização do algoritmo de Euclides normal.

A parte lenta do algoritmo normal são as operações de módulo. As operações de módulo, embora as vejamos como $O(1)$, são muito mais lentas do que operações mais simples como adição, subtração ou operações bitwise. Portanto, seria melhor evitá-las.

Acontece que você pode projetar um algoritmo de MDC rápido que evita operações de módulo. Ele é baseado em algumas propriedades:

Se ambos os números são pares, então podemos fatorar um dois de ambos e calcular o MDC dos números restantes: $\gcd(2a, 2b) = 2 \gcd(a, b)$.
Se um dos números é par e o outro é ímpar, então podemos remover o fator 2 do par: $\gcd(2a, b) = \gcd(a, b)$ se $b$ é ímpar.
Se ambos os números são ímpares, então subtrair um número do outro não mudará o MDC: $\gcd(a, b) = \gcd(b, a-b)$
Usando apenas essas propriedades, e algumas funções bitwise rápidas do GCC, podemos implementar uma versão rápida:

```cpp
int gcd(int a, int b) {
    if (!a || !b)
        return a | b;
    unsigned shift = __builtin_ctz(a | b);
    a >>= __builtin_ctz(a);
    do {
        b >>= __builtin_ctz(b);
        if (a > b)
            swap(a, b);
        b -= a;
    } while (b);
    return a << shift;
}
```
Note que tal otimização geralmente não é necessária, e a maioria das linguagens de programação já tem uma função de MDC em suas bibliotecas padrão. Por exemplo, o C++17 tem uma função std::gcd no cabeçalho numérico.
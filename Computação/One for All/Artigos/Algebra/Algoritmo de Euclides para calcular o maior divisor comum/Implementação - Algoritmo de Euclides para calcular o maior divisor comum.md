
Aqui está a implementação recursiva:

```cpp
int gcd (int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd (b, a % b);
}
```

Usando o operador ternário em C++, podemos escrevê-lo em uma linha:

```cpp
int gcd (int a, int b) {
    return b ? gcd (b, a % b) : a;
}
```

E finalmente, aqui está uma implementação não recursiva:

```cpp
int gcd (int a, int b) {
    while (b) {
        a %= b;
        swap(a, b);
    }
    return a;
}
```

Note que desde o C++17, o gcd é implementado como uma função padrão em C++. Isso significa que você pode usar `std::gcd(a, b)` para calcular o máximo divisor comum de `a` e `b`.

## Complexidade de Tempo

O tempo de execução do algoritmo é estimado pelo teorema de Lamé, que estabelece uma conexão surpreendente entre o algoritmo de Euclides e a sequência de Fibonacci:

Se $a > b \geq 1$ e $b < F_n$ para algum $n$, o algoritmo de Euclides realiza no máximo $n-2$chamadas recursivas.

Além disso, é possível mostrar que o limite superior deste teorema é ótimo. Quando$a = F_neb = F_{n-1},\gcd(a, b)$ realizará exatamente $n-2$ chamadas recursivas. Em outras palavras, números consecutivos de Fibonacci são o pior caso de entrada para o algoritmo de Euclides.

Dado que os números de Fibonacci crescem exponencialmente, obtemos que o algoritmo de Euclides funciona em $O(\log \min(a, b))$.

Outra maneira de estimar a complexidade é notar que $a \bmod b$ para o caso $a \geq b$ é pelo menos $2$ vezes menor que $a$, então o número maior é reduzido pelo menos pela metade em cada iteração do algoritmo.


[[Mínimo múltiplo comum]]
[[MDC Binário]]
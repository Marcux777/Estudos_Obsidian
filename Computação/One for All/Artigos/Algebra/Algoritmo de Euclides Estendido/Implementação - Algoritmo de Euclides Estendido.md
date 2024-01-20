
```cpp
int mdc(int a, int b, int& x, int& y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int x1, y1;
    int d = mdc(b, a % b, x1, y1);
    x = y1;
    y = x1 - y1 * (a / b);
    return d;
}
```
A função recursiva acima retorna o MDC e os valores dos coeficientes para x e y (que são passados por referência para a função).

Esta implementação do algoritmo euclidiano estendido produz resultados corretos para inteiros negativos também.

## Versão Iterativa

Também é possível escrever o Algoritmo Euclidiano Estendido de uma maneira iterativa. Como evita a recursão, o código será executado um pouco mais rápido do que o recursivo.

```cpp
int mdc(int a, int b, int& x, int& y) {
    x = 1, y = 0;
    int x1 = 0, y1 = 1, a1 = a, b1 = b;
    while (b1) {
        int q = a1 / b1;
        tie(x, x1) = make_tuple(x1, x - q * x1);
        tie(y, y1) = make_tuple(y1, y - q * y1);
        tie(a1, b1) = make_tuple(b1, a1 - q * b1);
    }
    return a1;
}
```
Se você olhar de perto as variáveis a1 e b1, pode notar que elas assumem exatamente os mesmos valores que na versão iterativa do algoritmo euclidiano normal. Portanto, o algoritmo pelo menos calculará o MDC correto.

Para ver por que o algoritmo também calcula os coeficientes corretos, você pode verificar que os seguintes invariantes serão mantidos a qualquer momento (antes do loop while e no final de cada iteração): $x \cdot a + y \cdot b = a_1$ e $x_1 \cdot a + y_1 \cdot b = b_1$. É trivial ver que essas duas equações são satisfeitas no início. E você pode verificar que a atualização na iteração do loop ainda manterá essas igualdades válidas.

No final, sabemos que $a_1$ contém o MDC, então $x \cdot a + y \cdot b = g$. O que significa que encontramos os coeficientes necessários.

Você pode até otimizar mais o código e remover a variável $a_1$ e $b_1$ do código e apenas reutilizar $a$ e $b$. No entanto, se você fizer isso, perderá a capacidade de argumentar sobre os invariantes.

O cálculo do mínimo múltiplo comum (comumente denotado por MMC) pode ser reduzido ao cálculo do MDC com a seguinte fórmula simples:

$$\text{lcm}(a, b) = \frac{a \cdot b}{\gcd(a, b)}$$

Assim, o MMC pode ser calculado usando o algoritmo de Euclides com a mesma complexidade de tempo:

Uma possível implementação, que evita inteligentemente estouros de inteiro dividindo primeiro $a$ pelo MDC, é dada aqui:

```cpp
int lcm (int a, int b) {
    return a / gcd(a, b) * b;
}
```

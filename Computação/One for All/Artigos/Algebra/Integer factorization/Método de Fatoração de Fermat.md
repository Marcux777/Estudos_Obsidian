
Podemos escrever um número composto ímpar  $n = p \cdot q$  como a diferença de dois quadrados  $n = a^2 - b^2$ :
$$n = \left(\frac{p + q}{2}\right)^2 - \left(\frac{p - q}{2}\right)^2$$ 
O método de fatoração de Fermat tenta explorar esse fato, adivinhando o primeiro quadrado  $a^2$ , e verifica se a parte restante  $b^2 = a^2 - n$  também é um número quadrado. Se for, então encontramos os fatores  $a - b$  e  $a + b$  de  $n$ .
```cpp
int fermat(int n) {
    int a = ceil(sqrt(n));
    int b2 = a*a - n;
    int b = round(sqrt(b2));
    while (b * b != b2) {
        a = a + 1;
        b2 = a*a - n;
        b = round(sqrt(b2));
    }
    return a - b;
}
```
Note que, este método de fatoração pode ser muito rápido, se a diferença entre os dois fatores  $p$  e  $q$  for pequena. O algoritmo funciona em  $O(|p - q|)$  tempo. No entanto, como é muito lento, uma vez que os fatores estão distantes, raramente é usado na prática.

No entanto, ainda existem um grande número de otimizações para essa abordagem. Por exemplo, ao olhar para os quadrados  $a^2$  módulo um número pequeno fixo, você pode notar que não precisa olhar para certos valores  $a$ , pois eles não podem produzir um número quadrado  $a^2 - n$ .
Enquanto o [Algoritmo de Euclides](obsidian://open?vault=Estudos_Obsidian&file=Computa%C3%A7%C3%A3o%2FOne%20for%20All%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum) calcula apenas o maior divisor comum (MDC) de dois inteiros $a$ e $b$, a versão estendida também encontra uma maneira de representar o MDC em termos de $a$ e $b$, ou seja, coeficientes $x$ e $y$ para os quais:

$$a \cdot x + b \cdot y = \gcd(a, b)$$

É importante notar que pela[ identidade de Bézout](https://en.wikipedia.org/wiki/Bézout%27s_identity), podemos sempre encontrar tal representação. Por exemplo, $\gcd(55, 80) = 5$, portanto, podemos representar $5$ como uma combinação linear com os termos $55$ e $80$: $55 \cdot 3 + 80 \cdot (-2) = 5$

Uma forma mais geral desse problema é discutida no artigo sobre [[Equações Diofantinas Lineares]]. Ele se baseará neste algoritmo.

## Algoritmo

Vamos denotar o MDC de $a$ e $b$ com $g$ nesta seção.

As mudanças no algoritmo original são muito simples. Se nos lembrarmos do algoritmo, podemos ver que o algoritmo termina com $b = 0$ e $a = g$. Para esses parâmetros, podemos facilmente encontrar coeficientes, ou seja, $g \cdot 1 + 0 \cdot 0 = g$.

Começando com esses coeficientes $(x, y) = (1, 0)$, podemos voltar nas chamadas recursivas. Tudo o que precisamos fazer é descobrir como os coeficientes $x$ e $y$ mudam durante a transição de $(a, b)$ para $(b, a \bmod b)$.

Vamos supor que encontramos os coeficientes $(x_1, y_1)$ para $(b, a \bmod b)$:

$$b \cdot x_1 + (a \bmod b) \cdot y_1 = g$$
e queremos encontrar o par $(x, y)$ para $(a, b)$:

$$ a \cdot x + b \cdot y = g$$
Podemos representar $a \bmod b$ como:

$$ a \bmod b = a - \left\lfloor \frac{a}{b} \right\rfloor \cdot b$$
Substituindo essa expressão na equação do coeficiente de $(x_1, y_1)$, obtemos:

$$ g = b \cdot x_1 + (a \bmod b) \cdot y_1 = b \cdot x_1 + \left(a - \left\lfloor \frac{a}{b} \right\rfloor \cdot b \right) \cdot y_1$$
e após rearranjar os termos:

$$g = a \cdot y_1 + b \cdot \left( x_1 - y_1 \cdot \left\lfloor \frac{a}{b} \right\rfloor \right)$$
Encontramos os valores de $x$ e $y$:

$$\begin{cases} x = y_1 \\ y = x_1 - y_1 \cdot \left\lfloor \frac{a}{b} \right\rfloor \end{cases} $$
## Implementação

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

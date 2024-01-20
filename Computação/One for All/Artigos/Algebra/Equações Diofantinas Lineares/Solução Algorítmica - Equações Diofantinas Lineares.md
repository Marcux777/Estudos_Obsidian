
Para encontrar uma solução da equação diofantina com 2 incógnitas, você pode usar o algoritmo Euclidiano Estendido. Primeiro, suponha que $a$ e $b$ são não negativos. Quando aplicamos o algoritmo Euclidiano Estendido para $a$ e $b$, podemos encontrar o máximo divisor comum $g$ e 2 números $x_g$ e $y_g$ tais que:

$$a x_g + b y_g = g$$
Se $c$ é divisível por $g = \gcd(a, b)$, então a equação diofantina dada tem uma solução, caso contrário, ela não tem nenhuma solução. A prova é direta: uma combinação linear de dois números é divisível pelo seu divisor comum.

Agora suponha que $c$ é divisível por $g$, então temos:

$$a \cdot x_g \cdot \frac{c}{g} + b \cdot y_g \cdot \frac{c}{g} = c$$
Portanto, uma das soluções da equação diofantina é:

$$x_0 = x_g \cdot \frac{c}{g},$$
$$y_0 = y_g \cdot \frac{c}{g}.$$
A ideia acima ainda funciona quando $a$ ou $b$ ou ambos são negativos. Só precisamos mudar o sinal de $x_0$ e $y_0$ quando necessário.

Finalmente, podemos implementar essa ideia da seguinte maneira (observe que este código não considera o caso $a = b = 0$):

```c++
int gcd(int a, int b, int& x, int& y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int x1, y1;
    int d = gcd(b, a % b, x1, y1);
    x = y1;
    y = x1 - y1 * (a / b);
    return d;
}

bool find_any_solution(int a, int b, int c, int &x0, int &y0, int &g) {
    g = gcd(abs(a), abs(b), x0, y0);
    if (c % g) {
        return false;
    }

    x0 *= c / g;
    y0 *= c / g;
    if (a < 0) x0 = -x0;
    if (b < 0) y0 = -y0;
    return true;
}
```

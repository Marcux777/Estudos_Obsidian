A partir de uma solução $(x_0, y_0)$, podemos obter todas as soluções da equação dada.

Seja $g = \gcd(a, b)$ e seja $x_0, y_0$ inteiros que satisfazem a seguinte relação:

$$a \cdot x_0 + b \cdot y_0 = c$$
Agora, devemos ver que adicionar $b / g$ a $x_0$, e, ao mesmo tempo, subtrair $a / g$ de $y_0$ não quebrará a igualdade:

$$a \cdot \left(x_0 + \frac{b}{g}\right) + b \cdot \left(y_0 - \frac{a}{g}\right) = a \cdot x_0 + b \cdot y_0 + a \cdot \frac{b}{g} - b \cdot \frac{a}{g} = c$$
Obviamente, esse processo pode ser repetido novamente, então todos os números da forma:

$$x = x_0 + k \cdot \frac{b}{g}$$
$$y = y_0 - k \cdot \frac{a}{g}$$
são soluções da equação diofantina dada.

Além disso, este é o conjunto de todas as soluções possíveis da equação diofantina dada.
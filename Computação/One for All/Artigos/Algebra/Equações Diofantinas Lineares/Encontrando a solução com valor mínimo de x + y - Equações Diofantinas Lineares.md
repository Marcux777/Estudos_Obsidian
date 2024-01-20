
Aqui, $x$ e $y$ também precisam ser dados algumas restrições, caso contrário, a resposta pode se tornar menos infinito.

A ideia é semelhante à seção anterior: encontramos qualquer solução da equação diofantina e, em seguida, deslocamos a solução para satisfazer algumas condições.

Finalmente, use o conhecimento do conjunto de todas as soluções para encontrar o mínimo:

$$x' = x + k \cdot \frac{b}{g},$$
$$y' = y - k \cdot \frac{a}{g}.$$
Note que $x + y$ muda da seguinte forma:

$$x' + y' = x + y + k \cdot \left(\frac{b}{g} - \frac{a}{g}\right) = x + y + k \cdot \frac{b-a}{g}$$
Se $a < b$, precisamos selecionar o menor valor possível de $k$. Se $a > b$, precisamos selecionar o maior valor possível de $k$. Se $a = b$, todas as soluções terão a mesma soma $x + y$.
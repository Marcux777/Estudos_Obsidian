Uma Equação Diofantina Linear (em duas variáveis) é uma equação da forma geral:

$$ax + by = c$$
onde $a$, $b$, $c$ são inteiros dados, e $x$, $y$ são inteiros desconhecidos.

Neste artigo, consideramos vários problemas clássicos sobre essas equações:

- encontrar uma solução
- encontrar todas as soluções
- encontrar o número de soluções e as próprias soluções em um dado intervalo
- encontrar uma solução com valor mínimo de $x + y$
### O caso degenerado
Um caso degenerado que precisa ser tratado é quando $a = b = 0$. É fácil ver que ou não temos soluções ou temos infinitas soluções, dependendo de se $c = 0$ ou não. No restante deste artigo, ignoraremos este caso.

### Solução analítica
Quando $a \neq 0$ e $b \neq 0$, a equação $ax+by=c$ pode ser tratada de forma equivalente como qualquer uma das seguintes:

$$\begin{gather} ax \equiv c \pmod b,\\ by \equiv c \pmod a. \end{gather}$$
Sem perda de generalidade, suponha que $b \neq 0$ e considere a primeira equação. Quando $a$ e $b$ são coprimos, a solução para isso é dada como

$$x \equiv ca^{-1} \pmod b,$$
onde $a^{-1}$ é o inverso modular de $a$ módulo $b$.

Quando $a$ e $b$ não são coprimos, os valores de $ax$ módulo $b$ para todos os inteiros $x$ são divisíveis por $g=\gcd(a, b)$, então a solução só existe quando $c$ é divisível por $g$. Neste caso, uma das soluções pode ser encontrada reduzindo a equação por $g$:

$$(a/g) x \equiv (c/g) \pmod{b/g}.$$
Pela definição de $g$, os números $a/g$ e $b/g$ são coprimos, então a solução é dada explicitamente como

$$\begin{cases} x \equiv (c/g)(a/g)^{-1}\pmod{b/g},\\ y = \frac{c-ax}{b}. \end{cases}$$

## Solução Algorítmica

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

## Obtendo todas as Soluções
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

## Encontrar o número de soluções e as soluções em um determinado intervalo

A partir da seção anterior, deve ficar claro que se não impusermos restrições às soluções, haverá um número infinito delas. Então, nesta seção, adicionamos algumas restrições ao intervalo de $x$ e $y$, e tentaremos contar e enumerar todas as soluções.

Suponha que existam dois intervalos: $[min_x; max_x]$ e $[min_y; max_y]$ e digamos que só queremos encontrar as soluções nesses dois intervalos.

Note que se $a$ ou $b$ é $0$, então o problema só tem uma solução. Não consideramos este caso aqui.

Primeiro, podemos encontrar uma solução que tenha o valor mínimo de $x$, tal que $x \ge min_x$. Para fazer isso, primeiro encontramos qualquer solução da equação diofantina. Em seguida, deslocamos essa solução para obter $x \ge min_x$ (usando o que sabemos sobre o conjunto de todas as soluções na seção anterior). Isso pode ser feito em $O(1)$. Denote este valor mínimo de $x$ por $l_{x1}$.

Da mesma forma, podemos encontrar o valor máximo de $x$ que satisfaça $x \le max_x$. Denote este valor máximo de $x$ por $r_{x1}$.

Da mesma forma, podemos encontrar o valor mínimo de $y$ $(y \ge min_y)$ e o valor máximo de $y$ $(y \le max_y)$. Denote os valores correspondentes de $x$ por $l_{x2}$ e $r_{x2}$.

A solução final são todas as soluções com x na interseção de $[l_{x1}, r_{x1}]$ e $[l_{x2}, r_{x2}]$. Vamos denotar esta interseção por $[l_x, r_x]$.

A seguir está o código implementando essa ideia. Observe que dividimos $a$ e $b$ no início por $g$. Como a equação $a x + b y = c$ é equivalente à equação $\frac{a}{g} x + \frac{b}{g} y = \frac{c}{g}$, podemos usar esta última e ter $\gcd(\frac{a}{g}, \frac{b}{g}) = 1$, o que simplifica as fórmulas.

```c++
void shift_solution(int & x, int & y, int a, int b, int cnt) {
    x += cnt * b;
    y -= cnt * a;
}

int find_all_solutions(int a, int b, int c, int minx, int maxx, int miny, int maxy) {
    int x, y, g;
    if (!find_any_solution(a, b, c, x, y, g))
        return 0;
    a /= g;
    b /= g;

    int sign_a = a > 0 ? +1 : -1;
    int sign_b = b > 0 ? +1 : -1;

    shift_solution(x, y, a, b, (minx - x) / b);
    if (x < minx)
        shift_solution(x, y, a, b, sign_b);
    if (x > maxx)
        return 0;
    int lx1 = x;

    shift_solution(x, y, a, b, (maxx - x) / b);
    if (x > maxx)
        shift_solution(x, y, a, b, -sign_b);
    int rx1 = x;

    shift_solution(x, y, a, b, -(miny - y) / a);
    if (y < miny)
        shift_solution(x, y, a, b, -sign_a);
    if (y > maxy)
        return 0;
    int lx2 = x;

    shift_solution(x, y, a, b, -(maxy - y) / a);
    if (y > maxy)
        shift_solution(x, y, a, b, sign_a);
    int rx2 = x;

    if (lx2 > rx2)
        swap(lx2, rx2);
    int lx = max(lx1, lx2);
    int rx = min(rx1, rx2);

    if (lx > rx)
        return 0;
    return (rx - lx) / abs(b) + 1;
}
```
Uma vez que temos $l_x$ e $r_x$, também é simples enumerar todas as soluções. Basta iterar através de $x = l_x + k \cdot \frac{b}{g}$ para todos $k \ge 0$ até $x = r_x$, e encontrar os valores correspondentes de $y$ usando a equação $a x + b y = c$.

## Encontrando a solução com valor mínimo de $x + y$

Aqui, $x$ e $y$ também precisam ser dados algumas restrições, caso contrário, a resposta pode se tornar menos infinito.

A ideia é semelhante à seção anterior: encontramos qualquer solução da equação diofantina e, em seguida, deslocamos a solução para satisfazer algumas condições.

Finalmente, use o conhecimento do conjunto de todas as soluções para encontrar o mínimo:

$$x' = x + k \cdot \frac{b}{g},$$
$$y' = y - k \cdot \frac{a}{g}.$$
Note que $x + y$ muda da seguinte forma:

$$x' + y' = x + y + k \cdot \left(\frac{b}{g} - \frac{a}{g}\right) = x + y + k \cdot \frac{b-a}{g}$$
Se $a < b$, precisamos selecionar o menor valor possível de $k$. Se $a > b$, precisamos selecionar o maior valor possível de $k$. Se $a = b$, todas as soluções terão a mesma soma $x + y$.
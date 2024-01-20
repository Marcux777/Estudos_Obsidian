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

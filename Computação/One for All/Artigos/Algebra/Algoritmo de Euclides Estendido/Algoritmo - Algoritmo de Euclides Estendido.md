
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
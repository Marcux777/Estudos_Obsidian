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

[[Solução Algorítmica - Equações Diofantinas Lineares]]
[[Obtendo todas as Soluções - Equações Diofantinas Lineares]]
[[Encontrar o número de soluções e as soluções em um determinado intervalo - Equações Diofantinas Lineares]]
[[Encontrando a solução com valor mínimo de x + y - Equações Diofantinas Lineares]]

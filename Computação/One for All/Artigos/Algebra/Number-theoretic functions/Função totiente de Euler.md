
A função totiente de Euler, também conhecida como função phi  $\phi (n)$ , conta o número de inteiros entre 1 e  $n$  inclusivo, que são coprimos a  $n$ . Dois números são coprimos se o maior divisor comum deles for igual a  $1$  ( $1$  é considerado coprimo a qualquer número).

Aqui estão os valores de  $\phi(n)$  para os primeiros inteiros positivos:
 
$$\begin{array}{|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|} \hline n & 1 & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 & 11 & 12 & 13 & 14 & 15 & 16 & 17 & 18 & 19 & 20 & 21 \\\\ \hline \phi(n) & 1 & 1 & 2 & 2 & 4 & 2 & 6 & 4 & 6 & 4 & 10 & 4 & 12 & 6 & 8 & 8 & 16 & 6 & 18 & 8 & 12 \\\\ \hline \end{array}$$ 
## Propriedades
As seguintes propriedades da função totiente de Euler são suficientes para calculá-la para qualquer número:

- Se  $p$  é um número primo, então  $\gcd(p, q) = 1$  para todos  $1 \le q < p$ . Portanto, temos:
 
$$\phi (p) = p - 1.$$ 
- Se  $p$  é um número primo e  $k \ge 1$ , então existem exatamente  $p^k / p$  números entre  $1$  e  $p^k$  que são divisíveis por  $p$ . O que nos dá:
 
$$\phi(p^k) = p^k - p^{k-1}.$$ 
- Se  $a$  e  $b$  são primos entre si, então:
$$\phi(a b) = \phi(a) \cdot \phi(b).$$ 
Essa relação não é trivial de se ver. Ela decorre do teorema chinês do resto. O teorema chinês do resto garante que, para cada  $0 \le x < a$  e cada  $0 \le y < b$ , existe um único  $0 \le z < a b$  com  $z \equiv x \pmod{a}$  e  $z \equiv y \pmod{b}$ . Não é difícil mostrar que  $z$  é coprimo a  $a b$  se e somente se  $x$  é coprimo a  $a$  e  $y$  é coprimo a  $b$ . Portanto, a quantidade de inteiros coprimos a  $a b$  é igual ao produto das quantidades de  $a$  e $b$ .

- Em geral, para  $a$  e  $b$  não coprimos, a equação
 
$$\phi(ab) = \phi(a) \cdot \phi(b) \cdot \dfrac{d}{\phi(d)}$$ 
com  $d = \gcd(a, b)$  é válida.

Assim, usando as três primeiras propriedades, podemos calcular  $\phi(n)$  através da fatoração de  $n$  (decomposição de  $n$  em um produto de seus fatores primos). Se  $n = {p_1}^{a_1} \cdot {p_2}^{a_2} \cdots {p_k}^{a_k}$ , onde  $p_i$  são fatores primos de  $n$ ,
 
 
$$\begin{align} \phi (n) &= \phi ({p_1}^{a_1}) \cdot \phi ({p_2}^{a_2}) \cdots \phi ({p_k}^{a_k}) \\\\ &= \left({p_1}^{a_1} - {p_1}^{a_1 - 1}\right) \cdot \left({p_2}^{a_2} - {p_2}^{a_2 - 1}\right) \cdots \left({p_k}^{a_k} - {p_k}^{a_k - 1}\right) \\\\ &= p_1^{a_1} \cdot \left(1 - \frac{1}{p_1}\right) \cdot p_2^{a_2} \cdot \left(1 - \frac{1}{p_2}\right) \cdots p_k^{a_k} \cdot \left(1 - \frac{1}{p_k}\right) \\\\ &= n \cdot \left(1 - \frac{1}{p_1}\right) \cdot \left(1 - \frac{1}{p_2}\right) \cdots \left(1 - \frac{1}{p_k}\right) \end{align}$$

[[Implementation - Função totiente de Euler]]
[[Função totiente de Euler de 1 a  n em  O(n loglogn)]]
[[Propriedade da soma dos divisores]]
[[Aplicação no teorema de Euler]]
[[Generalização]]


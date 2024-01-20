
Considere um sistema de duas equações para números primos entre si, $m_1, m_2$:

$$ \left\{\begin{align} a &\equiv a_1 \pmod{m_1} \\ a &\equiv a_2 \pmod{m_2} \\ \end{align}\right. $$

Queremos encontrar uma solução para $a \pmod{m_1 m_2}$. Usando o [Algoritmo Euclidiano Estendido](obsidian://open?vault=Algoritmos&file=algoritmos%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20Estendido%2FAlgoritmo%20-%20Algoritmo%20de%20Euclides%20Estendido), podemos encontrar os coeficientes de Bézout, $n_1, n_2$, tais que

$$n_1 m_1 + n_2 m_2 = 1.$$

Na verdade, $n_1$ e $n_2$ são apenas os [[inversos modulares]] de $m_1$ e $m_2$ módulo $m_2$ e $m_1$, respectivamente. Temos $n_1 m_1 \equiv 1 \pmod{m_2}$, então $n_1 \equiv m_1^{-1} \pmod{m_2}$, e vice-versa, $n_2 \equiv m_2^{-1} \pmod{m_1}$.

Com esses dois coeficientes, podemos definir uma solução:

$$a = (a_1 n_2 m_2 + a_2 n_1 m_1) \bmod{m_1 m_2}$$

É fácil verificar que isso é de fato uma solução calculando $a \bmod{m_1}$ e $a \bmod{m_2}$.

$$ \begin{array}{rcll} a & \equiv & a_1 n_2 m_2 + a_2 n_1 m_1 & \pmod{m_1}\\ & \equiv & a_1 (1 - n_1 m_1) + a_2 n_1 m_1 & \pmod{m_1}\\ & \equiv & a_1 - a_1 n_1 m_1 + a_2 n_1 m_1 & \pmod{m_1}\\ & \equiv & a_1 & \pmod{m_1} \end{array} $$

Observe que o Teorema Chinês dos Restos também garante que apenas uma solução existe módulo $m_1 m_2$. Isso também é fácil de provar.

Vamos assumir que você tenha duas soluções diferentes, $x$ e $y$. Como $x \equiv a_i \pmod{m_i}$ e $y \equiv a_i \pmod{m_i}$, segue que $x − y \equiv 0 \pmod{m_i}$ e, portanto, $x − y \equiv 0 \pmod{m_1 m_2}$ ou, equivalentemente, $x \equiv y \pmod{m_1 m_2}$. Portanto, $x$ e $y$ são, na verdade, a mesma solução.
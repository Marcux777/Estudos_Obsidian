
Seja $m = m_1 \cdot m_2 \cdots m_k$, onde $m_i$ são primos entre si dois a dois. Além dos $m_i$, também nos é fornecido um sistema de congruências

$$\left\{\begin{array}{rcl} a & \equiv & a_1 \pmod{m_1} \\ a & \equiv & a_2 \pmod{m_2} \\ & \vdots & \\ a & \equiv & a_k \pmod{m_k} \end{array}\right.$$

onde $a_i$ são constantes fornecidas. A forma original do Teorema Chinês dos Restos (CRT) afirma que o sistema dado de congruências sempre possui uma e exatamente uma solução módulo $m$.

Por exemplo, o sistema de congruências

$$\left\{\begin{array}{rcl} a & \equiv & 2 \pmod{3} \\ a & \equiv & 3 \pmod{5} \\ a & \equiv & 2 \pmod{7} \end{array}\right.$$

tem a solução $23$ módulo $105$, porque $23 \bmod{3} = 2$, $23 \bmod{5} = 3$ e $23 \bmod{7} = 2$. Podemos expressar todas as soluções como $23 + 105\cdot k$ para $k \in \mathbb{Z}$.

[[Corolário]]
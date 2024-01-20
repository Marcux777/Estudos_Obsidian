
Como mencionado, o algoritmo acima só funciona para módulos coprimos $m_1, m_2, \dots, m_k$.

No caso em que os módulos não são coprimos, um sistema de congruências tem exatamente uma solução módulo $\text{lcm}(m_1, m_2, \dots, m_k)$ ou não tem solução alguma.

Por exemplo, no sistema a seguir, a primeira congruência implica que a solução é ímpar, e a segunda congruência implica que a solução é par. Não é possível que um número seja simultaneamente ímpar e par, portanto, claramente não há solução.

$$\left\{\begin{align} a & \equiv 1 \pmod{4} \\ a & \equiv 2 \pmod{6} \end{align}\right.$$

É bastante simples determinar se um sistema tem uma solução. E se tiver, podemos usar o algoritmo original para resolver um sistema de congruências ligeiramente modificado.

Uma única congruência $a \equiv a_i \pmod{m_i}$ é equivalente ao sistema de congruências $a \equiv a_i \pmod{p_j^{n_j}}$ onde $p_1^{n_1} p_2^{n_2}\cdots p_k^{n_k}$ é a fatoração em primos de $m_i$.

Com esse fato, podemos modificar o sistema de congruências para um sistema que tenha apenas potências de primos como módulos. Por exemplo, o sistema de congruências acima é equivalente a:

$$\left\{\begin{array}{ll} a \equiv 1 & \pmod{4} \\ a \equiv 2 \equiv 0 & \pmod{2} \\ a \equiv 2 & \pmod{3} \end{array}\right.$$

Como originalmente alguns módulos tinham fatores comuns, obteremos alguns módulos de congruência com base no mesmo número primo, embora possivelmente com diferentes potências de primos.

Podemos observar que a congruência com o módulo de potência de primo mais alto será a congruência mais forte de todas as congruências baseadas no mesmo número primo. Ou ela fornecerá uma contradição com alguma outra congruência ou já implicará todas as outras congruências.

No nosso caso, a primeira congruência $a \equiv 1 \pmod{4}$ implica $a \equiv 1 \pmod{2}$ e, portanto, contradiz a segunda congruência $a \equiv 0 \pmod{2}$. Portanto, este sistema de congruências não tem solução.

Se não houver contradições, então o sistema de equações tem uma solução. Podemos ignorar todas as congruências, exceto aquelas com o módulo de potência de primo mais alto. Esses módulos são agora coprimos e, portanto, podemos resolver este sistema com o algoritmo discutido nas seções anteriores.

Por exemplo, o seguinte sistema tem uma solução módulo $\text{lcm}(10, 12) = 60$:

$$\left\{\begin{align} a & \equiv 3 \pmod{10} \\ a & \equiv 5 \pmod{12} \end{align}\right.$$

O sistema de congruências é equivalente ao sistema de congruências:

$$\left\{\begin{align} a & \equiv 3 \equiv 1 \pmod{2} \\ a & \equiv 3 \equiv 3 \pmod{5} \\ a & \equiv 5 \equiv 1 \pmod{4} \\ a & \equiv 5 \equiv 2 \pmod{3} \end{align}\right.$$

A única congruência com o mesmo módulo primo é $a \equiv 1 \pmod{4}$ e $a \equiv 1 \pmod{2}$. A primeira já implica a segunda, então podemos ignorar a segunda e resolver o seguinte sistema com módulos coprimos:

$$\left\{\begin{align} a & \equiv 3 \equiv 3 \pmod{5} \\ a & \equiv 5 \equiv 1 \pmod{4} \\ a & \equiv 5 \equiv 2 \pmod{3} \end{align}\right.$$

Ele tem a solução $53 \pmod{60}$, e de fato $53 \bmod{10} = 3$ e $53 \bmod{12} = 5$.
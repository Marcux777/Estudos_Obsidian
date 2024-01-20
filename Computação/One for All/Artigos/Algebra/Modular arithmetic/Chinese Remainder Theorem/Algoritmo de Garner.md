Outra consequência do Teorema Chinês dos Restos (CRT) é que podemos representar números grandes usando um array de inteiros pequenos.

Em vez de realizar muitos cálculos com números muito grandes, o que pode ser caro (pense em fazer divisões com números de 1000 dígitos), você pode escolher alguns módulos coprimos e representar o número grande como um sistema de congruências, realizando todas as operações no sistema de equações. Qualquer número $a$ menor que $m_1 m_2 \cdots m_k$ pode ser representado como um array $a_1, \ldots, a_k$, onde $a \equiv a_i \pmod{m_i}$.

Usando o algoritmo mencionado anteriormente, você pode reconstruir novamente o número grande sempre que precisar.

Alternativamente, você pode representar o número na forma de representação mista de base:

$$a = x_1 + x_2 m_1 + x_3 m_1 m_2 + \ldots + x_k m_1 \cdots m_{k-1} \text{ com } x_i \in [0, m_i)$$

O algoritmo de Garner, que é discutido no artigo dedicado a [[Garner's Algorithm]], calcula os coeficientes $x_i$. E com esses coeficientes, você pode restaurar o número completo.
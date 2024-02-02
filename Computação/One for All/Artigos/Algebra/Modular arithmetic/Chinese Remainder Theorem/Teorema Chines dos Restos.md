

O Teorema dos Restos Chineses (que será referido como CRT ao longo deste artigo) foi descoberto pelo matemático chinês Sun Zi.

## Formulação

Seja $m = m_1 \cdot m_2 \cdots m_k$, onde $m_i$ são primos entre si dois a dois. Além dos $m_i$, também nos é fornecido um sistema de congruências

$$\left\{\begin{array}{rcl} a & \equiv & a_1 \pmod{m_1} \\ a & \equiv & a_2 \pmod{m_2} \\ & \vdots & \\ a & \equiv & a_k \pmod{m_k} \end{array}\right.$$

onde $a_i$ são constantes fornecidas. A forma original do Teorema Chinês dos Restos (CRT) afirma que o sistema dado de congruências sempre possui uma e exatamente uma solução módulo $m$.

Por exemplo, o sistema de congruências

$$\left\{\begin{array}{rcl} a & \equiv & 2 \pmod{3} \\ a & \equiv & 3 \pmod{5} \\ a & \equiv & 2 \pmod{7} \end{array}\right.$$

tem a solução $23$ módulo $105$, porque $23 \bmod{3} = 2$, $23 \bmod{5} = 3$ e $23 \bmod{7} = 2$. Podemos expressar todas as soluções como $23 + 105\cdot k$ para $k \in \mathbb{Z}$.

### Corolário

Uma consequência do Teorema Chinês dos Restos (CRT) é que a equação

$$x \equiv a \pmod{m}$$

é equivalente ao sistema de equações

$$\left\{\begin{array}{rcl} x & \equiv & a_1 \pmod{m_1} \\ & \vdots & \\ x & \equiv & a_k \pmod{m_k} \end{array}\right.$$

(Como mencionado anteriormente, assuma que $m = m_1 m_2 \cdots m_k$ e que $m_i$ são primos entre si dois a dois).

## Solução para Dois Módulos

Considere um sistema de duas equações para números primos entre si, $m_1, m_2$:

$$ \left\{\begin{align} a &\equiv a_1 \pmod{m_1} \\ a &\equiv a_2 \pmod{m_2} \\ \end{align}\right. $$

Queremos encontrar uma solução para $a \pmod{m_1 m_2}$. Usando o [Algoritmo Euclidiano Estendido](obsidian://open?vault=Algoritmos&file=algoritmos%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20Estendido%2FAlgoritmo%20-%20Algoritmo%20de%20Euclides%20Estendido), podemos encontrar os coeficientes de Bézout, $n_1, n_2$, tais que

$$n_1 m_1 + n_2 m_2 = 1.$$

Na verdade, $n_1$ e $n_2$ são apenas os [inversos modulares](obsidian://open?vault=Estudos_Obsidian&file=Computa%C3%A7%C3%A3o%2FOne%20for%20All%2FArtigos%2FAlgebra%2FModular%20arithmetic%2FModular%20Inverse%2FInverso%20Multiplicativo%20Modular) de $m_1$ e $m_2$ módulo $m_2$ e $m_1$, respectivamente. Temos $n_1 m_1 \equiv 1 \pmod{m_2}$, então $n_1 \equiv m_1^{-1} \pmod{m_2}$, e vice-versa, $n_2 \equiv m_2^{-1} \pmod{m_1}$.

Com esses dois coeficientes, podemos definir uma solução:

$$a = (a_1 n_2 m_2 + a_2 n_1 m_1) \bmod{m_1 m_2}$$

É fácil verificar que isso é de fato uma solução calculando $a \bmod{m_1}$ e $a \bmod{m_2}$.

$$ \begin{array}{rcll} a & \equiv & a_1 n_2 m_2 + a_2 n_1 m_1 & \pmod{m_1}\\ & \equiv & a_1 (1 - n_1 m_1) + a_2 n_1 m_1 & \pmod{m_1}\\ & \equiv & a_1 - a_1 n_1 m_1 + a_2 n_1 m_1 & \pmod{m_1}\\ & \equiv & a_1 & \pmod{m_1} \end{array} $$

Observe que o Teorema Chinês dos Restos também garante que apenas uma solução existe módulo $m_1 m_2$. Isso também é fácil de provar.

Vamos assumir que você tenha duas soluções diferentes, $x$ e $y$. Como $x \equiv a_i \pmod{m_i}$ e $y \equiv a_i \pmod{m_i}$, segue que $x − y \equiv 0 \pmod{m_i}$ e, portanto, $x − y \equiv 0 \pmod{m_1 m_2}$ ou, equivalentemente, $x \equiv y \pmod{m_1 m_2}$. Portanto, $x$ e $y$ são, na verdade, a mesma solução.

## Solução para o Caso Geral
### Solução Indutiva

Como $m_1 m_2$ é coprimo a $m_3$, podemos aplicar repetidamente a solução para dois módulos para qualquer número de módulos. Primeiro, você calcula $b_2 := a \pmod{m_1 m_2}$ usando as duas primeiras congruências, então você pode calcular $b_3 := a \pmod{m_1 m_2 m_3}$ usando as congruências $a \equiv b_2 \pmod{m_1 m_2}$ e $a \equiv a_3 \pmod {m_3}$, e assim por diante.

### Construção Direta

Uma construção direta semelhante à interpolação de Lagrange é possível.

Defina $M_i := \prod_{i \neq j} m_j$, o produto de todos os módulos exceto $m_i$, e $N_i$ como os inversos modulares $N_i := M_i^{-1} \bmod{m_i}$. Então, uma solução para o sistema de congruências é:

$$a \equiv \sum_{i=1}^k a_i M_i N_i \pmod{m_1 m_2 \cdots m_k}$$

Podemos verificar que isso é de fato uma solução, calculando $a \bmod{m_i}$ para todos os $i$. Como $M_j$ é um múltiplo de $m_i$ para $i \neq j$, temos:

$$\begin{array}{rcll} a & \equiv & \sum_{j=1}^k a_j M_j N_j & \pmod{m_i} \\ & \equiv & a_i M_i N_i & \pmod{m_i} \\ & \equiv & a_i M_i M_i^{-1} & \pmod{m_i} \\ & \equiv & a_i & \pmod{m_i} \end{array}$$
### Implementação

```cpp
struct Congruence {
    long long a, m;
};

long long chinese_remainder_theorem(vector<Congruence> const& congruences) {
    long long M = 1;
    for (auto const& congruence : congruences) {
        M *= congruence.m;
    }

    long long solution = 0;
    for (auto const& congruence : congruences) {
        long long a_i = congruence.a;
        long long M_i = M / congruence.m;
        long long N_i = mod_inv(M_i, congruence.m);
        solution = (solution + a_i * M_i % M * N_i) % M;
    }
    return solution;
}
```
## Solução para Módulos não Coprimos

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
## Algoritmo de Garner
Outra consequência do Teorema Chinês dos Restos (CRT) é que podemos representar números grandes usando um array de inteiros pequenos.

Em vez de realizar muitos cálculos com números muito grandes, o que pode ser caro (pense em fazer divisões com números de 1000 dígitos), você pode escolher alguns módulos coprimos e representar o número grande como um sistema de congruências, realizando todas as operações no sistema de equações. Qualquer número $a$ menor que $m_1 m_2 \cdots m_k$ pode ser representado como um array $a_1, \ldots, a_k$, onde $a \equiv a_i \pmod{m_i}$.

Usando o algoritmo mencionado anteriormente, você pode reconstruir novamente o número grande sempre que precisar.

Alternativamente, você pode representar o número na forma de representação mista de base:

$$a = x_1 + x_2 m_1 + x_3 m_1 m_2 + \ldots + x_k m_1 \cdots m_{k-1} \text{ com } x_i \in [0, m_i)$$

O algoritmo de Garner, que é discutido no artigo dedicado a [[Garner's Algorithm]], calcula os coeficientes $x_i$. E com esses coeficientes, você pode restaurar o número completo.
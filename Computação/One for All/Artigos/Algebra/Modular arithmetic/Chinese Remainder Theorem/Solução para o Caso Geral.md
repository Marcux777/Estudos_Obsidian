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
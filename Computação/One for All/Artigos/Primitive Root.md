## Definição

Em aritmética modular, um número  $g$  é chamado de raiz primitiva módulo  $n$  se todo número primo com  $n$  for congruente a uma potência de  $g$  módulo  $n$ . Matematicamente,  $g$  é uma raiz primitiva módulo  $n$  se e somente se, para qualquer número inteiro  $a$  tal que  $\gcd(a, n) = 1$ , existe um inteiro  $k$  tal que: 
$g^k \equiv a \pmod n$ 

$k$  é então chamado de índice ou logaritmo discreto de  $a$  na base  $g$  módulo  $n$ .  
$g$  também é chamado de gerador do grupo multiplicativo dos inteiros módulo  
$n$ .

Em particular, no caso em que  $n$  é um número primo, as potências da raiz primitiva percorrem todos os números de  $1$  a  $n-1$ .

## Existência

Uma raiz primitiva módulo  $n$  existe se e somente se:
- $n$  é 1, 2, 4, ou
 
- $n$  é uma potência de um número primo ímpar  $(n = p^k)$ , ou
 
- $n$  é o dobro de uma potência de um número primo ímpar  $(n = 2 \cdot p^k)$ .

Este teorema foi provado por Gauss em 1801.

## Relação com a Função de Euler

Seja  $g$  uma raiz primitiva módulo  $n$ . Podemos mostrar que o menor número  $k$  para o qual  
$g^k \equiv 1 \pmod n$  é igual a  $\phi (n)$ . Além disso, o inverso também é verdadeiro, e esse fato será usado neste artigo para encontrar uma raiz primitiva.

Além disso, o número de raízes primitivas módulo  $n$ , se existirem, é igual a  $\phi (\phi (n) )$ .

## Algoritmo para encontrar uma raiz primitiva

Um algoritmo ingênuo seria considerar todos os números no intervalo  $[1, n-1]$ . Em seguida, verificar se cada um é uma raiz primitiva, calculando todas as suas potências para ver se são todas diferentes. Este algoritmo tem complexidade  $O(g \cdot n)$ , o que seria muito lento. Nesta seção, propomos um algoritmo mais rápido usando vários teoremas bem conhecidos.

Da seção anterior, sabemos que se o menor número  $k$  para o qual  $g^k \equiv 1 \pmod n$  é  $\phi (n)$ , então  
$g$  é uma raiz primitiva. Como, para qualquer número  $a$  coprimo com  $n$ , sabemos pelo teorema de Euler que  $a ^ { \phi (n) } \equiv 1 \pmod n$ , então, para verificar se  $g$  é uma raiz primitiva, é suficiente verificar que para todos  $d$  menor que  $\phi (n)$ ,  $g^d \not \equiv 1 \pmod n$ . No entanto, este algoritmo ainda é muito lento.

Do teorema de Lagrange, sabemos que o índice de 1 de qualquer número módulo  
$n$  deve ser um divisor de  $\phi (n)$ . Assim, é suficiente verificar para todos os divisores próprios  
$d \mid \phi (n)$  que  $g^d \not \equiv 1 \pmod n$ . Isso já é um algoritmo muito mais rápido, mas ainda podemos melhorar.

Fatorize  $\phi (n) = p_1 ^ {a_1} \cdots p_s ^ {a_s}$ . Provamos que, no algoritmo anterior, é suficiente considerar apenas os valores de  $d$  que têm a forma  $\frac { \phi (n) } {p_j}$ . De fato, seja  $d$  qualquer divisor próprio de  $\phi (n)$ . Então, obviamente, existe tal  $j$  que  $d \mid \frac { \phi (n) } {p_j}$ , isto é,  $d \cdot k = \frac { \phi (n) } {p_j}$ . No entanto, se  $g^d \equiv 1 \pmod n$ , teríamos:
 
$g ^ { \frac { \phi (n)} {p_j} } \equiv g ^ {d \cdot k} \equiv (g^d) ^k \equiv 1^k \equiv 1 \pmod n$ .

ou seja, entre os números da forma  $\frac {\phi (n)} {p_i}$ , haveria pelo menos um para o qual as condições não seriam atendidas.

Agora temos um algoritmo completo para encontrar a raiz primitiva:

-  Primeiro, encontre  $\phi (n)$  e a fatorize.
-  Em seguida, itere por todos os números  $g \in [1, n]$ , e para cada número, para verificar se é uma raiz primitiva, faça o seguinte:
	- Calcule todas as  $g ^ { \frac {\phi (n)} {p_i}} \pmod n$ .
	- Se todos os valores calculados forem diferentes de  $1$ , então  $g$  é uma raiz primitiva.

O tempo de execução deste algoritmo é  $O(Ans \cdot \log \phi (n) \cdot \log n)$  (assumindo que  $\phi (n)$  tem  $\log \phi (n)$  divisores).

Shoup (1990, 1992) provou, assumindo a [[hipótese generalizada de Riemann]], que  $g$  é  $O(\log^6 p)$ .
## Implementação

O código a seguir assume que o módulo  $p$  é um número primo. Para fazê-lo funcionar para qualquer valor de  $p$ , precisamos adicionar o cálculo de  $\phi (p)$ .

```cpp
int powmod(int a, int b, int p) {
    int res = 1;
    while (b)
        if (b & 1)
            res = int (res * 1ll * a % p), --b;
        else
            a = int (a * 1ll * a % p), b >>= 1;
    return res;
}

int generator(int p) {
    vector<int> fact;
    int phi = p - 1, n = phi;
    for (int i = 2; i * i <= n; ++i)
        if (n % i == 0) {
            fact.push_back(i);
            while (n % i == 0)
                n /= i;
        }
    if (n > 1)
        fact.push_back(n);

    for (int res = 2; res <= p; ++res) {
        bool ok = true;
        for (size_t i = 0; i < fact.size() && ok; ++i)
            ok &= powmod(res, phi / fact[i], p) != 1;
        if (ok) return res;
    }
    return -1;
}
```
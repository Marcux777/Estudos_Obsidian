
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
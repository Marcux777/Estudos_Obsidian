Para resolver o problema dado por completo, precisamos encontrar todas as soluções conhecendo uma delas:  $x_0 = g^{y_0} \pmod n$ .

Vamos lembrar o fato de que uma raiz primitiva sempre tem ordem de  
$\phi (n)$ , ou seja, a menor potência de  $g$  que resulta em 1 é  $\phi (n)$ . Portanto, se adicionarmos o termo  $\phi (n)$  ao exponencial, ainda obtemos o mesmo valor:
 
$x^k \equiv g^{ y_0 \cdot k + l \cdot \phi (n)} \equiv a \pmod n \forall l \in Z$ 

Assim, todas as soluções têm a forma:
 
$x = g^{y_0 + \frac {l \cdot \phi (n)}{k}} \pmod n \forall l \in Z$ .

onde  $l$  é escolhido de tal forma que a fração deve ser um número inteiro. Para que isso seja verdade, o numerador precisa ser divisível pelo mínimo múltiplo comum de  $\phi (n)$  e  $k$ . Lembre-se de que o mínimo múltiplo comum de dois números  $lcm(a, b) = \frac{a \cdot b}{gcd(a, b)}$ ; teremos
 
$x = g^{y_0 + i \frac {\phi (n)}{gcd(k, \phi (n))}} \pmod n \forall i \in Z$ .

Esta é a fórmula final para todas as soluções do problema da raiz discreta.



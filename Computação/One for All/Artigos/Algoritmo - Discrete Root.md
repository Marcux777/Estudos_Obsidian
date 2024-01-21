Resolveremos este problema reduzindo-o ao problema do logaritmo discreto.

Vamos aplicar o conceito de uma raiz primitiva módulo  $n$ . Seja  $g$  uma raiz primitiva módulo  
$n$ . Note que, uma vez que  $n$  é primo, ela deve existir, e pode ser encontrada em  $O(Ans \cdot \log \phi (n) \cdot \log n) = O(Ans \cdot \log^2 n)$  mais o tempo de fatoração de  $\phi (n)$ .

Podemos descartar facilmente o caso em que  $a = 0$ . Nesse caso, obviamente, há apenas uma resposta:   $x = 0$ .

Como sabemos que  $n$  é um número primo e que qualquer número entre 1 e  $n-1$  pode ser representado como uma potência da raiz primitiva, podemos representar o problema da raiz discreta da seguinte forma:

$(g^y)^k \equiv a \pmod n$ 

onde
 
$x \equiv g^y \pmod n$ 

Isso, por sua vez, pode ser reescrito como
 
$(g^k)^y \equiv a \pmod n$ 

Agora temos um desconhecido  $y$ , que é um problema de logaritmo discreto. A solução pode ser encontrada usando o algoritmo "baby-step giant-step" de Shanks em  $O(\sqrt {n} \log n)$  (ou podemos verificar se não há soluções).

Tendo encontrado uma solução  $y_0$ , uma das soluções do problema da raiz discreta será  $x_0 = g^{y_0} \pmod n$ .

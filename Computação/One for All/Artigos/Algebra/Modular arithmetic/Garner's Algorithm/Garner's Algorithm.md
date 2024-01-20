
Uma consequência do Teorema Chinês dos Restos (CRT) é que podemos representar números grandes usando um array de inteiros pequenos. Por exemplo, deixe $p$ ser o produto dos primeiros $1000$ números primos. $p$ tem cerca de $3000$ dígitos.

Qualquer número $a$ menor que $p$ pode ser representado como um array $a_1, \ldots, a_k$, onde $a_i \equiv a \pmod{p_i}$. Mas para fazer isso, obviamente, precisamos saber como recuperar o número $a$ a partir de sua representação. Uma maneira de fazer isso é discutida no artigo sobre o Teorema Chinês dos Restos.

Neste artigo, discutimos uma alternativa, o Algoritmo de Garner, que também pode ser usado para esse fim.

[[Representação de Base Mista]]
[[Implementação do Algoritmo de Garner]]
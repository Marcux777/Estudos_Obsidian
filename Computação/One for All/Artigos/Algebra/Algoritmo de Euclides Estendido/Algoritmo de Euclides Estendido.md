Enquanto o [Algoritmo de Euclides](obsidian://open?vault=Estudos_Obsidian&file=Computa%C3%A7%C3%A3o%2FOne%20for%20All%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum) calcula apenas o maior divisor comum (MDC) de dois inteiros $a$ e $b$, a versão estendida também encontra uma maneira de representar o MDC em termos de $a$ e $b$, ou seja, coeficientes $x$ e $y$ para os quais:

$$a \cdot x + b \cdot y = \gcd(a, b)$$

É importante notar que pela[ identidade de Bézout](https://en.wikipedia.org/wiki/Bézout%27s_identity), podemos sempre encontrar tal representação. Por exemplo, $\gcd(55, 80) = 5$, portanto, podemos representar $5$ como uma combinação linear com os termos $55$ e $80$: $55 \cdot 3 + 80 \cdot (-2) = 5$

Uma forma mais geral desse problema é discutida no artigo sobre [[Equações Diofantinas Lineares]]. Ele se baseará neste algoritmo.

[[Algoritmo - Algoritmo de Euclides Estendido]]
[[Implementação - Algoritmo de Euclides Estendido]]

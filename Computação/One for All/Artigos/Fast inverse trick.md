
Para calcular a inversa  $n^{\prime} := n^{-1} \bmod r$  de maneira eficiente, podemos usar o seguinte truque (inspirado no método de Newton):
$$a \cdot x \equiv 1 \bmod 2^k \Longrightarrow a \cdot x \cdot (2 - a \cdot x) \equiv 1 \bmod 2^{2k}$$ 
Isso pode ser facilmente comprovado. Se tivermos  $a \cdot x = 1 + m \cdot 2^k$ , então teremos:
$$\begin{aligned} a \cdot x \cdot (2 - a \cdot x) &= 2 \cdot a \cdot x - (a \cdot x)^2 \\ &= 2 \cdot (1 + m \cdot 2^k) - (1 + m \cdot 2^k)^2 \\ &= 2 + 2 \cdot m \cdot 2^k - 1 - 2 \cdot m \cdot 2^k - m^2 \cdot 2^{2k} \\ &= 1 - m^2 \cdot 2^{2k} \\ &\equiv 1 \bmod 2^{2k}. \end{aligned}$$ 
Isso significa que podemos começar com  $x = 1$  como a inversa de  $a$  módulo $2^1$ , aplicar o truque algumas vezes e em cada iteração dobramos o número de bits corretos de  $x$ .